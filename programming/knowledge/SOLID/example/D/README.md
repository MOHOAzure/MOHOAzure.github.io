## Dependency Inversion Principle
This states that classes should depend upon abstractions, not concretions. Essentially, don't depend on concrete classes, depend upon interfaces.

### Example

- Original code

  A PageLoader class that uses a MySqlConnection class to load pages from a database we might create the classes so that the connection class is passed to the constructor of the PageLoader class.

  ``` php
  class MySqlConnection {
      public function connect() {}
  }

  class PageLoader {
      private $dbConnection;
      public function __construct(MySqlConnection $dbConnection) {
          $this->dbConnection = $dbConnection;
      }
  }
  ```
  
- Analysis
  
  This structure means that we are essentially stuck with using MySQL for our database layer. What happens if we want to swap this out for a different database adaptor? We could extend the MySqlConnection class in order to create a connection to Memcache or something, but that would contravene the Liskov Substitution principle. Chances are that alternate database managers might be used to load the pages so we need to find a way to do this. The solution here is to create an interface called DbConnectionInterface and then implement this interface in the MySqlConnection class. Then, instead of relying on a MySqlConnection object being passed to the PageLoader class, we instead rely on any class that implements the DbConnectionInterface interface.

- SOLID code
  
  ``` php
  interface DbConnectionInterface {
      public function connect();
  } 

  class MySqlConnection implements DbConnectionInterface {
      public function connect() {}
  }

  class PageLoader {
      private $dbConnection;
      public function __construct(DbConnectionInterface $dbConnection) {
          $this->dbConnection = $dbConnection;
      }
  }
  ```
  With this in place we can now create a MemcacheConnection class and as long as it implements the DbConnectionInterface then we can use it in the PageLoader class to load pages. This approach also forces us to write code in such a way that prevents specific implementation details in classes that don't care about it. Because we have passed in a MySqlConnection class to our PageLoader class we shouldn't then write SQL queries in the PageLoader class. This means that when we pass in a MemcacheConnection object it will behave in the same way as any other type of connection class. When thinking about interfaces instead of classes it forces us to move that specific domain code out of our PageLoader class and into the MySqlConnection class.

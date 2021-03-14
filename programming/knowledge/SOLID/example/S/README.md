## Single Responsibility Principle
This states that a class should have a single responsibility, but more than that, a class should only have one reason to change.

### Example 
- Original code
  
  ``` php
  class Page {
    protected $title;

    public getPage($title) {
      return $this->title;
    }

    public function formatJson() {
      return json_encode($this->getTitle());
    }
  }
  ```
  
- Analysis
  This class knows about a title property and allows this title property to be retrieved by a get() method. We can also use a method in this class called formatJson() to return the page as a JSON string. This might seem like a good idea as the class is responsible for its own formatting. What happens, however, if we want to change the output of the JSON string, or to add another type of output to the class? We would need to alter the class to either add another method or change an existing method to suit. This is fine for a class as simple as this, but if it contained more properties then the formatting would be more complex to change. A better approach to this is to modify the Page class so that is only knows about the data is handles. We then create a secondary class called JsonPageFormatter that is used to format the Page objects into JSON.

- SOLID code
  
  ``` php
  class Page {
    protected $title;

    public getPage($title){
      return $this->title;
    }
  }

  class JsonPageFormatter {
      public function format(Page $page) {
          return json_encode($page->getTitle());
      }
  }
  ``` 
  
  Doing this means that if we wanted to create an XML format we could just add a class called XmlPageFormatter and write some simple code to output XML. We now have only one reason to change the Page class.

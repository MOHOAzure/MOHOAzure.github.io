## Liskov Substitution Principle
Created by Barbara Liskov in a 1987, this states that objects should be replaceable by their subtypes without altering how the program works. In other words, derived classes must be substitutable for their base classes without causing errors.

### Example 
- Original code

  ``` php
  class Rectangle {
    public function setWidth($w) { 
        $this->width = $w;
    }

    public function setHeight($h) {
        $this->height = $h;
    }

    public function getArea() {
        return $this->height * $this->width;
    }
  }
  ```
    
  Using that we can extend this into a Square class. Because a square a little different from a rectangle we need to override some of the code in order to allow a Square to exist correctly.
  
  ```php
  class Square extends Rectangle {
    public function setWidth($w) {
      $this->width = $w;
      $this->height = $w;
    }

    public function setHeight($h) {
      $this->height = $h;
      $this->width = $h;
    }
  }
  ```
    
- Analysis
  
  This seems fine, but ultimately a square is not a rectangle and so we have added code to force this situation to work. A good analogy that I read once was to think about a Duck and a Rubber Duck as represented by classes. Although it is possible to extend a Duck class into a Rubber Duck class we would need to override a lot of Duck functionality to suit the Rubber Duck. For example, a Duck quacks, but a Rubber Duck doesn't (ok, maybe it squeaks a bit), A Duck is alive, but a Rubber Duck isn't. Overriding lots of code in classes to suit specific situations can lead to maintenance problems. One solution to the rectangle vs square situation is to create an interface called Quadrilateral and implement this in separate Rectangle and Square classes. In this situation we are allowing the classes to be responsible for their own data, but enforcing the need for certain method footprints being available.
  
- SOLID code
  
  ``` php
  interface Quadrilateral {
    public function setHeight($h);

    public function setWidth($w);

    public function getArea();
  }

  class Rectangle implements Quadrilateral;

  class Square implements Quadrilateral;
  ```
  
  The bottom line here is that if you find you are overriding a lot of code then maybe your architecture is wrong and you should think about the Liskov Substitution principle.

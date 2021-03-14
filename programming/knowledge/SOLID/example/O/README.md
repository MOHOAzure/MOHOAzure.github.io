## Open/Closed Principle
In the open/closed principle classes should be open for extension, but closed for modification. Essentially meaning that classes should be extended to change functionality, rather than being altered.

### Example 
- Original code

  ``` php
  class Rectangle {
    public $width;
    public $height;
  }

  class Board {
    public $rectangles = [];
    public function calculateArea() {
      $area = 0;
      foreach ($this->rectangles as $rectangle) {
        $area += $rectangle->width * $rectangle->height;
      }
    }
  }
  ```
  
- Analysis

  We have a Rectangle class that contains the data for a rectangle, and a Board class that is used as a collection of Rectangle objects. With this setup we can easily find out the area of the board by looping through the items in the $rectangles collection and calculating their area. The problem with this setup is that we are restricted by the types of object we can pass to the Board class. For example, if we wanted to pass a Circle object to the Board class we would need to write conditional statements and code to detect and calculate the area of the Board. The correct way to approach this problem is to move the area calculation code into the shape class and have all shape classes extend a Shape interface. We can now create a Rectangle and Circle shape classes that will calculate their area when asked. The Board class can now be reworked so that it doesn't care what type of shape is passed to it, as long as they implement the area() method.

- SOLID code
  
  ``` php
  interface Shape {
     public function area();
  }

  class Rectangle implements Shape {
    public function area() {
      return $this->width * $this->height;
    }
  }

  class Circle implements Shape {
    public function area() {
      return $this->radius * $this->radius * pi();
    }
  }
  
  class Board {
    public $shapes;

    public function calculateArea() {
      $area = 0;
      foreach ($this->shapes as $shape) {
        $area+= $shape->area();
      }
      return $area;
    }
  }
  ```
  
  We have now setup these objects in a way that means we don't need to alter the Board class if we have a different type of object. We just create the object that implements Shape and pass it into the collection in the same way as the other classes.
  

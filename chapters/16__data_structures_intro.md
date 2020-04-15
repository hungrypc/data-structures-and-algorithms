# data structures intro

data structures are collections of values, the relationships among them, and the functions or operations that can be applied to the data
- different data structures excel at different things - some are highly specialized, while others (like arrays) are more generally used

## classes

a class is a blueprint for creating objects with pre-defined properties and methods

```js
class Student {
  contructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.tardies = 0;
  }

  // instance method
  markLate() {
    this.tardies++;
    return `${this.firstName} ${this.lastName} has been late ${this.tardies} times`;
  }

  // class method
  static enrollStudents(...students) {
    console.log('enrolling students');
  }
}

let studentOne = new Student('Phil', 'Chan');
let studentTwo = new Student('Xi', 'Lin');

studentOne.markLate(); // Phil Chan has been late n times
Student.enrollStudents(); // enrolling students
```

the method to create new objects **must** be called constructor
- instantiates new instances
the class keyword creates a constant, so you can not redefine it

instance methods provide functionality that pertains to a single instance of that particular class

class methods defines methods that are pertitent to classes but not necessarily individual instances of that class
- more like a utility function where it's not related to a single individual instance of that class where we're using data from that instance
```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  static distance(a, b) {
    const dx = a.x - b.x;
    const dy = a.y - b.y;

    return Math.hypot(dx, dy);
  }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);

Point.distance(p1, p2); // 7.00106...
```


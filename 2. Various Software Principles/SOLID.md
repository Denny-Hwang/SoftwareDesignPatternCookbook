SOLID is an acronym for a set of five design principles for object-oriented programming and design. These principles were first introduced by Robert C. Martin in his book “Agile Software Development, Principles, Patterns, and Practices”. The SOLID principles are intended to make software designs more maintainable and scalable.

## 2.1.1. Single Responsibility Principle (SRP)  
The Single Responsibility Principle states that a class should have only one reason to change. This means that a class should have only one responsibility and that responsibility should be entirely encapsulated by the class. A good way to check if a class has only one responsibility is to ask the question, “What is the main reason this class exists?”. If there is more than one answer to this question, the class probably has more than one responsibility.  
  
#### Code example in Java:  
```{.java}
// Good example
class Car {
    public void drive() {
        // code to drive the car
    }
}

// Bad example
class Car {
    public void drive() {
        // code to drive the car
    }
    public void honk() {
        // code to honk the horn
    }
}
```
  
#### Code example in C++:  
```{.cpp}
// Good example
class Car {
    public:
    void drive() {
        // code to drive the car
    }
};

// Bad example
class Car {
    public:
    void drive() {
        // code to drive the car
    }
    void honk() {
        // code to honk the horn
    }
};
```
In the good example, the class Car has only one responsibility, which is to drive. In the bad example, the class Car has two responsibilities, driving and honking. This violates the Single Responsibility Principle and makes the code harder to maintain.

## 2.1.2. Open-Closed Principle (OCP)  
The Open-Closed Principle states that a software module should be open for extension but closed for modification. This principle promotes code that is easy to understand, maintain, and extend.  
2.1.2.1. Extension  
The Open-Closed Principle encourages developers to design their code in a way that allows new functionality to be added through the use of inheritance or interfaces, without modifying existing code.  
2.1.2.2. Modification  
By following the Open-Closed Principle, developers can avoid the need to modify existing code when adding new functionality. This makes it easier to understand, maintain, and extend the codebase.  
2.1.2.3. Reusability  
The Open-Closed Principle promotes code that is reusable, making it easier to reuse existing code when adding new functionality.  

#### Code example in Java:  
```
// Good example
interface Shape {
    double getArea();
}
class Circle implements Shape {
    private double radius;
    public Circle(double radius) {
        this.radius = radius;
    }
    public double getArea() {
        return Math.PI * Math.pow(radius, 2);
    }
}
class Square implements Shape {
    private double side;
    public Square(double side) {
        this.side = side;
    }
    public double getArea() {
        return side * side;
    }
}
```  
In this example, the Shape interface and Circle and Square classes follow the Open-Closed Principle by allowing new shapes to be added through the use of inheritance, without modifying the existing Shape interface  

```
// Bad example (continued)
class Shape {
    public:
    double getArea(){
    return 0;
    }
};
class Circle: public Shape {
    private:
    double radius;
    public:
    Circle(double r) : radius(r) {}
    double getArea() {
        return 3.14159 * radius * radius;
    }
};
class Square: public Shape {
    private:
    double side;
    public:
    Square(double s) : side(s) {}
    double getArea() {
        return side * side;
    }
};
```

In this example, the Shape class and Circle and Square classes violate the Open-Closed Principle by modifying the existing Shape class when adding new shapes. This makes the codebase harder to understand, maintain and extend.

In the good examples, the Open-Closed Principle is followed by allowing new shapes to be added through the use of inheritance, without modifying the existing Shape interface. While in the bad examples, the principle is violated by modifying the existing Shape class when adding new shapes which makes the codebase harder to understand, maintain, and extend.

## 2.1.3. Liskov Substitution Principle (LSP)  
The Liskov Substitution Principle states that objects of a superclass should be able to be replaced with objects of a subclass without affecting the correctness of the program.  
#### Code example in Java:  
```{.java}
// Good example
class Rectangle {
    int width;
    int height;
    public int getWidth() { return width; }
    public void setWidth(int value) { width = value; }
    public int getHeight() { return height; }
    public void setHeight(int value) { height = value; }
    public int getArea() { return width * height; }
}
class Square extends Rectangle {
    public int getWidth() { return super.getWidth(); }
    public void setWidth(int value) { super.setWidth(value); super.setHeight(value); }
    public int getHeight() { return super.getHeight(); }
    public void setHeight(int value) { super.setWidth(value); super.setHeight(value); }
}
//In this example, a Square object can be used wherever a Rectangle object is expected because it adheres to the Liskov Substitution Principle by not changing the behavior of the parent class.

// Bad example
class Rectangle {
    int width;
    int height;
    public int getWidth() { return width; }
    public void setWidth(int value) { width = value; }
    public int getHeight() { return height; }
    public void setHeight(int value) { height = value; }
    public int getArea() { return width * height; }
}
class Square extends Rectangle {
    public int getWidth() { return super.getWidth(); }
    public void setWidth(int value) { width = value; }
    public int getHeight() { return super.getHeight(); }
    public void setHeight(int value) { height = value; }
}
```  
In this example, a Square object cannot be used wherever a Rectangle object is expected because it violates the Liskov Substitution Principle by changing the behavior of the parent class.  

## 2.1.4. Interface Segregation Principle (ISP)  
The Interface Segregation Principle states that a class should not be forced to implement interfaces it does not use. This principle promotes the creation of small, specific interfaces rather than large, general ones.  
#### Code example in Java:  
```{.java}
// Good example
interface Printer {
    void print();
}
interface Scanner {
    void scan();
}
class PrinterScanner implements Printer, Scanner {
    public void print() {
        // code to print
    }
    public void scan() {
        // code to scan
    }
}
//In this example, the PrinterScanner class implements only the interfaces that it needs and does not have to implement any unnecessary methods.
 
// Bad example
interface PrinterScanner {
    void print();
    void scan();
}
class Printer implements PrinterScanner {
    public void print() {
        // code to print
    }
    public void scan() {
        // code to scan
    }
}
```  
     
#### Code example in C++:  
```{.cpp}
// Good example
class Printer {
    public:
    virtual void print() = 0;
};
class Scanner {
    public:
    virtual void scan() = 0;
};
class PrinterScanner : public Printer, public Scanner {
    public:
    void print() {
        // code to print
    }
    void scan() {
        // code to scan
    }
};
//In this example, the PrinterScanner class implements only the interfaces that it needs and does not have to implement any unnecessary methods.
 
// Bad example
class PrinterScanner {
    public:
    virtual void print() = 0;
    virtual void scan() = 0;
};
class Printer : public PrinterScanner {
    public:
    void print() {
        // code to print
    }
    void scan() {
        // code to scan
    }
};
```  
In this example, the Printer class is forced to implement the scan() method even though it does not use it, violating the Interface Segregation Principle.


## 2.1.5. Dependency Inversion Principle (DIP)  
The Dependency Inversion Principle states that high-level modules should not depend on low-level modules, but both should depend on abstractions. This principle promotes the use of interfaces or abstract classes to create a clear separation between the high-level and low-level modules.

#### Code example in Java:  
```{.java}
// Good example
interface Printer {
    void print();
}
class ConsolePrinter implements Printer {
    public void print() {
        // code to print to console
    }
}
class Document {
    Printer printer;
    public Document(Printer printer) {
        this.printer = printer;
    }
    public void print() {
        printer.print();
    }
}
In this example, the high-level module (Document) depends on an abstraction (Printer) rather than a concrete implementation (ConsolePrinter). This allows for the low-level module (ConsolePrinter) to be easily swapped out with a different implementation without affecting the correctness of the program.  
// Bad example
class ConsolePrinter {
    public void print() {
        // code to print to console
    }
}
class Document {
    ConsolePrinter printer;
    public Document(ConsolePrinter printer) {
        this.printer = printer;
    }
    public void print() {
        printer.print();
    }
```  
In this example, the high-level module (Document) depends on a concrete implementation (ConsolePrinter) rather than an abstraction. This makes it difficult to swap out the low-level module (ConsolePrinter) with a different implementation without affecting the correctness of the program.


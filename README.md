# Interface Default and Static Methods

## Default Method

* default methods are implicitly public — there's no need to specify the public modifier.
* declared with the default keyword at the beginning of the method signature, and they provide an implementation.
* allow us to add new methods to an interface that are automatically available in the implementations.
* there's no need to modify the implementing classes.
* In this way, backward compatibility is neatly preserved without having to refactor the implementers.

```java

public interface Vehicle {
    
    String getBrand();
    
    String speedUp();
    
    String slowDown();
    
    default String turnAlarmOn() {
        return "Turning the vehicle alarm on.";
    }
    
    default String turnAlarmOff() {
        return "Turning the vehicle alarm off.";
    }
}

public class Car implements Vehicle {

    private String brand;
    
    // constructors/getters
    
    @Override
    public String getBrand() {
        return brand;
    }
    
    @Override
    public String speedUp() {
        return "The car is speeding up.";
    }
    
    @Override
    public String slowDown() {
        return "The car is slowing down.";
    }
}

public class Main {
    public static void main(String[] args) { 
        Vehicle car = new Car("BMW");
        System.out.println(car.getBrand());
        System.out.println(car.speedUp());
        System.out.println(car.slowDown());
        System.out.println(car.turnAlarmOn());
        System.out.println(car.turnAlarmOff());
    }
}
```

## Static Method

## Ref
* https://www.baeldung.com/java-static-default-methods

# Interface Default and Static Methods

## Default Method

* default methods are implicitly public — there's no need to specify the public modifier.
* declared with the default keyword at the beginning of the method signature, and they provide an implementation.
* allow us to add new methods to an interface that are automatically available in the implementations.
* there's no need to modify the implementing classes.
* In this way, backward compatibility is neatly preserved without having to refactor the implementers.
* The most typical use of default methods in interfaces is to incrementally provide additional functionality to a given type without breaking down the implementing classes.

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

### Multiple Interface Inheritance Rules

* what happens when a class implements several interfaces that define the same default methods.
* the code simply won't compile, as there's a conflict caused by multiple interface inheritance (a.k.a the Diamond Problem).

```java
public interface Alarm {

    default String turnAlarmOn() {
        return "Turning the alarm on.";
    }
    
    default String turnAlarmOff() {
        return "Turning the alarm off.";
    }
}

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

public class Car implements Vehicle, Alarm {
    // ...
}
```

* To solve this ambiguity, we must explicitly provide an implementation for the methods.

```java
public class Car implements Vehicle, Alarm {
    @Override
    public String turnAlarmOn() {
        // custom implementation
    }
        
    @Override
    public String turnAlarmOff() {
        // custom implementation
    }
}
```

* or we can use one of the two default implementation while overriding, or both

```java
public class Car implements Vehicle, Alarm {
    @Override
    public String turnAlarmOn() {
        return Vehicle.super.turnAlarmOn() + " " + Alarm.super.turnAlarmOn();
    }
        
    @Override
    public String turnAlarmOff() {
        return Vehicle.super.turnAlarmOff() + " " + Alarm.super.turnAlarmOff();
    }
}
```

## Static Method

## Ref
* https://www.baeldung.com/java-static-default-methods

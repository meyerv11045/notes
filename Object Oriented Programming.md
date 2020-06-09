## Object Oriented Programming:

### What is a Class:
- A blueprint
- Fields (instance variables)
  - What an object knows
- Methods(Functions)
  - What an object does

### What is Inheritance:
- Parent/Super class that shares fields/methods with its subclasses that also have their own fields & methods
- Subclasses abstract out the super class's features
- Subclasses can override or extend methods that don't work
- Subclasses only define the changes since the super's fields & methods are already defined when you extend the super class
- Use is A? principle to decide whether to extend a class
  - Ex: Is a Dog an Animal?
    - Yes, so Dog extends Animal
  - Ex: Is a Dog a cat?
    - No, so Dog doesn't extend Cat
- Use inheritance when a subclass needs most of the methods in the superclass
- Do not use inheritance just to reuse code if is A? doesn't work

``` Java
class Animal{
  private String name;
  private double height;
  private int weight;
  private String sound;
  
  public void setName(String newName){
    name = newName;
  }
  public void setSound(String newSound){
    sound = newSound;
  }
}

class Dog extends Animal{
  public Dog(){
    super(); //Calls super constructor
    setSound("Bark");
  }
  public void digHole(){
    System.out.println("Hole dug");
  }

}
```

### What is Encapsulation:
- Protects data
- Use private fields
- Do not set fields directly 
- Use public getter & setter functions to access & change the data
  - Setter = Mutator
  - Getter = Accessor 

```Java
class Dog{
  private double height;
  
  public void setHeight(newHeight){
    if(newHeight > 0){
      height = newHeight;
    }
    else{
      //Throw an Error
    }
  }
}
```
### Instance vs. Local Variables:
- Instance Variable(AKA fields) are declared in a class
- Local Variables are declared in a method

### What is Polymorphism:
- Allows you to write methods that don't need to change if new subclasses are created
  - Ex: Dog can add a new method w/o changing Animal
- Allows you to put diff subclasses in one array
```Java
Animal doggy = new Dog();
Animal kitty = new Cat();
Animal[] animals = [doggy,kitty];
kitty.getSound(); //Returns Meow 
doggy.digHole(); //Would not work 
((Dog)doggy).digHole(); //Would Work
```
- You can't access methods this way if they are only in the subclass
- Need to cast the object to the subclass that contains that method
- Cannot reference non-static variables or non-static-methods(w/o an object) in a static method
- Cannot access private methods outside of a subclass/class

### What is an Abstract Class:
- Gives power of polymorphism w/o all the work
- There are no abstract fields but can have protected variables that are rewritten as private fields in subclasses
- All methods do not have to be abstract w/in an abstract class
- You can have static methods w/in abstract classes
- Cannot create objects from abstract classes but subclasses can extend them and be made into objects
  - Have to override abstract methods in the subclass in order to extend the class
```Java
  abstract public Class Creature{
    protected String name;
    
    public abstract void setName(newName);
    
  }
```

### What is an Interface:
- A class w/ only abstract methods
- Can implement as many interfaces to a class as you want
- Can only use public static and final fields 
- Provide the ultimate flexibility
  - Classes from different inheritance trees can use a common interface 
- Avoid using interfaces just to force the creation of a method

```Java
public interface Living {
  public void setName(String newName);
}
public class Monkey implements Living{
  private name;
  public void setName(String newName){
    name = newName;
  }
}
```
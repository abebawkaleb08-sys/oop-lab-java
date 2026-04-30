# oop-lab-java


package inheritance_lab;

class Animal {
    protected String species;
    protected int age;
    private String secretCode = "ANIMAL-001";
    public String habitat;
    String dietType;

    public Animal() {
        System.out.println("Animal() constructor called (implicit super() to Object)");
        this.species = "Unknown";
        this.age = 0;
    }

    public Animal(String species, int age) {
        this();
        this.species = species;
        this.age = age;
        System.out.println("Animal(String, int) constructor called");
    }

    public void makeSound() {
        System.out.println("Animal makes a generic sound");
    }

    public void displayInfo() {
        System.out.println("Species: " + this.species + ", Age: " + this.age);
    }

    public String getSecretCode() {
        return this.secretCode;
    }

    public static void staticMethod() {
        System.out.println("Animal static method");
    }

    public final void finalMethod() {
        System.out.println("This is a final method - cannot be overridden!");
    }
}

class Dog extends Animal {
    private String breed;

    public Dog(String breed, int age) {
        super("Dog", age);
        this.breed = breed;
        System.out.println("Dog constructor called");
    }

    @Override
    public void makeSound() {
        System.out.println("Dog barks: Woof! Woof!");
    }

    public void displayParentInfo() {
        System.out.print("Calling parent displayInfo(): ");
        super.displayInfo();
    }

    public void showSpecies() {
        System.out.println("Species from parent: " + super.species);
    }

    public static void staticMethod() {
        System.out.println("Dog static method (HIDES Animal static method)");
    }

    public String getBreed() {
        return this.breed;
    }
}

class Puppy extends Dog {
    private String puppyName;

    public Puppy(String name, String breed, int age) {
        super(breed, age);
        this.puppyName = name;
        System.out.println("Puppy constructor called");
    }

    @Override
    public void makeSound() {
        System.out.println("Puppy whines: Yip! Yip!");
    }

    public void callGrandparentMethod() {
        super.displayParentInfo();
    }
}

class Cat extends Animal {
    private boolean isIndoor;

    public Cat(boolean indoor, int age) {
        super("Cat", age);
        this.isIndoor = indoor;
    }

    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow!");
    }

    public void purr() {
        System.out.println("Cat is purring...");
    }
}

class Bird extends Animal {
    private double wingspan;

    public Bird(double wingspan, int age) {
        super("Bird", age);
        this.wingspan = wingspan;
    }

    @Override
    public void makeSound() {
        System.out.println("Bird chirps: Tweet!");
    }

    public void fly() {
        System.out.println("Bird is flying with " + wingspan + "m wingspan");
    }
}

interface Flyable {
    void flyHigh();
}

interface Swimmable {
    void swimDeep();
}

class Duck extends Animal implements Flyable, Swimmable {
    public Duck(int age) {
        super("Duck", age);
    }

    @Override
    public void makeSound() {
        System.out.println("Duck quacks: Quack!");
    }

    @Override
    public void flyHigh() {
        System.out.println("Duck flying high!");
    }

    @Override
    public void swimDeep() {
        System.out.println("Duck swimming deep!");
    }
}

final class FinalClass {
    private int value;

    public FinalClass(int value) {
        this.value = value;
    }

    public void show() {
        System.out.println("FinalClass value: " + value);
    }
}

public class InheritanceLab {

    public static void animalSoundTest(Animal animal) {
        System.out.println("\n--- Testing polymorphism ---");
        System.out.println("Object type: " + animal.getClass().getSimpleName());
        animal.makeSound();
    }

    public static void main(String[] args) {

        Dog myDog = new Dog("Golden Retriever", 5);
        myDog.displayInfo();
        myDog.makeSound();

        myDog.displayParentInfo();
        myDog.showSpecies();

        Puppy myPuppy = new Puppy("Buddy", "Labrador", 1);
        myPuppy.makeSound();
        myPuppy.callGrandparentMethod();

        Cat myCat = new Cat(true, 3);
        Bird myBird = new Bird(1.5, 2);

        myCat.makeSound();
        myBird.makeSound();
        myBird.fly();

        Animal[] zoo = { myDog, myCat, myBird, myPuppy };
        for (Animal animal : zoo) {
            animalSoundTest(animal);
        }

        Animal upcastedDog = new Dog("Beagle", 4);
        upcastedDog.makeSound();

        if (upcastedDog instanceof Dog) {
            Dog downcastedDog = (Dog) upcastedDog;
            System.out.println("Downcast successful! Breed: " + downcastedDog.getBreed());
        }

        Animal.staticMethod();
        Dog.staticMethod();

        Animal refToDog = new Dog("Poodle", 3);
        refToDog.staticMethod();

        Duck myDuck = new Duck(2);
        myDuck.makeSound();
        myDuck.flyHigh();
        myDuck.swimDeep();

        FinalClass finalObj = new FinalClass(100);
        finalObj.show();
    }
}
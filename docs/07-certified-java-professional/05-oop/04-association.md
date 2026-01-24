# Association

It is not a design principle like SOLID. \
It is a fundamental relationship concept in OOP. \
It describes a `has-a` or `part-of` relationship. \
Understanding association is crucial for `Favor Composition over Inheritance` design principle.


## Key Characteristics
- Multiplicity: The relationship can be one-to-one, one-to-many, many-to-one, many-to-many.

## Two Specialised forms of Association
1. Aggregation (Weak Association) : 
    - In this `has-a` relationship, child/children can exist independently of the parent. 
    - Usually child is passed as an argument to a constructor or setter method of the parent.

```java
class Professor {
    private String name;
    Professor(String name) {this.name = name;}
}

class Department {
    private String deptName;
    private List<Professor> professors;
    
    // The Professor objects are created elsewhere
    // This is Aggregation
    Department(String deptName, List<Professor> professors) {
        this.deptName = deptName;
        this.professors = professors;
    }

    public void displayInfo() {
        System.out.println("The " + this.deptName + " department has " + this.professors.length + " professors.");
    }
}

```

2. Composition (Strong Association)
    - This is a `part-of` relationship where the child cannot exists without the parent.
    - Usually the children are instantiated inside the parent's constructor.

```java
class Room {
    private String type;
    Room(String type) {this.type = type;}

}

class House {
    private List<Rooms> rooms;

    public House() {
        this.rooms = new ArrayList<>();
        //  The Room objects are created inside the House
        // They cannot exist without the House. This is Composition.
        rooms.add(new Room("Bedroom"));
        rooms.add(new Room("Kitchen"));
    }

}
```

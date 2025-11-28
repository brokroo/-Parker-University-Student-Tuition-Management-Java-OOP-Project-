# 📘 Parker University – Student Tuition Management (Java OOP Project)

This project implements an **Object-Oriented Tuition System** for Parker University using:
✔ Inheritance  
✔ Abstraction  
✔ Method Overriding  
✔ Polymorphism  

The project defines a base `Student` class and three subclasses, each with its own tuition fee calculation.  
It also includes a demo driver program that creates student objects and prints their details.

---

## 📁 Project Files

| File Name | Description |
|----------|-------------|
| `Student.java` | Abstract parent class — contains ID, name, tuition fields |
| `UndergraduateStudent.java` | Child class → tuition `$4,000 per semester` |
| `GraduateStudent.java` | Child class → tuition `$6,000 per semester` |
| `StudentAtLarge.java` | Child class → tuition `$2,000 per semester` |
| `StudentDemo.java` | Main program to create and test all students |

---

## 🧩 Class Structure Diagram

           [ Student ] (abstract)
            /    |     \
           /     |      \

## Student.java
```
/**
 * Student.java
 * Abstract bean class for Parker University students.
 */

public abstract class Student {
    private int studentId;
    private String lastName;
    private double annualTuition;

    /**
     * Constructor requiring ID and last name.
     * @param studentId student ID number
     * @param lastName student's last name
     */
    public Student(int studentId, String lastName) {
        this.studentId = studentId;
        this.lastName = lastName;
    }

    // Getters and setters for each field
    public int getStudentId() {
        return studentId;
    }

    public void setStudentId(int studentId) {
        this.studentId = studentId;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public double getAnnualTuition() {
        return annualTuition;
    }

    /**
     * Concrete setter for annual tuition (keeps option to explicitly set tuition).
     * Subclasses will implement setTuition() to compute/set the tuition according to type.
     */
    public void setAnnualTuition(double annualTuition) {
        this.annualTuition = annualTuition;
    }

    /**
     * Abstract method that subclasses must implement to set tuition
     * according to their own rules (e.g., per-semester rates).
     */
    public abstract void setTuition();

    @Override
    public String toString() {
        return String.format("%s{id=%d, lastName='%s', annualTuition=$%.2f}",
                this.getClass().getSimpleName(),
                getStudentId(),
                getLastName(),
                getAnnualTuition());
    }
}

```

## UndergraduateStudent.java

```
/**
 * UndergraduateStudent.java
 * Undergraduate student: $4,000 per semester.
 */

public class UndergraduateStudent extends Student {

    private static final double PER_SEMESTER = 4000.0;

    public UndergraduateStudent(int studentId, String lastName) {
        super(studentId, lastName);
    }

    /**
     * Sets annual tuition as 2 * per-semester tuition.
     */
    @Override
    public void setTuition() {
        setAnnualTuition(PER_SEMESTER * 2);
    }
}

```
## GraduateStudent.java
```
/**
 * GraduateStudent.java
 * Graduate student: $6,000 per semester.
 */

public class GraduateStudent extends Student {

    private static final double PER_SEMESTER = 6000.0;

    public GraduateStudent(int studentId, String lastName) {
        super(studentId, lastName);
    }

    /**
     * Sets annual tuition as 2 * per-semester tuition.
     */
    @Override
    public void setTuition() {
        setAnnualTuition(PER_SEMESTER * 2);
    }
}

```

## StudentAtLarge.java
```
/**
 * StudentAtLarge.java
 * Student-at-large: $2,000 per semester.
 */

public class StudentAtLarge extends Student {

    private static final double PER_SEMESTER = 2000.0;

    public StudentAtLarge(int studentId, String lastName) {
        super(studentId, lastName);
    }

    /**
     * Sets annual tuition as 2 * per-semester tuition.
     */
    @Override
    public void setTuition() {
        setAnnualTuition(PER_SEMESTER * 2);
    }
}

```
## StudentDemo.java
```
/**
 * StudentDemo.java
 * Demonstrates creating and using Student objects of different types.
 */

public class StudentDemo {
    public static void main(String[] args) {
        Student[] students = new Student[] {
            new UndergraduateStudent(1001, "Smith"),
            new GraduateStudent(1002, "Johnson"),
            new StudentAtLarge(1003, "Williams"),
            new UndergraduateStudent(1004, "Brown"),
            new GraduateStudent(1005, "Jones"),
            new StudentAtLarge(1006, "Davis")
        };

        // Set tuition for each student according to their type and print
        System.out.println("Initial student list:");
        for (Student s : students) {
            s.setTuition();
            System.out.println(s);
        }

        // Demonstrate usage of setters/getters
        System.out.println("\nDemonstrating setters/getters with first student:");
        Student first = students[0];
        System.out.println("Before update: " + first);

        first.setStudentId(1101);
        first.setLastName("Smithers");
        // you can also explicitly set annual tuition if needed:
        // first.setAnnualTuition(9000.00);
        // or recalculate via setTuition():
        first.setTuition();

        System.out.println("After update:  " + first);
    }
}

```
## Expected Output
```
Initial student list:
UndergraduateStudent{id=1001, lastName='Smith', annualTuition=$8000.00}
GraduateStudent{id=1002, lastName='Johnson', annualTuition=$12000.00}
StudentAtLarge{id=1003, lastName='Williams', annualTuition=$4000.00}
UndergraduateStudent{id=1004, lastName='Brown', annualTuition=$8000.00}
GraduateStudent{id=1005, lastName='Jones', annualTuition=$12000.00}
StudentAtLarge{id=1006, lastName='Davis', annualTuition=$4000.00}
```

# school-notes
dump of my school notes


## c2030s

### week 1
- T `:<` S (`T` is is the type, `S` is the supertype). From `S` to `T`, GO **DOWN** IS *NARROWING CONVERSION*
  
<img width="998" alt="Screenshot 2024-08-13 at 3 06 24 AM" src="https://github.com/user-attachments/assets/db6b199d-4e98-4c70-9ac9-5308e346e146">

[https://nus-cs2030s.github.io/2425-s1/index.html](https://nus-cs2030s.github.io/2425-s1/index.html)


<img width="755" alt="Screenshot 2024-08-13 at 3 11 17 AM" src="https://github.com/user-attachments/assets/aec0d900-979e-40a2-9ede-04b330bc0e07">

### week 2
[https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html](https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html)

- Instance methods can access both instance AND class variables/methods
- Class methods can only access class variables/methods BUT NOT instance variables/access

For example, the following code wouldn't compile:
```java
public class A {
  private int x;

  // class method cannot access instance variables/methods!
  public static getX() {
    return this.x;
  }
}
```

- Constructors can be public/private
- A potential use case for private constructors would be delegation of public constructors to the private constructor:

```java
public class MyClass {
     private final String value;
     private final String type;

     public MyClass(int x){
         this(Integer.toString(x), "int");
     }

     public MyClass(boolean x){
         this(Boolean.toString(x), "boolean");
     }

     private MyClass(String value, String type){
         this.value = value;
         this.type = type;
     }
}
```

- Overriding equals method, [source](https://stackoverflow.com/questions/8180430/how-to-override-equals-method-in-java)
```java
// METHOD OVERLOADING
public boolean equals(People other){

// ACTUALLY OVERRIDES EQUAL
@Override // this annoation is not actually required, but it makes code 1) readable, 2) catches bug at compile-time
public boolean equals(Object other){
```

### week 3

- overloading depends on method signature (same name is OK, different parameters list)

Following code only throws runtime error *NOT COMPILE-TIME ERROR*, coz runtime type of `o` can be Circle
```java
class Circle {
  /...
}
public void f(Object o) {
  Circle c = (Circle) o; // narrowing conversion
}
```

To prevent runtime error,
```java
class Circle {
  /...
}
public void f(Object o) {
  if (o instanceof Circle) {
      Circle c = (Circle) o; // narrowing conversion
  }
}
```

- Widening conversion on the other hand is always okay tho!
- Don't even need typecasting
```java
class Circle {
  /...
}
public void f(Circle c) {
  Object o = c;
}
```
<img width="573" alt="Screenshot 2024-08-28 at 4 29 39 PM" src="https://github.com/user-attachments/assets/b6403e57-9827-42eb-b193-42cf11aef24a">

- Dynamic binding only applies to instance method invocation!

- Overidding 2-step process
  - Check if method signature is the same
  - If it is, check the return type. ensure return type is the type or subtype.
 ```java
class A {
    public A gay() {
        System.out.println("A::gay");
        return null;
    }
}

class B extends A {
    // return type is actual type
    @Override
    public A gay() {
        System.out.println("B::gay");
        return null;
    }
    
    // return type is a subtype
    @Override
    public B gay() {
        System.out.println("B::gay");
        return null;
    }
    
    // doesnt work coz diff return type
    @Override
    public int gay() {
        System.out.println("B::gay");
        return null;
    }
    
    // this is method overloading !
    public A gay(int x) {
        System.out.println("B::gay");
        return null;
    }
}
```

- Abstract classes
  
<img width="1436" alt="Screenshot 2024-08-28 at 4 31 52 PM" src="https://github.com/user-attachments/assets/26d38dc9-a1fe-455a-a589-086e0d8a1640">

- Interfaces

<img width="1440" alt="Screenshot 2024-08-28 at 4 36 05 PM" src="https://github.com/user-attachments/assets/35d6deda-e822-42de-9cbc-30f49c278995">

## cs2100

<img width="358" alt="Screenshot 2024-08-18 at 2 53 35 AM" src="https://github.com/user-attachments/assets/80e0cd4e-5e34-4efc-bbec-e3060b2340a4">

<img width="505" alt="Screenshot 2024-08-18 at 3 25 16 AM" src="https://github.com/user-attachments/assets/aa6d20d4-d7df-4433-8e87-5f6b57cac0f0">

- unsigned numbers: non-negative values
- signed numbers: all values

<img width="499" alt="Screenshot 2024-08-18 at 3 20 00 AM" src="https://github.com/user-attachments/assets/5cee56ba-897f-4e7a-8b49-600df418eb17">

- Given a number `x` which can be expressed as an `n-bit` binary number, its negated value can be obtained in 1s complement representation with `-x = 2^n - x - 1`.
- Or can you just invert the bits LMAO

```
x = 12 = b00001100
-x = 2^8 - 12 - 1 = 243 = b11110011
```

<img width="368" alt="Screenshot 2024-08-18 at 3 20 56 AM" src="https://github.com/user-attachments/assets/ede46323-9bb2-4425-b975-db3120096fcf">

<img width="507" alt="Screenshot 2024-08-18 at 3 26 56 AM" src="https://github.com/user-attachments/assets/e17b2ba2-9ff4-4a1b-8dfc-88eacadab7c4">

- Given a number `x` which can be expressed as an `n-bit` binary number, its negated value can be obtained in 2s complement representation with `-x = 2^n - x`.
- Or can you just invert the bits and +1 
```
x = 12 = b00001100
-x = 2^8 - 12 = 244 = b11110100

INVERSION of bits
b00001100 = b11110011
ADD ONE
b11110011 = b11110100


Prof Colin trick: From its positive equivalent in 2s complement representation, find the first 1 leftwards and invert everything after
11110100

REMEMBER TO THROW AWAY THE DP for fractional numbers
```

<img width="498" alt="Screenshot 2024-08-18 at 3 32 44 AM" src="https://github.com/user-attachments/assets/eb9f8de2-0aaf-4261-b179-0f60d4f175f7">

```
Prof Colin trick: Given an 4-bit number in 2s complement, represent the MSB (i.e signed bit) as negative (-2^n-1) to facilitate conversion

-8  |  4  |  2  |   1

Prof Colin trick: Given an 4-bit number in 1s complement, represent the MSB (i.e signed bit) as negative (-2^n-1 + 1) to facilitate conversion

-7  |  4  |  2  |   1
```

<img width="464" alt="Screenshot 2024-08-18 at 4 38 15 PM" src="https://github.com/user-attachments/assets/0eae3eed-39b1-4d69-bc89-b8581ea5021e">

### excess-4 representation

- convert the binary to integer, account for offset of 4
- Given n-bit number, do an excess of 2^(n-1) representation.(i.e 3-bit, we do excess 4 representation | for 4-bit, we do excess 8 representation)

  
<img width="469" alt="Screenshot 2024-08-18 at 5 00 54 PM" src="https://github.com/user-attachments/assets/ff9ab727-3faa-4e17-8439-8f5d051149fc">

<img width="460" alt="Screenshot 2024-08-18 at 5 03 57 PM" src="https://github.com/user-attachments/assets/aa8b9176-a88a-470e-92b4-f26f9d8b2ef7">

### week 3

- MIPS register stats
<img width="500" alt="Screenshot 2024-08-28 at 5 03 36 PM" src="https://github.com/user-attachments/assets/6c68c060-af15-49b2-9494-4afda5938986">

- `add` and `addi` command in MIPS
<img width="500" alt="Screenshot 2024-08-28 at 5 05 14 PM" src="https://github.com/user-attachments/assets/a70a2acb-84ef-462e-ad54-f677d047e0d3">

<img width="500" alt="Screenshot 2024-08-28 at 5 17 27 PM" src="https://github.com/user-attachments/assets/e9d68399-f42e-459a-a4cf-08ac1a78a915">

- assignment operator in MIPS

<img width="500" alt="Screenshot 2024-08-28 at 5 20 20 PM" src="https://github.com/user-attachments/assets/0c7b43c8-8fad-48a6-bf52-7ed61928869e">
<img width="500" alt="Screenshot 2024-08-28 at 5 44 08 PM" src="https://github.com/user-attachments/assets/e2083229-e38e-4dd7-8658-b29942f3609c">
<img width="500" alt="Screenshot 2024-08-28 at 5 44 21 PM" src="https://github.com/user-attachments/assets/9c3ec645-42ea-4497-ae24-8bd8f90bd5e0">
<img width="500" alt="Screenshot 2024-08-28 at 5 45 04 PM" src="https://github.com/user-attachments/assets/eed9e718-834e-4f22-8c0c-63ff0598d392">
<img width="500" alt="Screenshot 2024-08-28 at 5 45 14 PM" src="https://github.com/user-attachments/assets/dd245783-0c99-4c9f-8de2-082b04731ca6">
<img width="500" alt="Screenshot 2024-08-28 at 5 47 55 PM" src="https://github.com/user-attachments/assets/1aa68e62-221e-4072-a48d-6316816e157a">
<img width="500" alt="Screenshot 2024-08-28 at 5 47 43 PM" src="https://github.com/user-attachments/assets/48b5a3be-1b5a-4538-bbe0-49d413e7de4d">

<img width="806" alt="Screenshot 2024-08-28 at 6 02 13 PM" src="https://github.com/user-attachments/assets/dc5a429a-7996-45c1-80c3-eafa424b9d38">


EXCEPT FOR ANDI, ORI, AND XORI

<img width="1037" alt="Screenshot 2024-09-05 at 12 52 06 AM" src="https://github.com/user-attachments/assets/2cc68e6b-721d-4ba7-88d0-a4cf42c3e59f">
<img width="1031" alt="Screenshot 2024-09-05 at 1 09 09 AM" src="https://github.com/user-attachments/assets/5af563b4-f40b-4620-a183-2f473ab5b126">

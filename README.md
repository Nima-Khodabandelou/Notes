# java_core

Core concepts of Java SE

- Main Java features:

      Used for Desktop, Mobile, and Web application development
    
      Platform-independent
    
      Robust
    
      Secure
    
      High-level
    
      Multi-threaded
    
- Does not support:

      pointers (Handles it internally)
    
      goto
    
      operator overloading
    
      call by reference
    
      structures and unions

- Super keyword:

       A reference variable used for refering to the immediate parent class object
       
       Called implicitly by the class constructor if not provided  
       
       Can refer to immediate parent class instance variable
       
       For immediate parent class method invocation
       
       To differentiate between local and instance variables in the class constructor
       
       Must be the first statement in constructor
       
- Path and Classpath:

       PATH: An environment variable used by the operating system to locate the executables

       Classpath: Java specific used to locate class files. it can be a directory, ZIP, JAR files etc.

- Source files: 

       Each source Java file may have multiple classes among which only one shall be public.
       
       Source file name shall be the same as class name.
       


- OS Architecture: Java is neutral w.r.t to OS architecture (32 bit or 64 bit).

- Interpreter/Compiler:

      Just-in-time (JIT): An interpreter to improve performance 

      Compiler: transforms instruction set of a Java virtual machine (JVM) to the instruction set of a specific CPU (Java code to Bytecode).

      JIT compiles parts of the bytecode having similar functionality, and therefore reduces compilation time. 

      Classloader: JVM subsystem  for loading class files using java.lang.ClassLoader.loadClass(). part of the Java Runtime Environment

      Three built-in classloaders:

            Bootstrap ClassLoader: The first classloader in native code (e.g. c++) which loads rt.jar file containing all core libraries and class files of Java SE
                                   There are various implementations of this Bootstrap class loader for various platforms.

            Extension ClassLoader: Its parent is Bootstrap classloader used for loading Java core extension classes in order to be available to all applications                                          running on each platform. 

            System/Application ClassLoader: loads our files in the classpath.
            
- Local variables: not initialized to any default value.

- Acccess modifiers:

      Default: accessible within the package only.
      
      Protected: accessible by the class and sub-class of the same package, or by the sub-class in another packages.
      
      Public: accessible anywhere
      
      Private: accessible within the class
       
       
       
       
       
       
       
       
       
       







/**
SOLID Principles:
1- Single Responsibility : a class should only have one responsibility. Furthermore, it should only have
   one reason to change. benefits:
	 Testing – A class with one responsibility will have far fewer test cases.
	 Lower coupling – Less functionality in a single class will have fewer dependencies.
	 Organization – Smaller, well-organized classes are easier to search than monolithic ones.
2- Open/Closed: Open for Extension, Closed for Modification.
   we stop ourselves from modifying existing code and causing potential new bugs.
   one exception to the rule is when fixing bugs in existing code. let's stick to the open-closed
   principle and simply extend our class
3- Liskov Substitution: if class A is a subtype of class B, we should be able to replace B with A
   without disrupting the behavior of our program. */
public interface Car {
	void turnOnEngine();
	void accelerate();
}
public class MotorCar implements Car {

    private Engine engine;

    //Constructors, getters + setters

    public void turnOnEngine() {
        //turn on the engine!
        engine.on();
    }

    public void accelerate() {
        //move forward!
        engine.powerOn(1000);
    }
}
// As our code describes, we have an engine that we can turn on, and we can increase the power.
// But wait — we are now living in the era of electric cars:
public class ElectricCar implements Car {

    public void turnOnEngine() {
        throw new AssertionError("I don't have an engine!");
    }

    public void accelerate() {
        //this acceleration is crazy!
    }
}
/**
By throwing a car without an engine into the mix, we are inherently changing the behavior
of our program. This is a blatant violation of Liskov substitution and is a bit harder to
fix than our previous two principles. One possible solution would be to rework our model
into interfaces that take into account the engine-less state of our Car. */
4- Interface Segregation: larger interfaces should be split into smaller ones. By doing so,
   we can ensure that implementing classes only need to be concerned about the methods that
   are of interest to them.
5- Dependency Inversion: The principle of dependency inversion refers to the decoupling of
   software modules. This way, instead of high-level modules depending on low-level modules,
   both will depend on abstractions. Abstractions should not depend on details. Details
   should depend on abstractions.
ex:
public class BackEndDeveloper {

    public void writeJava() {
    }
}   
public class FrontEndDeveloper {

    public void writeJavascript() {
    }

}
public class Project {

    private BackEndDeveloper backEndDeveloper = new BackEndDeveloper();
    private FrontEndDeveloper frontEndDeveloper = new FrontEndDeveloper();

    public void implement() {

        backEndDeveloper.writeJava();
        frontEndDeveloper.writeJavascript();
    }

}
as we can see, the Project class is a high-level module, and it depends on low-level modules such 
as BackEndDeveloper and FrontEndDeveloper. methods writeJava and writeJavascript are methods bound 
to the corresponding classes. to tackle this problem -> introduce abstraction and then refactor: 
public interface Developer {

    void develop();
}
public class BackEndDeveloper implements Developer {

    @Override
    public void develop() {
        writeJava();
    }

    private void writeJava() {
    }

}
public class FrontEndDeveloper implements Developer {

    @Override
    public void develop() {
        writeJavascript();
    }

    public void writeJavascript() {
    }

}
public class Project {

    private List<Developer> developers;

    public Project(List<Developer> developers) {

        this.developers = developers;
    }

    public void implement() {

        developers.forEach(d->d.develop());
    }

}

Java is architectural neutral as it is not dependent on the architecture (32 bit or 64 bit).

uses the Just-in-time (JIT) interpreter along with the compiler. Just-In-Time(JIT) compiler: It is used
to improve the performance.
JIT compiles parts of the bytecode that have similar
functionality at the same time, and hence reduces the amount of time needed for compilation. Here the
term “compiler” refers to a
translator from the instruction set of a Java virtual
machine (JVM) to the instruction set of a specific CPU.

Classloader is a subsystem of JVM which is used to load class files. Whenever we run the java program,
it is loaded first by the classloader.
There are three built-in classloaders in Java.

Bootstrap ClassLoader: This is the first classloader written in native code. It loads the rt.jar file
which contains all class files of Java
Standard Edition like
  java.lang, java.net, java.util, java.io, java.sql, etc., and other core libraries located in the
   $JAVA_HOME/jre/lib directory. Different
  platforms might have different implementations of this particular class loader.
Extension ClassLoader: This is the child classloader of Bootstrap. load classes that are an extension
  of the standard core Java classes.so that they're available to all applications running on the platform.
  The extension class loader loads from the JDK extensions directory, usually the $JAVA_HOME/lib/ext
  directory, or
  any other directory mentioned in the java.ext.dirs
  system property.
System/Application ClassLoader: loads our own files in the classpath.
Class loaders are part of the Java Runtime Environment. When the JVM requests a class, the class loader
 tries to locate the class and load
 the class definition into the runtime using the fully
 qualified class name. The java.lang.ClassLoader.loadClass() method is responsible for loading the class
 definition into runtime. It tries
 to load the class based on a fully qualified name.
 If the class isn't already loaded, it delegates the request to the parent class loader. This process
 happens recursively. Eventually, if the
 parent class loader doesn’t find the class, then
 the child class will call the java.net.URLClassLoader.findClass() method to look for classes in the
 file system itself. If the last child
 class loader isn't able to load the class either,
 it throws java.lang.NoClassDefFoundError or java.lang.ClassNotFoundException.

delete, next, main, exit or null are not keyword

The local variables are not initialized to any default value, neither primitives nor object references.

Default Default are accessible within the package only. Protected can be accessed by the class and
sub-class of the same package, or by the
sub-class in another packages.

A final class cannot be subclassed. A final method cannot be overridden.
If we follow the rules of good design strictly, we should create and document a class carefully or
declare it final for safety reasons.
However, we should use caution when creating final classes.
Notice that making a class final means that no other programmer can improve it. Imagine that we're
using a class and don’t have the source
code for it, and there's a problem with one method.
If the class is final, we can’t extend it to override the method and fix the problem. In other words,
we lose extensibility, one of the
benefits of object-oriented programming.
If some methods of our class are called by other methods, we should consider making the called methods
final. Otherwise, overriding them
can affect the work of callers and cause surprising results.
If our constructor calls other methods, we should generally declare these methods final for the above
reason. What’s the difference between
making all methods of the class final and marking
the class itself final? In the first case, we can extend the class and add new methods to it. In the
second case, we can’t do this.
If we have a final reference variable, we can’t reassign it either. But this doesn’t mean that the
object it refers to is immutable. We can
change the properties of this object freely.
let’s declare the final reference variable cat and initialize it:
 final Cat cat = new Cat();
If we try to reassign it we’ll see a compiler error But we can change the properties of Cat instance
 cat.setWeight(5);
Final fields can be either constants or write-once fields. To distinguish them, we should ask a
 question — would we include this field if we
 were to serialize the object?
If no, then it’s not part of the object, but a constant. Note that according to naming conventions,
 class constants should be uppercase, with
 components separated by underscore (“_”) characters:
 static final int MAX_WIDTH = 999;
Note that any final field must be initialized before the constructor completes. For static final
 fields, this means that we can initialize them:
upon declaration as shown in the above example
in the static initializer block
For instance final fields, this means that we can initialize them:
upon declaration
in the instance initializer block
in the constructor
A final argument can’t be changed inside a method:
	public void methodWithFinalArguments(final int x) {
		x=1;
	}
The above assignment causes the compiler error.
Immutability means once we create an object, we are not allowed to change the content of that object.
 If we try to change the content and the
 alteration is successfully done with those changes,
in such a case, a new object will be created. If there are no changes in the content, the existing
 object will be reused.

An object is immutable when its state doesn’t change after it has been initialized. For example,
 String is an immutable class and, once instantiated,
 the value of a String object never changes.
Because an immutable object can’t be updated, programs need to create a new object for every change
 of state. However, immutable objects also have
 the following benefits:
	An immutable class is good for caching purposes because you don’t have to worry about the value
	changes.
	An immutable class is inherently thread-safe, so you don’t have to worry about thread safety in
	multi-threaded environments.
To create an immutable class in Java, you need to follow these general principles:
	Declare the class as final so it can’t be extended.
	Make all of the fields private so that direct access is not allowed.
	Don’t provide setter methods for variables.
	Make all mutable fields final so that a field’s value can be assigned only once.
	Initialize all fields using a constructor method performing deep copy.
	Perform cloning of objects in the getter methods to return a copy rather than returning the actual
	object reference.
Example: */
public final class FinalClassExample {
	// fields of the FinalClassExample class
	private final int id;	
	private final String name;	
	private final HashMap<String,String> testMap;	
	public int getId() {
		return id;
	}
	public String getName() {
		return name;
	}
	// Getter function for mutable objects
	public HashMap<String, String> getTestMap() {
		return (HashMap<String, String>) testMap.clone();
	}
	// Constructor method performing deep copy	
	public FinalClassExample(int i, String n, HashMap<String,String> hm){
		System.out.println("Performing Deep Copy for Object initialization");

		// "this" keyword refers to the current object
		this.id=i;
		this.name=n;
		HashMap<String,String> tempMap=new HashMap<String,String>();
		String key;
		Iterator<String> it = hm.keySet().iterator();
		while(it.hasNext()){
			key=it.next();
			tempMap.put(key, hm.get(key));
		}
		this.testMap=tempMap;
	}
	// Test the immutable class
	public static void main(String[] args) {
		HashMap<String, String> h1 = new HashMap<String,String>();
		h1.put("1", "first");
		h1.put("2", "second");		
		String s = "original";		
		int i=10;		
		FinalClassExample ce = new FinalClassExample(i,s,h1);		
		// print the ce values
		System.out.println("ce id: "+ce.getId());
		System.out.println("ce name: "+ce.getName());
		System.out.println("ce testMap: "+ce.getTestMap());
		// change the local variable values
		i=20;
		s="modified";
		h1.put("3", "third");
		// print the values again
		System.out.println("ce id after local variable change: "+ce.getId());
		System.out.println("ce name after local variable change: "+ce.getName());
		System.out.println("ce testMap after local variable change: "+ce.getTestMap());		
		HashMap<String, String> hmTest = ce.getTestMap();
		hmTest.put("4", "new");		
		System.out.println("ce testMap after changing variable from getter methods: "+ce.getTestMap());
	}
}
/**
Output:
	Performing Deep Copy for Object initialization
	ce id: 10
	ce name: original
	ce testMap: {1=first, 2=second}
	ce id after local variable change: 10
	ce name after local variable change: original
	ce testMap after local variable change: {1=first, 2=second}
	ce testMap after changing variable from getter methods: {1=first, 2=second}
The output shows that the HashMap values didn’t change because the constructor uses deep copy and the
 getter function returns a clone of the
 original object.
You can make changes to the FinalClassExample.java file to show what happens when you use shallow copy
 instead of deep copy and return the object
 insetad of a copy.
Make the following changes:*/
// Getter function for mutable objects
	public HashMap<String, String> getTestMap() {
		return testMap;
	}
	//Constructor method performing shallow copy
	public FinalClassExample(int i, String n, HashMap<String,String> hm){
		System.out.println("Performing Shallow Copy for Object initialization");
		this.id=i;
		this.name=n;
		this.testMap=hm;
	}
/**	
Output:
Performing Shallow Copy for Object initialization
ce id: 10
ce name: original
ce testMap: {1=first, 2=second}
ce id after local variable change: 10
ce name after local variable change: original
ce testMap after local variable change: {1=first, 2=second, 3=third}
ce testMap after changing variable from getter methods: {1=first, 2=second, 3=third, 4=new}

The methods or variables defined as static are shared among all the objects of the class. The static
 is the part of the class and not of the object.
The static variables are stored in the class area, and we do not need to create the object to access
 such variables.

There are various advantages of defining packages in Java. avoid the name clashes. provides easier
 access control. can  have the hidden classes.
It is easier to locate the related classes.

The Object is the real-time entity having some state and behavior. In Java, Object is an instance of
 the class having the instance variables as the
state of the object and the methods as the behavior of the object. The object of a class can be created
 by using the new keyword.

All object references are initialized to null in Java.

The constructor can be defined as the special type of method that is used to initialize the state of an
 object. It is invoked when the class is
 instantiated,
and the memory is allocated for the object. Every time, an object is created using the new keyword, the
 default constructor of the class is called.
The name of the constructor must be similar to the class name. The constructor must not have an explicit
 return type.
The parameterized constructor is the one which can initialize the instance variables with the given values.
The default constructor is mainly used to initialize the instance variable with the default values. */
Ex:
class Student3{  
int id;  
String name; 
void display(){System.out.println(id+" "+name);}  
public static void main(String args[]){  
Student3 s1=new Student3();  
Student3 s2=new Student3();  
s1.display();  
s2.display();  
}  
}  

/**
constructor implicitly returns the current instance of the class. The constructor is not inherited.
 constructor can't be final.
There are many ways to copy the values of one object into another in java. They are:
 By constructor
 By assigning the values of one object into another
 By clone() method of Object class
In this example, we are going to copy the values of one object into another using java constructor.
*/
//Java program to initialize the values from one object to another  
class Student6{  
    int id;  
    String name;  
    //constructor to initialize integer and string  
    Student6(int i,String n){  
    id = i;  
    name = n;  
    }  
    //constructor to initialize another object  
    Student6(Student6 s){  
    id = s.id;  
    name =s.name;  
    }  
    void display(){System.out.println(id+" "+name);}   
    public static void main(String args[]){  
    Student6 s1 = new Student6(111,"Karan");  
    Student6 s2 = new Student6(s1);  
    s1.display();  
    s2.display();  
   }  
}  

/**
constructor is used to initialize the state of an object. method is used to expose the behavior of an
 object
constructor must not have a return type method must have a return type
constructor is invoked implicitly method is invoked explicitly
Java compiler provides a default constructor if you don't have any constructor in a class. method is
 not provided by the compiler in any case.
constructor name must be same as the class name method name may or may not be same as class name.
*/

// Example of automatic type promotion (casting)
public class Test   
{  
    Test(int a, int b)  
    {  
        System.out.println("a = "+a+" b = "+b);  
    }  
    Test(int a, float b)  
    {  
        System.out.println("a = "+a+" b = "+b);  
    }  
    public static void main (String args[])  
    {  
        byte a = 10;   
        byte b = 15;  
        Test test = new Test(a,b);  
    }  
}  

/**
Type promotion in Java:
Byte -> Short -> Int 
Char -> Int
Int -> Long -> Float -> Double

*/

class Test   
{  
    int i;   
}  
public class Main   
{  
    public static void main (String args[])   
    {  
        Test test = new Test();   
        System.out.println(test.i);  
    }  
}  

class Test   
{  
    int test_a, test_b;  
    Test(int a, int b)   
    {  
    test_a = a;   
    test_b = b;   
    }  
    public static void main (String args[])   
    {  
        Test test = new Test();   
        System.out.println(test.test_a+" "+test.test_b);  
    }  
} 

//Static variable gets memory only once in the class area at the time of class loading. Using a
// static variable makes your program more memory
//efficient (it saves memory). Static variable belongs to the class rather than the object.
// The static method can not use non-static data member or call the non-static method directly.
// this and super cannot be used in static context as they are non-static.

//Program of static variable    
class Student8{  
   int rollno;  
   String name;  
   static String college ="ITS";       
   Student8(int r,String n){  
   rollno = r;  
   name = n;  
   }  
 void display (){System.out.println(rollno+" "+name+" "+college);}  
  
 public static void main(String args[]){  
 Student8 s1 = new Student8(111,"Karan");  
 Student8 s2 = new Student8(222,"Aryan");     
 s1.display();  
 s2.display();  
 }  
}  
for pic -> https://www.javatpoint.com/corejava-interview-questions  No.39

/**   
Why is the main method static? Because the object is not required to call the static method. If we
make the main method non-static, JVM will have to create its object first and then call main()
method which will lead to the extra memory allocation.
can't override static methods.

Static block is used to initialize the static data member. It is executed before the main method,
at the time of classloading.
As we know that the static context (method, block, or variable) belongs to the class, not the object.
Since Constructors are invoked only when the object is created, there is no sense to make the
constructors static.

In Java, if we make the abstract methods static, It will become the part of the class, and we can
directly call it which is unnecessary. Calling an undefined method is completely useless therefore
it is not allowed.
we can declare static variables and methods in an abstract class

1) this: to distinguish local variable and instance variable.
   If local variables(formal arguments) and instance variables are different, there is no need to
   use this keyword. It is better approach to use meaningful names for variables. So we use same
   name for instance variables and parameters in real time, and always use this keyword.
2) this: You may invoke the method of the current class by using the this keyword. If you don't
   use the this keyword, compiler automatically adds this keyword while invoking the method. */
	class A{  
	 void m(){System.out.println("hello m");}  
	 void n(){  
	  System.out.println("hello n");  
	 //m();//same as this.m()  
	 this.m();  
	 }  
	 }  
	class TestThis4{  
	 public static void main(String args[]){  
	 A a=new A();  
	 a.n();  
	}} 
/**	
3) this() : used for constructor chaining */
    // ex1
	class A{  
		A(){System.out.println("hello a");}  
		A(int x){  
		this();  
		System.out.println(x);  
		}  
	}  
	class TestThis5{  
		public static void main(String args[]){  
		A a=new A(10);  
	}}
	// ex2
	class A{  
		A(){  
		this(5);  
		System.out.println("hello a");  
		}  
		A(int x){  
		System.out.println(x);  
		}  
	}  
	class TestThis6{  
		public static void main(String args[]){  
		A a=new A();  
	}}  
	// ex3
	class Student{  
		int rollno;  
		String name,course;  
		float fee;  
		Student(int rollno,String name,String course){  
		this.rollno=rollno;  
		this.name=name;  
		this.course=course;  
		}  
		Student(int rollno,String name,String course,float fee){  
		this(rollno,name,course);//reusing constructor  
		this.fee=fee;  
		}  
		void display(){System.out.println(rollno+" "+name+" "+course+" "+fee);}  
	}  
	class TestThis7{  
		public static void main(String args[]){  
			Student s1=new Student(111,"ankit","java");  
			Student s2=new Student(112,"sumit","java",6000f);  
			s1.display();  
			s2.display();  
	}}  
// Rule: Call to this() must be the first statement in constructor.
/**
4) this: to pass this as an argument in the method. mainly used in the event handling. */
	class S2{  
	  void m(S2 obj){  
	  System.out.println("method is invoked");  
	  }  
	  void p(){  
	  m(this);  
	  }  
	  public static void main(String args[]){  
	  S2 s1 = new S2();  
	  s1.p();  
	  }  
	}  
/**
5) this: to pass as argument in the constructor call. It is useful if we have to use one object
   in multiple classes */
   // ex
	class B{  
	  A4 obj;  
	  B(A4 obj){  
		this.obj=obj;  
	  }  
	  void display(){  
		System.out.println(obj.data);//using data member of A4 class  
	  }  
	}  	  
	class A4{  
	  int data=10;  
	  A4(){  
	   B b=new B(this);  
	   b.display();  
	  }  
	  public static void main(String args[]){  
	   A4 a=new A4();  
	  }  
	}     
/**
6) this keyword can be used to return current class instance. We can return this keyword as an
   statement from the method. In such case, return type of the method must be the class type
   (non-primitive). Let's prove that this keyword refers to the current class instance variable: */
	class A5{  
		void m(){  
		System.out.println(this);//prints same reference ID  
		}  
		public static void main(String args[]){  
			A5 obj=new A5();  
			System.out.println(obj);//prints the reference ID  
			obj.m();  
		}  
	} 
// this cannot be assigned to any value because it always points to the current class object and
// this is the final reference in Java.
public class Test  
{  
    public Test()  
    {  
        this = null;   
        System.out.println("Test class constructor called");  
    }  
    public static void main (String args[])  
    {  
        Test t = new Test();  
    }  
}  
// It is possible to use this keyword to refer static members because this is just a reference variable
// which refers to the current class object. However, as we know that, it is unnecessary to access
// static variables through objects, therefore, it is not the best practice to use this to refer
// static members.
public class Test   
{  
    static int i = 10;   
    public Test ()  
    {  
        System.out.println(this.i);      
    }  
    public static void main (String args[])  
    {  
        Test t = new Test();  
    }  
}  
// Constructor chaining enables us to call one constructor from another constructor of the class with
// respect to the current class object. We can use this keyword to perform constructor chaining within
// the same class.
public class Employee  
{  
    int id,age;   
    String name, address;  
    public Employee (int age)  
    {  
        this.age = age;  
    }  
    public Employee(int id, int age)  
    {  
        this(age);  
        this.id = id;  
    }  
    public Employee(int id, int age, String name, String address)  
    {  
        this(id, age);  
        this.name = name;   
        this.address = address;   
    }  
    public static void main (String args[])  
    {  
        Employee emp = new Employee(105, 22, "Vikas", "Delhi");  
        System.out.println("ID: "+emp.id+" Name:"+emp.name+" age:"+emp.age+" address: "+emp.address);  
    }  
      
} 
/** 
As we know, that this refers to the current class object, therefore, it must be similar to the
current class object. However, there can be two main advantages of passing this into a method
instead of the current class object. this is a final variable. Therefore, this cannot be
assigned to any new value whereas the current class object might not be final and can be changed.
this can be used in the synchronized block.

Inheritance provides code reusability. The derived class does not need to redefine the method
of base class unless it needs to provide the specific implementation of the method.
Runtime polymorphism cannot be achieved without using inheritance. We can simulate the inheritance
of classes with the real-time objects which makes OOPs more realistic. Inheritance provides data
hiding. The base class can hide some data from the derived class by making it private. Method
overriding cannot be achieved without inheritance. By method overriding, we can give a specific
implementation of some basic method contained by the base class. */

Aggregation can be defined as the relationship between two classes where the aggregate class
contains a reference to the class it owns. Aggregation is best described as a has-a relationship.

public class Address {  
	.
	.
	.	  
}  
public class Emp {  
	int id;  
	String name;  
	Address address; 
	.
    .
	.
}  

Holding the reference of a class within some other class is known as composition.
When an object contains the other object, if the contained object cannot exist without
the existence of container object, then it is called composition. In other words,
we can say that composition is the particular case of aggregation which represents a
stronger relationship between two objects. Example: A class contains students. A student
cannot exist without a class. There exists composition between class and students.
Aggregation represents the weak relationship whereas composition represents the
strong relationship.

The pointer is a variable that refers to the memory address. They are not used in Java
because they are unsafe(unsecured) and complex to understand.

The super keyword in Java is a reference variable that is used to refer to the
immediate parent class object. Whenever you create the instance of the subclass,
an instance of the parent class is created implicitly which is referred by super
reference variable. The super() is called in the class constructor implicitly by
the compiler if there is no super or this. super can be used to refer to the
immediate parent class instance variable. super can be used to invoke the
immediate parent class method. super() can be used to invoke immediate parent class
constructor. The super keyword is primarily used for initializing the base class variables
within the derived class constructor whereas this keyword primarily used to differentiate between
local and instance variables when passed in the class constructor.
The super and this must be the first statement inside constructor

constructor chaining be done by using super:
class Person  
{  
    String name,address;  
    int age;  
    public Person(int age, String name, String address)  
    {  
        this.age = age;  
        this.name = name;  
        this.address = address;  
    }  
}  
class Employee extends Person  
{  
    float salary;  
    public Employee(int age, String name, String address, float salary)  
    {  
        super(age,name,address);  
        this.salary = salary;  
    }  
}  
public class Test  
{  
    public static void main (String args[])  
    {  
        Employee e = new Employee(22, "Mukesh", "Delhi", 90000);  
        System.out.println("Name: "+e.name+" Salary: "+e.salary+" Age: "+e.age+" Address: "+e.address);  
    }  
}  

The super() is implicitly invoked by the compiler if no super() or this() is included explicitly
within the derived class constructor. Therefore, below, The Person class constructor is called
first and then the Employee class constructor is called.
ex:
class Person  
{  
    public Person()  
    {  
        System.out.println("Person class constructor called");  
    }  
}  
public class Employee extends Person  
{  
    public Employee()  
    {  
        System.out.println("Employee class constructor called");  
    }  
    public static void main (String args[])  
    {  
        Employee e = new Employee();  
    }  
}

Can't you use this() and super() both in a constructor

The object cloning is used to create the exact copy of an object. The clone() method of the Object
class is used to clone an object. The java.lang.Cloneable interface must be implemented by the class
whose object clone we want to create.
Syntax of the clone() method is as follows:
protected Object clone() throws CloneNotSupportedException
The clone() method saves the extra processing task for creating the exact copy of an object. If we
perform it by using the new keyword, it will take a lot of processing time to be performed that is
why we use object cloning.
Advantage of Object cloning
Although Object.clone() has some design issues but it is still a popular and easy way of copying objects.
Following is a list of advantages of using clone() method:
  You don't need to write lengthy and repetitive codes. Just use an abstract class with a 4- or 5-line
  long clone() method.
  It is the easiest and most efficient way for copying objects, especially if we are applying it to an
  already developed or an old project. Just define a parent class, implement Cloneable in it, provide
  the definition of the clone() method and the task will be done.
  Clone() is the fastest way to copy array.
Disadvantage of Object cloning
  To use the Object.clone() method, we have to change a lot of syntaxes to our code, like implementing
  a Cloneable interface, defining the clone() method and handling CloneNotSupportedException, and finally,
  calling Object.clone() etc.
  We have to implement cloneable interface while it doesn't have any methods in it. We just have to use it
  to tell the JVM that we can perform clone() on our object.
  Object.clone() is protected, so we have to provide our own clone() and indirectly call Object.clone()
  from it.
  Object.clone() doesn't invoke any constructor so we don't have any control over object construction.
  If you want to write a clone method in a child class then all of its superclasses should define the
  clone() method in them or inherit it from another parent class. Otherwise, the super.clone() chain
  will fail. Object.clone() supports only shallow copying but we will need to override it if we need deep
  cloning.
 ex: 
class Student18 implements Cloneable{  
	int rollno;  
	String name;  
	 
	Student18(int rollno,String name){  
		this.rollno=rollno;  
	this.name=name;  
}  
 
public Object clone()throws CloneNotSupportedException{  
	return super.clone();  
}  
public static void main(String args[]){  
	try{  
		Student18 s1=new Student18(101,"amit");  
		 
		Student18 s2=(Student18)s1.clone();  
		 
		System.out.println(s1.rollno+" "+s1.name);  
		System.out.println(s2.rollno+" "+s2.name);  
	 
	}catch(CloneNotSupportedException c){}  
	 
	}  
}

Method overloading is the polymorphism technique which allows us to create multiple methods with the
same name but different signature. We can achieve method overloading in two ways.
	By Changing the number of arguments
	By Changing the data type of arguments
Method overloading increases the readability of the program. Method overloading is performed to figure
out the program quickly.

Type promotion is method overloading, we mean that one data type can be promoted to another implicitly
if no exact matching is found.
ex:
class OverloadingCalculation1{  
  void sum(int a,long b){System.out.println(a+b);}  
  void sum(int a,int b,int c){System.out.println(a+b+c);}  
 
  public static void main(String args[]){  
  OverloadingCalculation1 obj=new OverloadingCalculation1();  
  obj.sum(20,20);//now second int literal will be promoted to long  
  obj.sum(20,20,20);  
  }  
}  
ex:
class OverloadingCalculation3{    
  void sum(int a,long b){System.out.println("a method invoked");}    
  void sum(long a,int b){System.out.println("b method invoked");}    
   
  public static void main(String args[]){    
  OverloadingCalculation3 obj=new OverloadingCalculation3();    
  obj.sum(20,20);//now ambiguity    
  }    
}
ex:
class Base  
{  
    void method(int a)  
    {  
        System.out.println("Base class method called with integer a = "+a);  
    }  
       
    void method(double d)  
    {  
        System.out.println("Base class method called with double d ="+d);  
    }  
}    
class Derived extends Base  
{  
    @Override  
    void method(double d)  
    {  
        System.out.println("Derived class method called with double d ="+d);  
    }  
}    
public class Main  
{      
    public static void main(String[] args)  
    {  
        new Derived().method(10);  
    }  
} 

you can't override a static method because they are the part of the class, not the object.
we override any overloaded method. Override <--> IS-A (super/sub relationship)
can change the scope of the overridden method in the subclass.However, we must notice that we cannot
decrease the accessibility of the method. The private can be changed to protected, public, or default.
The protected can be changed to public or default. The default can be changed to public.
The public will always remain public.        <-- check these
we can modify the throws clause of the superclass method while overriding it in the subclass. However,
there are some rules which are to be followed:
Problem 1:  If The SuperClass doesn’t declare an exception:
	Case 1: If SuperClass doesn’t declare any exception and subclass declare checked exception -> error
	Case 2: If SuperClass doesn’t declare any exception and SubClass declare Unchecked exception
Problem 2: If The SuperClass declares an exception:
	Case 1: If SuperClass declares an exception and SubClass declares exceptions other than the child
	exception of the SuperClass declared Exception. -> error
	Case 2: If SuperClass declares an exception and SubClass declares a child exception of the SuperClass
	declared Exception.
	Case 3: If SuperClass declares an exception and SubClass declares without exception.
In brief:
If SuperClass does not declare an exception, then the SubClass can only declare unchecked exceptions,
but not the checked exceptions.
If SuperClass declares an exception, then the SubClass can only declare the same or child exceptions
of the exception declared by the SuperClass and any new Runtime Exceptions, just not any new checked
exceptions at the same level or higher.
If SuperClass declares an exception, then the SubClass can declare without exception.

it is possible to override any method by changing the return type if the return type
of the subclass overriding method is subclass type. It is known as covariant return type.
The covariant return type specifies that the return type may vary in the same direction as the subclass.

class A{  
	A get(){return this;}  
}   
class B1 extends A{  
	B1 get(){return this;}  
    void message(){System.out.println("welcome to covariant return type");}  
public static void main(String args[]){  
	new B1().get().message();  
	}  
}  
/**
Covariance can be considered as a contract for how a subtype is accepted when only the supertype
is defined. means, we can access specific elements defined via their supertype. However, we aren't
allowed to put elements into a covariant system, since the compiler would fail to determine the
actual type of the generic structure.The covariant return type is – when we override a method – what
allows the return type to be the subtype of the type of the overridden method.
ex:*/
public class Producer {
    public Object produce(String input) {
        Object result = input.toLowerCase();
        return result;
    }
}
public class IntegerProducer extends Producer {
    @Override
    public Integer produce(String input) {
        return Integer.parseInt(input);
    }
}
//As a result of the Object as a return type, we can have a more concrete return type in the child class.
//That will be the covariant return type and will produce numbers from character sequences:

class Base   
{  
    public void baseMethod()  
    {  
        System.out.println("BaseMethod called ...");  
    }  
}  
class Derived extends Base   
{  
    public void baseMethod()  
    {  
        System.out.println("Derived method called ...");  
    }  
}  
public class Test   
{  
    public static void main (String args[])  
    {  
        Base b = new Derived();  
        b.baseMethod();  
    }  
}  
/**
The method of Base class, i.e., baseMethod() is overridden in Derived class. In Test class,
the reference variable b (of type Base class) refers to the instance of the Derived class.
Here, Runtime polymorphism is achieved between class Base and Derived. At compile time,
the presence of method baseMethod checked in Base class, If it presence then the program
compiled otherwise the compiler error will be shown. In this case, baseMethod is present
in Base class; therefore, it is compiled successfully. However, at runtime, It checks whether
the baseMethod has been overridden by Derived class, if so then the Derived class method is
called otherwise Base class method is called. In this case, the Derived class overrides the
baseMethod; therefore, the Derived class method is called.

the final variable once assigned to a value, can never be changed after that.
The final variable which is not assigned to any value can only be assigned through the class constructor.
final method is inherited but you cannot override it. If we make any class final, we can't inherit it
into any of the subclasses. The constructor can never be declared as final because it is never inherited.
we cannot declare an interface as final because the interface must be implemented. */ 
class Bike10{  
  final int speedlimit;//blank final variable      
  Bike10(){  
  speedlimit=70;  
  System.out.println(speedlimit);  
  }    
  public static void main(String args[]){  
    new Bike10();  
 }  
}
ex:
class Main {  
 public static void main(String args[]){  
   final int i;  
   i = 20;  
   System.out.println(i);  
 }  
}  
// Since i is the blank final variable. It can be initialized only once. We have initialized it to 20.
// Therefore, 20 will be printed.

compile-time polymorphism and runtime polymorphism:
1	In compile-time polymorphism, call to a method is resolved at compile-time.
	In runtime polymorphism, call to an overridden method is resolved at runtime.
2	compile-time polymorphism is also known as static binding, early binding, or overloading.
	runtime polymorphism is also known as dynamic binding, late binding, overriding,
	or dynamic method dispatch.
3	Overloading is a way to achieve compile-time polymorphism in which,
    we can define multiple methods or constructors with different signatures.
	Overriding is a way to achieve runtime polymorphism in which, we can redefine
	some particular method or variable in the derived class. By using overriding,
	we can give some specific implementation to the base class properties in the derived class.
4	compile-time polymorphism provides fast execution because the type of an object
    is determined at compile-time.runtime polymorphism provides slower execution as
	compare to compile-time because the type of an object is determined at run-time.
5	Compile-time polymorphism provides less flexibility because all the things are resolved
    at compile-time. Run-time polymorphism provides more flexibility because all the
	things are resolved at runtime.
Runtime polymorphism or dynamic method dispatch is a process in which a call to an overridden
method is resolved at runtime rather than at compile-time. In this process, an overridden
method is called through the reference variable of a superclass. The determination of the
method to be called is based on the object being referred to by the reference variable.
class Bike{  
  void run(){System.out.println("running");}  
}  
class Splendor extends Bike{  
  void run(){System.out.println("running safely with 60km");}  
  public static void main(String args[]){  
    Bike b = new Splendor();//upcasting  
    b.run();  
  }  
}  
Cann't achieve Runtime Polymorphism by data members. because method overriding is used to
achieve runtime polymorphism and data members cannot be overridden. We can override the
member functions but not the data members.
class Bike{  
 int speedlimit=90;  
}  
class Honda3 extends Bike{  
 int speedlimit=150;  
public static void main(String args[]){  
  Bike obj=new Honda3();  
  System.out.println(obj.speedlimit);
}  

//In case of the static binding, the type of the object is determined at compile-time whereas,
//in the dynamic binding, the type of the object is determined at runtime. If there is any private,
// final or static method in a class, there is static binding.
//Static Binding
class Dog{  
 private void eat(){System.out.println("dog is eating...");}  
  
 public static void main(String args[]){  
  Dog d1=new Dog(); //Here d1 is an instance of Dog class, but it is also an instance of Animal. 
  d1.eat();  
 }  
}  
//Dynamic Binding
class Animal{  
 void eat(){System.out.println("animal is eating...");}  
}  
  
class Dog extends Animal{  
 void eat(){System.out.println("dog is eating...");}  
  
 public static void main(String args[]){  
  Animal a=new Dog(); //object type cannot be determined by the compiler, because the instance
                      //of Dog is also an instance of Animal.So compiler doesn't know its type,
					  //only its base type.  
  a.eat();  
 }  
}  
ex:
class BaseTest   
{  
  void print()  
  {  
    System.out.println("BaseTest:print() called");  
  }  
}  
public class Test extends BaseTest   
{  
  void print()   
  {  
    System.out.println("Test:print() called");  
  }  
  public static void main (String args[])  
  {  
    BaseTest b = new Test();  
    b.print();  
  }  
}  
//type of reference variable b is determined at runtime. At compile-time, it is checked whether
//that method is present in the Base class. In this case, it is overridden in the child class,
//therefore, at runtime the derived class method is called.

/**
instanceof: compares the instance with type.
Simple1 s=new Simple1();  
System.out.println(s instanceof Simple1);//true

Abstraction enables you to focus on what the object does instead of how it does it.
encapsulation wraps code and data into a single unit.
An abstract class must be declared with an abstract keyword.
It can have abstract and non-abstract methods.
It cannot be instantiated.
It can have constructors and static methods also.
It can have final methods which will force the subclass not to change the body of the method.
An abstract class can have a data member, abstract method, method body (non-abstract method),
constructor, and even main() method.
abstract class can never be instantiated even if it contains a constructor and all of its methods
are implemented. methods of an interface are abstract by default, and we can not use static
and abstract together. A Marker interface can be defined as the interface which has no data
member and member functions. For example, Serializable, Cloneable. The abstract class can
provide the implementation of the interface. The Interface can't provide the implementation
of the abstract class. An abstract class can extend another Java class and implement multiple
Java interfaces. An interface can extend another Java interface only. Members of a Java interface
are public by default. An object reference can be cast to an interface reference when the object
implements the referenced interface.*/
 abstract class Bike{  
   Bike(){System.out.println("bike is created");}  
   abstract void run();  
   void changeGear(){System.out.println("gear changed");}  
 }  
 class Honda extends Bike{  
 void run(){System.out.println("running safely..");}  
 }  
 class TestAbstraction2{  
 public static void main(String args[]){  
  Bike obj = new Honda();  
  obj.run();  
  obj.changeGear();  
 }  
} 
ex:
interface A{  
	void a();  
	void b();  
	void c();  
	void d();  
}    
abstract class B implements A{  
	public void c(){System.out.println("I am c");}  
}   
class M extends B{  
	public void a(){System.out.println("I am a");}  
	public void b(){System.out.println("I am b");}  
	public void d(){System.out.println("I am d");}  
}    
class Test5{  
public static void main(String args[]){  
	A a=new M();  
	a.a();  
	a.b();  
	a.c();  
	a.d();  
}}  
ex:
abstract class Calculate  
{  
    abstract int multiply(int a, int b);  
}     
public class Main  
{  
    public static void main(String[] args)  
    {  
        int result = new Calculate()  
        {      
            @Override  
            int multiply(int a, int b)  
            {  
                return a*b;  
            }  
        }.multiply(12,32);  
        System.out.println("result = "+result);  
    }  
}  

Encapsulation:
A class can be made read-only by making all of the fields private. The read-only class will have
only getter methods which return the private property of the class to the main method. 
A class can be made write-only by making all of the fields private. The write-only class will have
only setter methods which set the value passed from the main method to the private fields.
It provides you the control over the data. Suppose you want to set the value of id which should
be greater than 100 only, you can write the logic inside the setter method. You can write the
logic not to store the negative numbers in the setter methods.
It is a way to achieve data hiding in Java because other class will not be able to access the
data through the private data members.
The encapsulate class is easy to test. So, it is better for unit testing.

A package is a group of similar type of classes, interfaces, and sub-packages. It provides
access protection and removes naming collision. One can import the same package or the same
class multiple times. Neither compiler nor JVM complains about it. However, the JVM will
internally load the class only once

It is not necessary that each try block must be followed by a catch block. It should be followed
by either a catch block OR a finally block. 
Checked Exception: Checked exceptions are the one which are checked at compile-time. For example,
 SQLException, ClassNotFoundException, etc.
Unchecked Exception: Unchecked exceptions are the one which are handled at runtime because they
 can not be checked at compile-time. For example, ArithmaticException, NullPointerException,
 ArrayIndexOutOfBoundsException, etc.
Error: Error cause the program to exit since they are not recoverable. For Example,
 OutOfMemoryError, AssertionError, etc.
The core advantage of exception handling is to maintain the normal flow of the application.
An exception normally disrupts the normal flow of the application; that is why we need to
handle exceptions. The "throw" keyword is used to throw an exception. The "throws" keyword
is used to declare exceptions. It specifies that there may occur an exception in the method.
It doesn't throw an exception. It is always used with method signature.
Hierarchy of Java Exception classes:
	Throwable -> Exception, Error
	Exception -> IOException, SQLException, ClassNotFoundException, RuntimeException
	RuntimeException -> ArithmeticException, NullPointerException, NumberFormatException,
						IndexOutOfBoundsException
	IndexOutOfBoundsException -> ArrayIndexOutOfBoundsException, StringIndexOutOfBoundsException
	Error -> StackOverflowError, VirtualMachineError, OutOfMemoryError					
Common Scenarios of Java Exceptions:
	If we divide any number by zero, there occurs an ArithmeticException.
	If we have a null value in any variable, performing any operation on the variable throws a
	 NullPointerException.
	If the formatting of any variable or number is mismatched, it may result into
	 NumberFormatException. Suppose we have a string variable that has characters;
	 converting this variable into digit will cause NumberFormatException.
	When an array exceeds to it's size, the ArrayIndexOutOfBoundsException occurs.
	 there may be other reasons to occur ArrayIndexOutOfBoundsException.
Exception Propagation:
	An exception is first thrown from the top of the stack and if it is not caught, it drops down
	the call stack to the previous method. If not caught there, the exception again drops down
	to the previous method, and so on until they are caught or until they reach the very bottom
	of the call stack. 
By default Unchecked Exceptions are forwarded in calling chain (propagated).
class TestExceptionPropagation1{  
  void m(){  
    int data=50/0;  
  }  
  void n(){  
    m();  
  }  
  void p(){  
   try{  
    n();  
   }catch(Exception e){System.out.println("exception handled");}  
  }  
  public static void main(String args[]){  
   TestExceptionPropagation1 obj=new TestExceptionPropagation1();  
   obj.p();  
   System.out.println("normal flow...");  
  }  
}  
By default, Checked Exceptions are not forwarded in calling chain (propagated).
class TestExceptionPropagation2{  
  void m(){  
    throw new java.io.IOException("device error");//checked exception  
  }  
  void n(){  
    m();  
  }  
  void p(){  
   try{  
    n();  
   }catch(Exception e){System.out.println("exception handeled");}  
  }  
  public static void main(String args[]){  
   TestExceptionPropagation2 obj=new TestExceptionPropagation2();  
   obj.p();  
   System.out.println("normal flow");  
  }  
} 
Nested try block: Sometimes a situation may arise where a part of a block may cause one
error and the entire block itself may cause another error. In such cases, exception
handlers have to be nested. For example, the inner try block can be used to handle
ArrayIndexOutOfBoundsException while the outer try block can handle the ArithemeticException
(division by zero).
final is an access modifier, finally is the block in Exception Handling and finalize (deprecated) is the
method of object class. Finally block is executed as soon as the try-catch block is executed.
finalize method is executed just before the object is destroyed.
finalize method performs the cleaning activities with respect to the object before its destruction.
custom exceptions: To catch and provide specific treatment to a subset of existing Java exceptions.
Business logic exceptions: These are the exceptions related to business logic and workflow.
It is useful for the application users or the developers to understand the exact problem.
In order to create custom exception, we need to extend Exception class that belongs to 
java.lang package.
Finally block will not be executed if program exits(either by calling System.exit() or by causing
a fatal error that causes the process to abort) 
ex:
public class WrongFileNameException extends Exception {  
    public WrongFileNameException(String errorMessage) {  
    super(errorMessage);  
    }  
}  
ex:
class InvalidAgeException  extends Exception  
{  
    public InvalidAgeException (String str)  
    {  
        super(str);  
    }  
}    
public class TestCustomException1  
{  
    static void validate (int age) throws InvalidAgeException{    
       if(age < 18){  
        throw new InvalidAgeException("age is not valid to vote");    
    }  
       else {   
        System.out.println("welcome to vote");   
        }  
     }  
    public static void main(String args[])  
    {  
        try  
        {  
            validate(13);  
        }  
        catch (InvalidAgeException ex)  
        {  
            System.out.println("Caught the exception");    
            System.out.println("Exception occured: " + ex);  
        }    
        System.out.println("rest of the code...");    
    }  
}  
ex:
class MyCustomException extends Exception  
{  
    
}      
public class TestCustomException2  
{  
    public static void main(String args[])  
    {  
        try  
        {  
            throw new MyCustomException();  
        }  
        catch (MyCustomException ex)  
        {  
            System.out.println("Caught the exception");  
            System.out.println(ex.getMessage());  
        }  
        System.out.println("rest of the code...");    
    }  
}  
Exception Handling with Method Overriding in Java:
If the superclass method does not declare an exception, subclass overridden method cannot
declare the checked exception but it can declare unchecked exception.
If the superclass method does not declare an exception, subclass overridden method cannot
declare the checked exception but can declare unchecked exception.
If the superclass method declares an exception, subclass overridden method can declare
the same exception or no exception but cannot declare exception which is the superclass of parent
class exception.
ex:
class Parent{    
  void msg()throws ArithmeticException {  
    System.out.println("parent method");  
  }    
}    
    
public class TestExceptionChild2 extends Parent{    
  void msg()throws Exception {  
    System.out.println("child method");  
  }    
    
  public static void main(String args[]) {    
   Parent p = new TestExceptionChild2();    
     
   try {    
   p.msg();    
   }  
   catch (Exception e){}   
  
  }    
}    
ex:
class Parent{    
  void msg() throws Exception {  
    System.out.println("parent method");  
  }    
}    
    
public class TestExceptionChild3 extends Parent {    
  void msg()throws Exception {  
    System.out.println("child method");  
  }    
    
  public static void main(String args[]){    
   Parent p = new TestExceptionChild3();    
     
   try {    
   p.msg();    
   }  
   catch(Exception e) {}    
  }    
}    
ex:
class Parent{    
  void msg()throws Exception {  
    System.out.println("parent method");  
  }    
}    
    
class TestExceptionChild4 extends Parent{    
  void msg()throws ArithmeticException {  
    System.out.println("child method");  
  }    
    
  public static void main(String args[]){    
   Parent p = new TestExceptionChild4();    
     
   try {    
   p.msg();    
   }  
   catch(Exception e) {}    
  }    
}
ArithmaticException is the subclass of Exception. Therefore, it can not be used after Exception.
ex:
public class ExceptionHandlingExample {  
	public static void main(String args[])  
	{  
		try  
		{  
			int a = 1/0;  
			System.out.println("a = "+a);  
		}  
		catch(Exception e){System.out.println(e);}  
		catch(ArithmeticException ex){System.out.println(ex);}    
	}  
}  
the throwable objects can only be thrown. If we try to throw an integer object, The compiler
will show an error since we can not throw basic data type from a block of code.
public class Main{  
    public static void main(String []args){  
        try  
        {  
            throw 90;   
        }  
        catch(int e){  
            System.out.println("Caught the exception "+e);  
        }                
    }  
} 
ex: // چه جالب
class Calculation extends Exception  
{  
    public Calculation()   
    {  
        System.out.println("Calculation class is instantiated");  
    }  
    public void add(int a, int b)  
    {  
        System.out.println("The sum is "+(a+b));  
    }  
}  
public class Main{  
     public static void main(String []args){  
        try  
        {  
            throw new Calculation();   
        }  
        catch(Calculation c){  
            c.add(10,20);  
        }  
    }  
} 
The object of Calculation is thrown from the try block which is caught in the catch block.
The add() of Calculation class is called with the integer values 10 and 20 by using the
object of this class. Therefore there sum 30 is printed. The object of the Main class 
can only be thrown when the type of the object is throwable. To do so, we 
need to extend the throwable class. exception can be rethrown

ex: propagation
public class Main   
{  
    void a()  
    {  
        try{  
        System.out.println("a(): Main called");  
        b();  
        }catch(Exception e)  
        {  
            System.out.println("Exception is caught");  
        }  
    }  
    void b() throws Exception  
    {  
     try{  
         System.out.println("b(): Main called");  
         c();  
     }catch(Exception e){  
         throw new Exception();  
     }  
     finally   
     {  
         System.out.println("finally block is called");  
     }  
    }  
    void c() throws Exception   
    {  
        throw new Exception();  
    }  
  
    public static void main (String args[])  
    {  
        Main m = new Main();  
        m.a();  
    }  
}  
In the main method, a() of Main is called which prints a message and call b(). The method b()
prints some message and then call c(). The method c() throws an exception which is handled by
the catch block of method b. However, It propagates this exception by using throw Exception()
to be handled by the method a(). As we know, finally block is always executed therefore the
finally block in the method b() is executed first and prints a message. At last, the exception
is handled by the catch block of the method a().
ex:
public class Calculation   
{  
    int a;   
    public Calculation(int a)  
    {  
        this.a = a;  
    }  
    public int add()  
    {  
        a = a+10;   
        try   
        {  
            a = a+10;   
            try   
            {  
                a = a*10;   
                throw new Exception();   
            }catch(Exception e){  
                a = a - 10;  
            }  
        }catch(Exception e)  
        {  
            a = a - 10;   
        }  
        return a;  
    }        
    public static void main (String args[])  
    {  
        Calculation c = new Calculation(10);  
        int result = c.add();  
        System.out.println("result = "+result);  
    }  
}  
The instance variable a of class Calculation is initialized to 10 using the class constructor
which is called while instantiating the class. The add method is called which returns an integer
value result. In add() method, a is incremented by 10 to be 20. Then, in the first try block, 10
is again incremented by 10 to be 30. In the second try block, a is multiplied by 10 to be 300.
The second try block throws the exception which is caught by the catch block associated with this
try block. The catch block again alters the value of a by decrementing it by 10 to make it 290.
Thus the add() method returns 290 which is assigned to result. However, the catch block associated
with the outermost try block will never be executed since there is no exception which can be
handled by this catch block.

String pool is the space reserved in the heap memory that can be used to store the strings.
The main advantage of using the String pool is whenever we create a string literal; the JVM
checks the "string constant pool" first. If the string already exists in the pool, a reference
to the pooled instance is returned. If the string doesn't exist in the pool, a new string
instance is created and placed in the pool. The simple meaning of immutable is unmodifiable
or unchangeable. In Java, String is immutable, i.e., once string object has been created,
its value can't be changed.
class Testimmutablestring{  
 public static void main(String args[]){  
   String s="Sachin";  
   s.concat(" Tendulkar"); 
   System.out.println(s); 
 }  
} 

ways can we create the string object:
1) String Literal
	Java String literal is created by using double quotes. For Example:
	String s ="welcome";  
    String s2="Welcome";//It doesn't create a new instance
2) By new keyword
	String s=new String("Welcome");//creates two objects and one reference variable
	In such case, JVM will create a new string object in normal (non-pool) heap memory,
	and the literal "Welcome" will be placed in the constant string pool. The variable s
	will refer to the object in a heap (non-pool).
public class Test   
{
  public static void main (String args[])  
  {  
      String a = new String("Sharma is a good player");  
      String b = "Sharma is a good player";  
      if(a == b)  
      {  
          System.out.println("a == b");  
      }  
      if(a.equals(b))  
      {  
          System.out.println("a equals b");  
	  }	  
  }  
}
The operator == also check whether the references of the two string objects are equal or not.
Although both of the strings contain the same content, their references are not equal because
both are created by different ways(Constructor and String literal) therefore, a == b is unequal.
On the other hand, the equal() method always check for the content. Since their content is
equal hence, a equals b is printed.
public class Test   
{  
    public static void main (String args[])  
    {  
        String s1 = "Sharma is a good player";  
        String s2 = new String("Sharma is a good player");  
        s2 = s2.intern();  
        System.out.println(s1 ==s2);  
    }  
}  
The intern method returns the String object reference from the string pool. In this case,
s1 is created by using string literal whereas, s2 is created by using the String pool. However,
s2 is changed to the reference of s1, and the operator == returns true.

differences between the String and StringBuffer:
1)	The String class is immutable.	The StringBuffer class is mutable.
2)	The String is slow and consumes more memory when you concat too many strings because every
    time it creates a new instance.	The StringBuffer is fast and consumes less memory when you
	cancat strings.
3)	The String class overrides the equals() method of Object class. So you can compare the
    contents of two strings by equals() method.	The StringBuffer class doesn't override
	the equals() method of Object class.

differences between the StringBuffer and StringBuilder:
1)	StringBuffer is synchronized, i.e., thread safe. It means two threads can't call the methods
    of StringBuffer simultaneously.	StringBuilder is non-synchronized,i.e., not thread safe.
	It means two threads can call the methods of StringBuilder simultaneously.
2)	StringBuffer is less efficient than StringBuilder.	StringBuilder is more efficient than
    StringBuffer.

create an immutable class by defining a final class having all of its members as final.

purpose of toString() method:
returns the string representation of an object. If you print any object, java compiler internally
invokes the toString() method on the object. So overriding the toString() method, returns the
desired output, it can be the state of an object, etc. depending upon your implementation.
By overriding the toString() method of the Object class, we can return the values of the
object, so we don't need to write much code.

CharArray() is preferred over String to store the password. String stays in the string pool until
the garbage is collected. If we store the password into a string, it stays in the memory for a
longer period, and anyone having the memory-dump can extract the password as clear text. On the
other hand, Using CharArray allows us to set it to blank whenever we are done with the password.
It avoids the security threat with the string by enabling us to control the memory.

classes and interfaces present in java.util.regex: 
	MatchResult Interface
	Matcher class
	Pattern class
	PatternSyntaxException class

Metacharacters have the special meaning to the regular expression engine. The metacharacters
are ^, $, ., *, +, etc. The regular expression engine does not consider them as the regular
characters. To enable the regular expression engine treating the metacharacters as ordinary
characters, we need to escape the metacharacters with the backslash.

A password must start with an alphabet and followed by alphanumeric characters; Its length must be
in between 8 to 20. regular expression to validate a password:
	^[a-zA-Z][a-zA-Z0-9]{8,19}
	where ^ represents the start of the regex, [a-zA-Z] represents that the
	first character must be an alphabet, [a-zA-Z0-9] represents the alphanumeric character, {8,19} 
	represents that the length of the password must be in between 8 and 20.

There are two types of advantages of Java inner classes.

Nested classes represent a special type of relationship that is it can access all the members
data members and methods) of the outer class including private. Nested classes are used to develop
a more readable and maintainable code because it logically
groups classes and interfaces in one place only. A nested class can access all the data members of
the outer class including private data members and methods. 
There are two types of nested classes, static nested class, and non-static nested class.
The non-static nested class can also be called as inner-class

main disadvantages of using inner classes:
Inner classes increase the total number of classes used by the developer and therefore increases the
workload of JVM since it has to perform some routine operations for those extra classes which result
in slower performance.
IDEs provide less support to the inner classes as compare to the top level classes and therefore it
annoys the developers while working with inner classes.

three types of inner classes used in Java:
	Member Inner Class:	A class created within class and outside method.
	Anonymous Inner Class:	A class created for implementing an interface or extending class. Its name
		is decided by the java compiler.
	Local Inner Class:	A class created within the method.
		the local variable must be constant if you want to access it in the local inner class.

How many class files are created on compiling the OuterClass in the following program:
public class Person {  
	String name, age, address;  
	class Employee{  
	  float salary=10000;  
	}  
	class BusinessMen{  
	  final String gstin="£4433drt3$";   
	}  
	public static void main (String args[])  
	{  
	  Person p = new Person();  
	}  
} 

an interface can be defined within the class. It is called a nested interface.
The nested interface must be public if it is declared inside the interface, but it can have any
access modifier if declared within the class.
Nested interfaces are declared static
interface Showable{  
  void show();  
  interface Message{  
   void msg();  
  }  
}  
class TestNestedInterface1 implements Showable.Message{  
 public void msg(){System.out.println("Hello nested interface");}  
  
 public static void main(String args[]){  
  Showable.Message message=new TestNestedInterface1();//upcasting here  
  message.msg();  
 }  
}  
we are accessing the Message interface by its outer interface Showable because it cannot be accessed directly. 
The java compiler internally creates a public and static interface as displayed below:

public static interface Showable$Message  
{  
  public abstract void msg();  
}  
class A{  
  interface Message{  
   void msg();  
  }  
}    
class TestNestedInterface2 implements A.Message{  
 public void msg(){System.out.println("Hello nested interface");}  
  
 public static void main(String args[]){  
  A.Message message=new TestNestedInterface2();//upcasting here  
  message.msg();  
 }  
}  
if we define a class inside the interface, the Java compiler creates a static nested class:
interface M{  
  class A{}  
} 

Garbage Collection:
the process of removing unused objects from the memory to free up space and make this space
available for Java Virtual Machine. Due to garbage collection java gives 0 as output to a
variable whose value is not set, i.e., the variable has been defined but not initialized.
The gc() method is used to invoke the garbage collector for cleanup processing. This method
is found in System and Runtime classes. This function explicitly makes the Java Virtual Machine
free up the space occupied by the unused objects so that it can be utilized or reused. However,
it depends upon the JVM whether to perform it or not.
public class TestGarbage1{  
 public void finalize(){System.out.println("object is garbage collected");}  
 public static void main(String args[]){  
  TestGarbage1 s1=new TestGarbage1();  
  TestGarbage1 s2=new TestGarbage1();  
  s1=null;  
  s2=null;  
  System.gc();  
 }  
}  

an object can be unreferenced by:
	By nulling the reference
		Employee e=new Employee();  
		e=null; 
	By assigning a reference to another
		Employee e1=new Employee();  
		Employee e2=new Employee();  
		e1=e2;//now the first object referred by e1 is available for garbage collection
	By anonymous object
		new Employee(); 

an unreferenced object can be referenced again

Garbage collector is Daemon thread.

Java Runtime class is used to interact with a java runtime environment. Java Runtime class
provides methods to execute a process, invoke GC, get total and free memory, etc. There is
only one instance of java.lang.Runtime class is available for one java application.
The Runtime.getRuntime() method returns the singleton instance of Runtime class.

invoke any external process in Java By Runtime.getRuntime().exec(?):
public class Runtime1{  
 public static void main(String args[])throws Exception{  
  Runtime.getRuntime().exec("notepad");//will open a new notepad  
 }  
}  

hierarchy of InputStream and OutputStream classes:
OutputStream -> FileOutputStream, ByteArrayOutputStream, FilterOutputStream, PipedOutputStream
                ObjectOutputStream
FilterOutputStream -> DataOutputStream, BufferedOutputStream, PrintStream
InputStream -> FileInputStream, ByteArrayInputStream, FilterInputStream, PipedInputStream
               ObjectInputStream
FilterInputStream -> DataInputStream, BufferedInputStream, PushBackInputStream

The stream is a sequence of data that flows from source to destination. It is composed of bytes.
In Java, three streams are created for us automatically:
System.out: standard output stream
System.in: standard input stream
System.err: standard error stream

difference between the Reader/Writer class hierarchy and the InputStream/OutputStream class hierarchy:
The Reader/Writer class hierarchy is character-oriented, and the InputStream/OutputStream class
hierarchy is byte-oriented. The ByteStream classes are used to perform input-output of 8-bit 
bytes whereas the CharacterStream classes are used to perform the input/output for the 16-bit 
Unicode system. There are many classes in the ByteStream class hierarchy, but the most frequently 
used classes are FileInputStream and FileOutputStream. The most frequently used classes CharacterStream 
class hierarchy is FileReader and FileWriter.

All the stream classes can be divided into two types of classes that are ByteStream classes and
CharacterStream Classes. The ByteStream classes are further divided into InputStream classes and
OutputStream classes. CharacterStream classes are also divided into Reader classes and Writer
classes. The SuperMost classes for all the InputStream classes is java.io.InputStream and for all
the output stream classes is java.io.OutPutStream. Similarly, for all the reader classes, the
super-most class is java.io.Reader, and for all the writer classes, it is java.io.Writer.

Java FileOutputStream is an output stream used for writing data to a file. If you have some
primitive values to write into a file, use FileOutputStream class. You can write byte-oriented
as well as character-oriented data through the FileOutputStream class. However,
for character-oriented data, it is preferred to use FileWriter than FileOutputStream. Consider 
the following example of writing a byte into a file.
import java.io.FileOutputStream;    
public class FileOutputStreamExample {    
    public static void main(String args[]){      
           try{      
             FileOutputStream fout=new FileOutputStream("D:\\testout.txt");      
             fout.write(65);      
             fout.close();      
             System.out.println("success...");      
            }catch(Exception e){System.out.println(e);}      
      }      
}    
Java FileInputStream class obtains input bytes from a file. It is used for reading
byte-oriented data (streams of raw bytes) such as image data, audio, video, etc. You
can also read character-stream data. However, for reading streams of characters, it
is recommended to use FileReader class. Consider the following example for reading bytes
from a file.
import java.io.FileInputStream;    
public class DataStreamExample {    
     public static void main(String args[]){      
          try{      
            FileInputStream fin=new FileInputStream("D:\\testout.txt");      
            int i=fin.read();    
            System.out.print((char)i);      
    
            fin.close();      
          }catch(Exception e){System.out.println(e);}      
         }      
        }    
    

Java BufferedOutputStream class is used for buffering an output stream. It internally
uses a buffer to store data. It adds more efficiency than to write data directly into
a stream. So, it makes the performance fast. Whereas, Java BufferedInputStream class
is used to read information from the stream. It internally uses the buffer mechanism
to make the performance fast.

In Java, FilePermission class is used to alter the permissions set on a file. Java
FilePermission class contains the permission related to a directory or file. All the
permissions are related to the path. The path can be of two types:
D:\\IO\\-: It indicates that the permission is associated with all subdirectories and 
      files recursively.
D:\\IO\\*: It indicates that the permission is associated with all directory and files
      within this directory excluding subdirectories.
Let's see the simple example in which permission of a directory path is granted with read
permission and a file of this directory is granted for write permission.
package com.javatpoint;  
import java.io.*;  
import java.security.PermissionCollection;  
public class FilePermissionExample{  
     public static void main(String[] args) throws IOException {  
      String srg = "D:\\IO Package\\java.txt";  
      FilePermission file1 = new FilePermission("D:\\IO Package\\-", "read");  
      PermissionCollection permission = file1.newPermissionCollection();  
      permission.add(file1);  
           FilePermission file2 = new FilePermission(srg, "write");  
           permission.add(file2);  
         if(permission.implies(new FilePermission(srg, "read,write"))) {  
           System.out.println("Read, Write permission is granted for the path "+srg );  
             }else {  
            System.out.println("No Read, Write permission is granted for the path "+srg);            }  
     }   
}  

FilterStream classes are used to add additional functionalities to the other stream classes.
FilterStream classes act like an interface which read the data from a stream, filters it,
and pass the filtered data to the caller. The FilterStream classes provide extra
functionalities like adding line numbers to the destination file, etc.

An I/O filter is an object that reads from one stream and writes to another, usually altering
the data in some way as it is passed from one stream to another. Many Filter classes that allow
a user to make a chain using multiple input streams. It generates a combined effect on several
filters.

In Java, there are three ways by using which, we can take input from the console:
Using BufferedReader class: we can take input from the console by wrapping System.
	in into an InputStreamReader and passing it into the BufferedReader. It provides an
	efficient reading as the input gets buffered. Consider the following example.
import java.io.BufferedReader;   
import java.io.IOException;   
import java.io.InputStreamReader;   
public class Person   
{   
    public static void main(String[] args) throws IOException    
    {   
      System.out.println("Enter the name of the person");  
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));   
        String name = reader.readLine();   
        System.out.println(name);           
    }   
}   
Using Scanner class: The Java Scanner class breaks the input into tokens using a delimiter
	that is whitespace by default. It provides many methods to read and parse various primitive
	values. Java Scanner class is widely used to parse text for string and primitive types using
	a regular expression. Java Scanner class extends Object class and implements Iterator and
	Closeable interfaces. Consider the following example.
import java.util.*;    
public class ScannerClassExample2 {      
      public static void main(String args[]){                         
          String str = "Hello/This is JavaTpoint/My name is Abhishek.";    
          //Create scanner with the specified String Object    
          Scanner scanner = new Scanner(str);    
          System.out.println("Boolean Result: "+scanner.hasNextBoolean());              
          //Change the delimiter of this scanner    
          scanner.useDelimiter("/");    
          //Printing the tokenized Strings    
          System.out.println("---Tokenizes String---");     
        while(scanner.hasNext()){    
            System.out.println(scanner.next());    
        }    
          //Display the new delimiter    
          System.out.println("Delimiter used: " +scanner.delimiter());              
          scanner.close();    
          }      
}    
    
Using Console class: The Java Console class is used to get input from the console. It provides
	methods to read texts and passwords. If you read the password using the Console class, it will
	not be displayed to the user. The java.io.Console class is attached to the system console internally.
	The Console class is introduced since 1.5. Consider the following example.
import java.io.Console;    
class ReadStringTest{      
public static void main(String args[]){      
Console c=System.console();      
System.out.println("Enter your name: ");      
String n=c.readLine();      
System.out.println("Welcome "+n);      
}      
}    

Serialization in Java is a mechanism of writing the state of an object into a byte stream. It is
used primarily in Hibernate, RMI, JPA, EJB and JMS technologies. It is mainly used to travel
object's state on the network (which is known as marshaling). Serializable interface is used
to perform serialization. It is helpful when you require to save the state of a program to storage
such as the file. At a later point of time, the content of this file can be restored using 
deserialization. It is also required to implement RMI(Remote Method Invocation). With the help of 
RMI, it is possible to invoke the method of a Java object on one machine to another machine.

A class can become serializable by implementing the Serializable interface.
It is very tricky to prevent serialization of child class if the base class is intended to implement
the Serializable interface. However, we cannot do it directly, but the serialization can be avoided
by implementing the writeObject() or readObject() methods in the subclass and
throw NotSerializableException from these methods. 
import java.io.FileInputStream;   
import java.io.FileOutputStream;   
import java.io.IOException;   
import java.io.NotSerializableException;   
import java.io.ObjectInputStream;   
import java.io.ObjectOutputStream;   
import java.io.Serializable;   
class Person implements Serializable   
{   
    String name = " ";  
    public Person(String name)    
    {   
        this.name = name;   
    }         
}   
class Employee extends Person  
{   
    float salary;  
    public Employee(String name, float salary)    
    {   
        super(name);   
        this.salary = salary;   
    }   
    private void writeObject(ObjectOutputStream out) throws IOException   
    {   
        throw new NotSerializableException();   
    }   
    private void readObject(ObjectInputStream in) throws IOException   
    {   
        throw new NotSerializableException();   
    }   
        
}   
public class Test   
{   
    public static void main(String[] args)    
            throws Exception    
    {   
        Employee emp = new Employee("Sharma", 10000);   
            
        System.out.println("name = " + emp.name);   
        System.out.println("salary = " + emp.salary);   
            
        FileOutputStream fos = new FileOutputStream("abc.ser");   
        ObjectOutputStream oos = new ObjectOutputStream(fos);   
                
        oos.writeObject(emp);   
                
        oos.close();   
        fos.close();   
                
        System.out.println("Object has been serialized");   
            
        FileInputStream f = new FileInputStream("ab.txt");   
        ObjectInputStream o = new ObjectInputStream(f);   
                
        Employee emp1 = (Employee)o.readObject();   
                
        o.close();   
        f.close();   
                
        System.out.println("Object has been deserialized");   
            
        System.out.println("name = " + emp1.name);   
        System.out.println("salary = " + emp1.salary);   
    }   
}   

we can transfer a serialized object via network because the serialized object is stored in the memory
in the form of bytes and can be transmitted over the network. We can also write the serialized object
to the disk or the database.

Deserialization is the process of reconstructing the object from the serialized state. It is the reverse
operation of serialization. An ObjectInputStream deserializes objects and primitive data written using an
ObjectOutputStream.
import java.io.*;  
class Depersist{  
 public static void main(String args[])throws Exception{  
    
  ObjectInputStream in=new ObjectInputStream(new FileInputStream("f.txt"));  
  Student s=(Student)in.readObject();  
  System.out.println(s.id+" "+s.name);  
  
  in.close();  
 }  
}  

If you define any data member as transient, it will not be serialized. By determining transient keyword,
the value of variable need not persist when it is restored. More details.

The Externalizable interface is used to write the state of an object into a byte stream in a compressed
format. It is not a marker interface.

difference between Serializable and Externalizable interface:
1)	The Serializable interface does not have any method, i.e., it is a marker interface.
	The Externalizable interface contains is not a marker interface, It contains two methods,
	i.e., writeExternal() and readExternal().
2)	It is used to "mark" Java classes so that objects of these classes may get the certain capability.
	The Externalizable interface provides control of the serialization logic to the programmer.
3)	It is easy to implement but has the higher performance cost.	It is used to perform the
    serialization and often result in better performance.
4)	No class constructor is called in serialization.	We must call a public default constructor
    while using this interface.

Java Socket programming is used for communication between the applications running on different JRE.
Java Socket programming can be connection-oriented or connectionless. Socket and ServerSocket classes
are used for connection-oriented socket programming and DatagramSocket, and DatagramPacket classes are
used for connectionless socket programming. The client in socket programming must know two information:
	IP address of the server
	port number

A socket is simply an endpoint for communications between the machines. It provides the connection 
mechanism to connect the two computers using TCP. The Socket class can be used to create a socket.

steps that are followed when two computers connect through TCP:
The ServerSocket object is instantiated by the server which denotes the port number to which,
the connection will be made.
After instantiating the ServerSocket object, the server invokes accept() method of ServerSocket
class which makes server wait until the client attempts to connect to the server on the given port.
Meanwhile, the server is waiting, a socket is created by the client by instantiating Socket class.
The socket class constructor accepts the server port number and server name.
The Socket class constructor attempts to connect with the server on the specified name.
If the connection is established, the client will have a socket object that can communicate with the server.
The accept() method invoked by the server returns a reference to the new socket on the server that
is connected with the server.

program in Java to establish a connection between client and server:
import java.io.*;  
import java.net.*;  
public class MyServer {  
public static void main(String[] args){  
try{  
ServerSocket ss=new ServerSocket(6666);  
Socket s=ss.accept();//establishes connection   
DataInputStream dis=new DataInputStream(s.getInputStream());  
String  str=(String)dis.readUTF();  
System.out.println("message= "+str);  
ss.close();  
}catch(Exception e){System.out.println(e);}  
}  
}  
import java.io.*;  
import java.net.*;  
public class MyClient {  
public static void main(String[] args) {  
try{    
Socket s=new Socket("localhost",6666);  
DataOutputStream dout=new DataOutputStream(s.getOutputStream());  
dout.writeUTF("Hello Server");  
dout.flush();  
dout.close();  
s.close();  
}catch(Exception e){System.out.println(e);}  
}  
}  

convert a numeric IP address like 192.18.97.39 into a hostname like java.sun.com:
By InetAddress.getByName("192.18.97.39").getHostName() where 192.18.97.39 is the IP address:
import java.io.*;    
import java.net.*;    
public class InetDemo{    
public static void main(String[] args){    
try{    
InetAddress ip=InetAddress.getByName("195.201.10.8");  
System.out.println("Host Name: "+ip.getHostName());    
}catch(Exception e){System.out.println(e);}    
}    
}    

Reflection is the process of examining or modifying the runtime behavior of a class at runtime.
The java.lang.Class class provides various methods that can be used to get metadata, examine and
change the runtime behavior of a class. The java.lang and java.lang.reflect packages provide
classes for java reflection.

The java.lang.Class class performs mainly two tasks:
Provides methods to get the metadata of a class at runtime.
Provides methods to examine and change the runtime behavior of a class.

three ways to instantiate the Class class:
forName() method of Class class: The forName() method is used to load the class dynamically.
 It returns the instance of Class class. It should be used if you know the fully qualified
 name of the class. This cannot be used for primitive types.
getClass() method of Object class: It returns the instance of Class class. It should be used
 if you know the type. Moreover, it can be used with primitives.
the .class syntax: If a type is available, but there is no instance then it is possible to
 obtain a Class by appending ".class" to the name of the type. It can be used for primitive
 data type also.

class Simple{    
 public Simple()  
 {  
   System.out.println("Constructor of Simple class is invoked");  
 }  
 void message(){System.out.println("Hello Java");}    
}        
class Test1{    
 public static void main(String args[]){    
  try{    
  Class c=Class.forName("Simple");    
  Simple s=(Simple)c.newInstance();    
  s.message();    
  }catch(Exception e){System.out.println(e);}    
 }    
}    
The newInstance() method of the Class class is used to invoke the constructor at runtime. 
In this program, the instance of the Simple class is created.

The javap command disassembles a class file. The javap command displays information about
 the fields, constructors and methods present in a class file.

You can call the private method from outside the class by changing the runtime behaviour of the class.

With the help of java.lang.Class class and java.lang.reflect.Method class, we can call a
 private method from any other class.
Required methods of Method class:
1) public void setAccessible(boolean status) throws SecurityException sets the accessibility of the method.
2) public Object invoke(Object method, Object... args) throws IllegalAccessException,
   IllegalArgumentException, InvocationTargetException is used to invoke the method.
Required method of Class class:
1) public Method getDeclaredMethod(String name,Class[] parameterTypes)throws NoSuchMethodException,
   SecurityException: returns a Method object that reflects the specified declared method of the class
   or interface represented by this Class object.

calling private method from another class:
public class A {  
  private void message(){System.out.println("hello java"); }  
}  
import java.lang.reflect.Method;  
public class MethodCall{  
public static void main(String[] args)throws Exception{  
  
    Class c = Class.forName("A");  
    Object o= c.newInstance();  
    Method m =c.getDeclaredMethod("message", null);  
    m.setAccessible(true);  
    m.invoke(o, null);  
}  
}  

call parameterized private method from another class:
class A{  
private void cube(int n){System.out.println(n*n*n);}  
}  
import java.lang.reflect.*;  
class M{  
public static void main(String args[])throws Exception{  
Class c=A.class;  
Object obj=c.newInstance();  
Method m=c.getDeclaredMethod("cube",new Class[]{int.class});  
m.setAccessible(true);  
m.invoke(obj,4);  
}}  

Accessing Private Constructors of a class:
constructors of a class are a special kind of method this is used to instantiate the class.
 To access the private constructor, we use the method getDeclaredConstructor().
 The getDeclaredConstructor() is used to access a parameterless as well as a parametrized
 constructor of a class. The following example shows the same:  
import java.lang.reflect.Constructor;  
import java.lang.reflect.Modifier;  
import java.lang.reflect.InvocationTargetException;  
class Vehicle   
{     
private Integer vId;  
private String vName;  
private Vehicle()  
{  
      
}    
private Vehicle(Integer vId, String vName)   
{  
   this.vId = vId;  
   this.vName = vName;  
}    
public void setVehicleId(Integer vId)  
{  
   this.vId = vId;  
}  
  
public void setVehicleName(String vName)  
{  
   this.vName = vName;   
}   
public Integer getVehicleId()   
{  
   return vId;  
}  
public String getVehicleName()   
{  
  return vName;  
}  
}  
public class PvtConstructorDemo   
{  
// the createObj() method is used to create an object of Vehicle class using the parameterless constructor.   
public void craeteObj(int vId, String vName) throws InstantiationException, IllegalAccessException,   
IllegalArgumentException, InvocationTargetException, NoSuchMethodException   
{  
// using the parametereless contructor  
Constructor<Vehicle> constt = Vehicle.class.getDeclaredConstructor();  
constt.setAccessible(true);  
Object obj = constt.newInstance();  
if (obj instanceof Vehicle)   
{  
  Vehicle v = (Vehicle)obj;  
   v.setVehicleId(vId);  
   v.setVehicleName(vName);  
     System.out.println("Vehicle Id: " +  v.getVehicleId());  
     System.out.println("Vehicle Name: " +  v.getVehicleName());  
}  
}  
// the craeteObjByConstructorName() method is used to create an object   
// of the Vehicle class using the parameterized constructor.   
public void craeteObjByConstructorName(int vId, String vName) throws NoSuchMethodException, SecurityException,  
InstantiationException, IllegalAccessException, IllegalArgumentException, InvocationTargetException  
{  
// using the parameterized contructor  
Constructor<Vehicle> constt = Vehicle.class.getDeclaredConstructor(Integer.class, String.class);  
if (Modifier.isPrivate(constt.getModifiers()))   
{  
constt.setAccessible(true);      
Object obj = constt.newInstance(vId, vName);  
if(obj instanceof Vehicle)  
{  
     Vehicle v = (Vehicle)obj;  
     System.out.println("Vehicle Id: " +  v.getVehicleId());  
     System.out.println("Vehicle Name: " + v.getVehicleName());  
}  
}  
}  
// delegating the responsibility to Java Virtual Machine (JVM) to handle the raised   
// exception  
// main method  
public static void main(String argvs[]) throws InstantiationException,   
IllegalAccessException, IllegalArgumentException, InvocationTargetException,   
NoSuchMethodException, SecurityException   
{       
   // creating an object of the class PvtConstructorDemo  
   PvtConstructorDemo ob = new PvtConstructorDemo();  
   ob.craeteObj(20, "Indica");  
   System.out.println(" -------------------------- ");  
   ob.craeteObjByConstructorName(30, "Alto");  
}  
}  

Wrapper classes are classes that allow primitive types to be accessed as objects. In other words,
we can say that wrapper classes are built-in java classes which allow the conversion of objects
to primitives and primitives to objects. The process of converting primitives to objects is
called autoboxing, and the process of converting objects to primitives is called unboxing.
There are eight wrapper classes present in java.lang package is given below.
Primitive Type	Wrapper class:
boolean	Boolean
char	Character
byte	Byte
short	Short
int	Integer
long	Long
float	Float
double	Double

The autoboxing is the process of converting primitive data type to the corresponding wrapper
class object, eg., int to Integer. The unboxing is the process of converting wrapper class
object to primitive data type. For eg., integer to int. Unboxing and autoboxing occur
automatically in Java. However, we can externally convert one into another by using the
methods like valueOf() or xxxValue().
It can occur whenever a wrapper class object is expected, and primitive data type is provided or vice versa:
Adding primitive types into Collection like ArrayList in Java.
Creating an instance of parameterized classes ,e.g., ThreadLocal which expect Type.
Java automatically converts primitive to object whenever one is required and another is
 provided in the method calling.
When a primitive type is assigned to an object type.

public class Test1  
{  
  public static void main(String[] args) {  
  Integer i = new Integer(201);  
  Integer j = new Integer(201);  
  if(i == j)  
  {  
    System.out.println("hello");  
  }  
  else   
  {  
    System.out.println("bye");  
  }  
  }  
}  
The Integer class caches integer values from -127 to 127. Therefore, the Integer objects
can only be created in the range -128 to 127. The operator == will not work for the value
greater than 127; thus bye is printed.

The object cloning is a way to create an exact copy of an object. The clone() method of the
Object class is used to clone an object. The java.lang.Cloneable interface must be implemented
by the class whose object clone we want to create. If we don't implement Cloneable interface,
clone() method generates CloneNotSupportedException. The clone() method is defined in the Object
class. The syntax of the clone() method is as follows:
protected Object clone() throws CloneNotSupportedException

Advantage of Object Cloning:
You don't need to write lengthy and repetitive codes. Just use an abstract class with a
4- or 5-line long clone() method. It is the easiest and most efficient way of copying objects,
especially if we are applying it to an already developed or an old project. Just define a
parent class, implement Cloneable in it, provide the definition of the clone() method and 
the task will be done. Clone() is the fastest way to copy the array.
Disadvantage of Object Cloning:
To use the Object.clone() method, we have to change many syntaxes to our code, like implementing
a Cloneable interface, defining the clone() method and handling CloneNotSupportedException, and
finally, calling Object.clone(), etc.
We have to implement the Cloneable interface while it does not have any methods in it. We have
to use it to tell the JVM that we can perform a clone() on our object.
Object.clone() is protected, so we have to provide our own clone() and indirectly call
Object.clone() from it.
Object.clone() does not invoke any constructor, so we do not have any control over object construction.
If you want to write a clone method in a child class, then all of its superclasses should define
the clone() method in them or inherit it from another parent class. Otherwise, the super.clone()
chain will fail.
Object.clone() supports only shallow copying, but we will need to override it if we need deep cloning.

A native method is a method that is implemented in a language other than Java. Natives methods
are sometimes also referred to as foreign methods.

Java strictfp keyword ensures that you will get the same result on every platform
if you perform operations in the floating-point variable. The precision may differ
from platform to platform that is why java programming language has provided the
strictfp keyword so that you get the same result on every platform. So, now you
have better control over the floating-point arithmetic.

The purpose of the System class is to provide access to system resources such as
standard input and output. It cannot be instantiated. Facilities provided by System class are given below:
Standard input
Error output streams
Standard output
utility method to copy the portion of an array
utilities to load files and libraries
There are the three fields of Java System class, i.e., static printstream err,
 static inputstream in, and standard output stream.

shallow copy <--> Object cloning.

Singleton class is the class which can not be instantiated more than once. To make a class singleton,
we either make its constructor private or use the static getInstance method. Consider the following example.
class Singleton{  
    private static Singleton single_instance = null;  
    int i;  
     private Singleton ()  
     {  
         i=90;  
     }  
     public static Singleton getInstance()  
     {  
         if(single_instance == null)  
         {  
             single_instance = new Singleton();  
         }  
         return single_instance;  
     }  
}  
public class Main   
{  
    public static void main (String args[])  
    {  
        Singleton first = Singleton.getInstance();  
        System.out.println("First instance integer value:"+first.i);  
        first.i=first.i+90;  
        Singleton second = Singleton.getInstance();  
        System.out.println("Second instance integer value:"+second.i);  
    }  
}  
      
Java program that prints all the values given at command-line:
class A{  
public static void main(String args[]){  
  
for(int i=0;i<args.length;i++)  
System.out.println(args[i]);  
  
}  
}  

A Locale object represents a specific geographical, political, or cultural region. This object can
be used to get the locale-specific information such as country name, language, variant, etc.
import java.util.*;  
public class LocaleExample {  
public static void main(String[] args) {  
Locale locale=Locale.getDefault();  
//Locale locale=new Locale("fr","fr");//for the specific locale    
System.out.println(locale.getDisplayCountry());  
System.out.println(locale.getDisplayLanguage());  
System.out.println(locale.getDisplayName());  
System.out.println(locale.getISO3Country());  
System.out.println(locale.getISO3Language());  
System.out.println(locale.getLanguage());  
System.out.println(locale.getCountry());  
      
}  
}  

load a specific locale By ResourceBundle.getBundle(?) method.

JavaBean is a reusable software component written in the Java programming language, designed to
be manipulated visually by a software development environment, like JBuilder or VisualAge for Java.
A JavaBean encapsulates many objects into one object so that we can access this object from multiple
places. Moreover, it provides the easy maintenance. Consider the following example to create a
JavaBean class.
package mypack;  
public class Employee implements java.io.Serializable{  
private int id;  
private String name;  
public Employee(){}  
public void setId(int id){this.id=id;}  
public int getId(){return id;}  
public void setName(String name){this.name=name;}  
public String getName(){return name;}  
} 
 
A bean encapsulates many objects into one object so that we can access this object from multiple places.
Moreover, it provides the easy maintenance.

The persistence property of Java bean comes into the act when the properties, fields, and state
information are saved to or retrieve from the storage.

The RMI (Remote Method Invocation) is an API that provides a mechanism to create the distributed
application in java. The RMI allows an object to invoke methods on an object running in another
JVM. The RMI provides remote communication between the applications using two objects stub and skeleton.

The stub is an object, acts as a gateway for the client side. All the outgoing requests are routed
through it. It resides at the client side and represents the remote object. When the caller invokes
the method on the stub object, it does the following tasks:
It initiates a connection with remote Virtual Machine (JVM).
It writes and transmits (marshals) the parameters to the remote Virtual Machine (JVM).
It waits for the result.
It reads (unmarshals) the return value or exception.
It finally, returns the value to the caller.

The skeleton is an object, acts as a gateway for the server side object. All the incoming requests are
routed through it. When the skeleton receives the incoming request, it does the following tasks:
It reads the parameter for the remote method.
It invokes the method on the actual remote object.
It writes and transmits (marshals) the result to the caller.

There are 6 steps which are performed to write RMI based programs:
Create the remote interface.
Provide the implementation of the remote interface.
Compile the implementation class and create the stub and skeleton objects using the rmic tool.
Start the registry service by the rmiregistry tool.
Create and start the remote application.
Create and start the client application.

HTTP-tunneling in RMI can be defined as the method which doesn't need any setup to work within the
firewall environment. It handles the HTTP connections through the proxy servers. However, it does
not allow outbound TCP connections.

JRMP (Java Remote Method Protocol) can be defined as the Java-specific, stream-based protocol which
looks up and refers to the remote objects. It requires both client and server to use Java objects.
It is wire level protocol which runs under RMI and over TCP/IP.


Multithreading in Java is a process of executing multiple threads simultaneously.
A thread is a lightweight sub-process, the smallest unit of processing. Multiprocessing
and multithreading, both are used to achieve multitasking.However, we use multithreading
than multiprocessing because threads use a shared memory area. They don't allocate separate
memory area so saves memory, and context-switching between the threads takes less time than process.
Java Multithreading is mostly used in games, animation, etc.
Advantages of Java Multithreading
1) It doesn't block the user because threads are independent and you can perform multiple operations at the same time.
2) You can perform many operations together, so it saves time.
3) Threads are independent, so it doesn't affect other threads if an exception occurs in a single thread.

Multitasking is a process of executing multiple tasks simultaneously. We use multitasking to utilize the
CPU. Multitasking can be achieved in two ways:
1) Process-based Multitasking (Multiprocessing)
Each process has an address in memory. In other words, each process allocates a separate memory area.
A process is heavyweight.
Cost of communication between the process is high.
Switching from one process to another requires some time for saving and loading registers, memory maps,
updating lists, etc.
2) Thread-based Multitasking (Multithreading)
Threads share the same address space.
A thread is lightweight.
Cost of communication between the thread is low.
At least one process is required for each thread.

A thread is a lightweight subprocess, the smallest unit of processing. It is a separate path of execution.
Threads are independent. If there occurs exception in one thread, it doesn't affect other threads.
It uses a shared memory area.
As shown in the above figure, a thread is executed inside the process. There is context-switching
between the threads. There can be multiple processes inside the OS, and one process can have multiple
threads. At a time one thread is executed only.

Java provides Thread class to achieve thread programming. Thread class provides constructors
and methods to create and perform operations on a thread. Thread class extends Object class
and implements Runnable interface.
Java Thread Methods
S.N.	Modifier and Type	Method	Description
1)	void	start()	It is used to start the execution of the thread.
2)	void	run()	It is used to do an action for a thread.
3)	static void	sleep()	It sleeps a thread for the specified amount of time.
4)	static Thread	currentThread()	It returns a reference to the currently executing thread object.
5)	void	join()	It waits for a thread to die.
6)	int	getPriority()	It returns the priority of the thread.
7)	void	setPriority()	It changes the priority of the thread.
8)	String	getName()	It returns the name of the thread.
9)	void	setName()	It changes the name of the thread.
10)	long	getId()	It returns the id of the thread.
11)	boolean	isAlive()	It tests if the thread is alive.
12)	static void	yield()	It causes the currently executing thread object to pause and allow other threads to execute temporarily.
13)	void	suspend()	It is used to suspend the thread.
14)	void	resume()	It is used to resume the suspended thread.
15)	void	stop()	It is used to stop the thread.
16)	void	destroy()	It is used to destroy the thread group and all of its subgroups.
17)	boolean	isDaemon()	It tests if the thread is a daemon thread.
18)	void	setDaemon()	It marks the thread as daemon or user thread.
19)	void	interrupt()	It interrupts the thread.
20)	boolean	isinterrupted()	It tests whether the thread has been interrupted.
21)	static boolean	interrupted()	It tests whether the current thread has been interrupted.
22)	static int	activeCount()	It returns the number of active threads in the current thread's thread group.
23)	void	checkAccess()	It determines if the currently running thread has permission to modify the thread.
24)	static boolean	holdLock()	It returns true if and only if the current thread holds the monitor lock on the specified object.
25)	static void	dumpStack()	It is used to print a stack trace of the current thread to the standard error stream.
26)	StackTraceElement[]	getStackTrace()	It returns an array of stack trace elements representing the stack dump of the thread.
27)	static int	enumerate()	It is used to copy every active thread's thread group and its subgroup into the specified array.
28)	Thread.State	getState()	It is used to return the state of the thread.
29)	ThreadGroup	getThreadGroup()	It is used to return the thread group to which this thread belongs
30)	String	toString()	It is used to return a string representation of this thread, including the thread's name, priority, and thread group.
31)	void	notify()	It is used to give the notification for only one thread which is waiting for a particular object.
32)	void	notifyAll()	It is used to give the notification to all waiting threads of a particular object.
33)	void	setContextClassLoader()	It sets the context ClassLoader for the Thread.
34)	ClassLoader	getContextClassLoader()	It returns the context ClassLoader for the thread.
35)	static Thread.UncaughtExceptionHandler	getDefaultUncaughtExceptionHandler()	It returns the default handler invoked when a thread abruptly terminates due to an uncaught exception.
36)	static void	setDefaultUncaughtExceptionHandler()	It sets the default handler invoked when a thread abruptly terminates due to an uncaught exception.

Life cycle of a Thread (Thread States):
In Java, a thread always exists in any one of the following states. These states are:
New: Whenever a new thread is created, it is always in the new state. For a thread in the new state,
 the code has not been run yet and thus has not begun its execution.
Active: When a thread invokes the start() method, it moves from the new state to the active state.
 The active state contains two states within it: one is runnable, and the other is running.
Runnable: A thread, that is ready to run is then moved to the runnable state. In the runnable state,
 the thread may be running or may be ready to run at any given instant of time. It is the duty of
 the thread scheduler to provide the thread time to run, i.e., moving the thread the running state.
A program implementing multithreading acquires a fixed slice of time to each individual thread.
 Each and every thread runs for a short span of time and when that allocated time slice is over,
 the thread voluntarily gives up the CPU to the other thread, so that the other threads can also
 run for their slice of time. Whenever such a scenario occurs, all those threads that are willing
 to run, waiting for their turn to run, lie in the runnable state. In the runnable state, there is
 a queue where the threads lie.
Running: When the thread gets the CPU, it moves from the runnable to the running state. Generally,
 the most common change in the state of a thread is from runnable to running and again back to runnable.
Blocked or Waiting: Whenever a thread is inactive for a span of time (not permanently) then, either
 the thread is in the blocked state or is in the waiting state.

For example, a thread (let's say its name is A) may want to print some data from the printer. However,
at the same time, the other thread (let's say its name is B) is using the printer to print some data.
Therefore, thread A has to wait for thread B to use the printer. Thus, thread A is in the blocked state.
A thread in the blocked state is unable to perform any execution and thus never consume any cycle of the
Central Processing Unit (CPU). Hence, we can say that thread A remains idle until the thread scheduler
reactivates thread A, which is in the waiting or blocked state.

When the main thread invokes the join() method then, it is said that the main thread is in the waiting
state. The main thread then waits for the child threads to complete their tasks. When the child threads
complete their job, a notification is sent to the main thread, which again moves the thread from waiting
to the active state.
If there are a lot of threads in the waiting or blocked state, then it is the duty of the thread scheduler
to determine which thread to choose and which one to reject, and the chosen thread is then given the
opportunity to run.
Timed Waiting: Sometimes, waiting for leads to starvation. For example, a thread (its name is A) has
 entered the critical section of a code and is not willing to leave that critical section. In such a
 scenario, another thread (its name is B) has to wait forever, which leads to starvation. To avoid
 such scenario, a timed waiting state is given to thread B. Thus, thread lies in the waiting state
 for a specific span of time, and not forever. A real example of timed waiting is when we invoke the
 sleep() method on a specific thread. The sleep() method puts the thread in the timed wait state. After
 the time runs out, the thread wakes up and start its execution from when it has left earlier.
Terminated: A thread reaches the termination state because of the following reasons:
When a thread has finished its job, then it exists or terminates normally.
Abnormal termination: It occurs when some unusual events such as an unhandled exception or
 segmentation fault.
A terminated thread means the thread is no more in the system. In other words, the thread is
 dead, and there is no way one can respawn (active after kill) the dead thread.

The following diagram shows the different states involved in the life cycle of a thread.
https://www.javatpoint.com/life-cycle-of-a-thread

Implementation of Thread States:
In Java, one can get the current state of a thread using the Thread.getState() method. The
 java.lang.Thread.State class of Java provides the constants ENUM to represent the state of a thread.
 These constants are:
public static final Thread.State NEW  
It represents the first state of a thread that is the NEW state.
public static final Thread.State RUNNABLE  
It represents the runnable state.It means a thread is waiting in the queue to run.
public static final Thread.State BLOCKED  
It represents the blocked state. In this state, the thread is waiting to acquire a lock.
public static final Thread.State WAITING  
It represents the waiting state. A thread will go to this state when it invokes the Object.wait()
 method, or Thread.join() method with no timeout. A thread in the waiting state is waiting for
 another thread to complete its task.
public static final Thread.State TIMED_WAITING  
It represents the timed waiting state. The main difference between waiting and timed waiting is the time
 constraint. Waiting has no time constraint, whereas timed waiting has the time constraint. A thread
 invoking the following method reaches the timed waiting state.
sleep
join with timeout
wait with timeout
parkUntil
parkNanos
public static final Thread.State TERMINATED  
It represents the final state of a thread that is terminated or dead. A terminated thread means it
 has completed its execution.

Java Program for Demonstrating Thread States
class ABC implements Runnable  
{  
public void run()  
{  
try  
{  
// moving thread t2 to the state timed waiting  
Thread.sleep(100);  
}  
catch (InterruptedException ie)  
{  
ie.printStackTrace();  
}    
System.out.println("The state of thread t1 while it invoked the method join() on thread t2 -"+
 ThreadState.t1.getState());  
try  
{  
Thread.sleep(200);  
}  
catch (InterruptedException ie)  
{  
ie.printStackTrace();  
}     
}  
}    
public class ThreadState implements Runnable  
{  
public static Thread t1;  
public static ThreadState obj;  
public static void main(String argvs[])  
{  
obj = new ThreadState();  
t1 = new Thread(obj);   
// thread t1 is spawned   
// The thread t1 is currently in the NEW state.  
System.out.println("The state of thread t1 after spawning it - " + t1.getState());  
// invoking the start() method on the thread t1  
t1.start();    
// thread t1 is moved to the Runnable state  
System.out.println("The state of thread t1 after invoking the method start() on it - " + t1.getState());  
}  
  
public void run()  
{  
ABC myObj = new ABC();  
Thread t2 = new Thread(myObj);    
// thread t2 is created and is currently in the NEW state.  
System.out.println("The state of thread t2 after spawning it - "+ t2.getState());  
t2.start();  
// thread t2 is moved to the runnable state  
System.out.println("the state of thread t2 after calling the method start() on it - " + t2.getState());  
// try-catch block for the smooth flow of the  program  
try  
{  
// moving the thread t1 to the state timed waiting   
Thread.sleep(200);  
}  
catch (InterruptedException ie)  
{  
ie.printStackTrace();  
}  
System.out.println("The state of thread t2 after invoking the method sleep() on it - "+ t2.getState());  
// try-catch block for the smooth flow of the  program  
try  
{  
// waiting for thread t2 to complete its execution  
t2.join();  
}  
catch (InterruptedException ie)  
{  
ie.printStackTrace();  
}  
System.out.println("The state of thread t2 when it has completed it's execution - " + t2.getState());  
}  
}  

two ways to create a thread:
Thread class: provide constructors and methods to create and perform operations on a thread.
Thread class extends Object class and implements Runnable interface.

Commonly used Constructors of Thread class:
Thread()
Thread(String name)
Thread(Runnable r)
Thread(Runnable r,String name)
Commonly used methods of Thread class:
public void run(): is used to perform action for a thread.
public void start(): starts the execution of the thread.JVM calls the run() method on the thread.
public void sleep(long miliseconds): Causes the currently executing thread to sleep (temporarily
 cease execution) for the specified number of milliseconds.
public void join(): waits for a thread to die.
public void join(long miliseconds): waits for a thread to die for the specified miliseconds.
public int getPriority(): returns the priority of the thread.
public int setPriority(int priority): changes the priority of the thread.
public String getName(): returns the name of the thread.
public void setName(String name): changes the name of the thread.
public Thread currentThread(): returns the reference of currently executing thread.
public int getId(): returns the id of the thread.
public Thread.State getState(): returns the state of the thread.
public boolean isAlive(): tests if the thread is alive.
public void yield(): causes the currently executing thread object to temporarily pause and allow
 other threads to execute.
public void suspend(): is used to suspend the thread(depricated).
public void resume(): is used to resume the suspended thread(depricated).
public void stop(): is used to stop the thread(depricated).
public boolean isDaemon(): tests if the thread is a daemon thread.
public void setDaemon(boolean b): marks the thread as daemon or user thread.
public void interrupt(): interrupts the thread.
public boolean isInterrupted(): tests if the thread has been interrupted.
public static boolean interrupted(): tests if the current thread has been interrupted.
Runnable interface:
The Runnable interface should be implemented by any class whose instances are intended to be executed by
 a thread. Runnable interface have only one method named run().
The start() method performs the following tasks:
A new thread starts(with new callstack).
The thread moves from New state to the Runnable state.
When the thread gets a chance to execute, its target run() method will run.

Java Thread Example by extending Thread class
class Multi extends Thread{  
public void run(){  
System.out.println("thread is running...");  
}  
public static void main(String args[]){  
Multi t1=new Multi();  
t1.start();  
 }  
}  

Java Thread Example by implementing Runnable interface
class Multi3 implements Runnable{  
public void run(){  
System.out.println("thread is running...");  
}    
public static void main(String args[]){  
Multi3 m1=new Multi3();  
Thread t1 =new Thread(m1);   // Using the constructor Thread(Runnable r)  
t1.start();  
 }  
}  
If you are not extending the Thread class, your class object would not be treated as a thread object.
 So you need to explicitly create the Thread class object. We are passing the object of your
 class that implements Runnable so that your class run() method may execute.

We can directly use the Thread class to spawn new threads using the constructors defined above.
public class MyThread1  
{  
// Main method  
public static void main(String argvs[])  
{  
// creating an object of the Thread class using the constructor Thread(String name)   
Thread t= new Thread("My first thread");    
// the start() method moves the thread to the active state  
t.start();  
// getting the thread name by invoking the getName() method  
String str = t.getName();  
System.out.println(str);  
}  
}  

Using the Thread Class: Thread(Runnable r, String name)
public class MyThread2 implements Runnable  
{    
public void run()  
{    
System.out.println("Now the thread is running ...");    
}    
// main method  
public static void main(String argvs[])  
{   
// creating an object of the class MyThread2  
Runnable r1 = new MyThread2();  
// creating an object of the class Thread using Thread(Runnable r, String name)  
Thread th1 = new Thread(r1, "My new thread");  
// the start() method moves the thread to the active state  
th1.start();  
// getting the thread name by invoking the getName() method  
String str = th1.getName();  
System.out.println(str);  
}    
}    

Thread Scheduler in Java:
A component of Java that decides which thread to run or execute and which thread to wait is called a
 thread scheduler in Java. In Java, a thread is only chosen by a thread scheduler if it is in the
 runnable state. However, if there is more than one thread in the runnable state, it is up to the
 thread scheduler to pick one of the threads and ignore the other ones. There are some criteria that
 decide which thread will execute first. There are two factors for scheduling a thread i.e. Priority
 and Time of arrival.

Priority: Priority of each thread lies between 1 to 10. If a thread has a higher priority, it means that
 thread has got a better chance of getting picked up by the thread scheduler.

Time of Arrival: Suppose two threads of the same priority enter the runnable state, then priority cannot
 be the factor to pick a thread from these two threads. In such a case, arrival time of thread is
 considered by the thread scheduler. A thread that arrived first gets the preference over the other threads.

Thread Scheduler Algorithms:
On the basis of the above-mentioned factors, the scheduling algorithm is followed by a Java thread scheduler:
First Come First Serve Scheduling:
the scheduler picks the threads thar arrive first in the runnable queue. Observe the following table:
Threads	Time of Arrival
t1	0
t2	1
t3	2
t4	3
In the above table, we can see that Thread t1 has arrived first, then Thread t2, then t3, and at last t4,
 and the order in which the threads will be processed is according to the time of arrival of threads.
Hence, Thread t1 will be processed first, and Thread t4 will be processed last.

Time-slicing scheduling:
Usually, the First Come First Serve algorithm is non-preemptive, which is bad as it may lead to
 infinite blocking (also known as starvation). To avoid that, some time-slices are provided to
 the threads so that after some time, the running thread has to give up the CPU. Thus, the other
 waiting threads also get time to run their job.

In the above diagram, each thread is given a time slice of 2 seconds. Thus, after 2 seconds, the
 first thread leaves the CPU, and the CPU is then captured by Thread2. The same process repeats for
 the other threads too.

Preemptive-Priority Scheduling:
The name of the scheduling algorithm denotes that the algorithm is related to the priority of the threads.

Suppose there are multiple threads available in the runnable state. The thread scheduler picks that
 thread that has the highest priority. Since the algorithm is also preemptive, therefore, time slices
 are also provided to the threads to avoid starvation. Thus, after some time, even if the highest
 priority thread has not completed its job, it has to release the CPU because of preemption.

working of the Java thread scheduler. Suppose, there are five threads that have different arrival times
 and different priorities. Now, it is the responsibility of the thread scheduler to decide which thread
 will get the CPU first.
The thread scheduler selects the thread that has the highest priority, and the thread begins the execution
of the job. If a thread is already in runnable state and another thread (that has higher priority) reaches
in the runnable state, then the current thread is pre-empted from the processor, and the arrived thread
with higher priority gets the CPU time.
When two threads (Thread 2 and Thread 3) having the same priorities and arrival time, the scheduling will
be decided on the basis of FCFS algorithm. Thus, the thread that arrives first gets the opportunity to
execute first.

The Java Thread class provides the two variant of the sleep() method. First one accepts only an arguments,
 whereas the other variant accepts two arguments. The method sleep() is being used to halt the working of
 a thread for a given amount of time. The time up to which the thread remains in the sleeping state is
 known as the sleeping time of the thread. After the sleeping time is over, the thread starts its execution
 from where it has left.

syntax of the sleep() method:
public static void sleep(long mls) throws InterruptedException   
public static void sleep(long mls, int n) throws InterruptedException   
The method sleep() with the one parameter is the native method, and the implementation of the native
 method is accomplished in another programming language. The other methods having the two parameters
 are not the native method. That is, its implementation is accomplished in Java. We can access the
 sleep() methods with the help of the Thread class, as the signature of the sleep() methods contain
 the static keyword. The native, as well as the non-native method, throw a checked Exception. Therefore,
 either try-catch block or the throws keyword can work here.

The Thread.sleep() method can be used with any thread. It means any other thread or the main thread
 can invoke the sleep() method..

Whenever the Thread.sleep() methods execute, it always halts the execution of the current thread.
Whenever another thread does interruption while the current thread is already in the sleep mode,
 then the InterruptedException is thrown.
If the system that is executing the threads is busy, then the actual sleeping time of the thread
 is generally more as compared to the time passed in arguments. However, if the system executing
 the sleep() method has less load, then the actual sleeping time of the thread is almost equal to
 the time passed in the argument.

Example on the custom thread:
class TestSleepMethod1 extends Thread{    
 public void run(){    
  for(int i=1;i<5;i++){   
    try{Thread.sleep(500);}catch(InterruptedException e){System.out.println(e);}    
    System.out.println(i);    
  }    
 }    
 public static void main(String args[]){    
  TestSleepMethod1 t1=new TestSleepMethod1();    
  TestSleepMethod1 t2=new TestSleepMethod1();      
  t1.start();    
  t2.start();    
 }    
}    
As you know well that at a time only one thread is executed. If you sleep a thread for the specified time,
 the thread scheduler picks up another thread and so on.

Example the main thread
public class TestSleepMethod2  
{  
public static void main(String argvs[])  
{  
try {  
for (int j = 0; j < 5; j++)  
{  
Thread.sleep(1000);  
System.out.println(j);  
}  
}  
catch (Exception expn)   
{  
System.out.println(expn);  
}  
}  
}  
Example When the sleeping time is negative.
public class TestSleepMethod3  
{  
public static void main(String argvs[])  
{  
try   
{  
for (int j = 0; j < 5; j++)   
{  
Thread.sleep(-100);  
System.out.println(j);  
}  
}  
catch (Exception expn)   
{  
System.out.println(expn);  
}  
}  
} 

After starting a thread, it can never be started again.

The wait() method is provided by the Object class in Java. This method is used for inter-thread
 communication in Java. The java.lang.Object.wait() is used to pause the current thread, and wait
 until another thread does not call the notify() or notifyAll() method. Its syntax is given below:
public final void wait()

wait() method be called from the synchronized block. Moreover, we need wait() method for inter-thread
 communication with notify() and notifyAll(). Therefore It must be present in the synchronized
 block for the proper and correct communication.

Multithreading programming has the following advantages:

Multithreading allows an application/program to be always reactive for input, even already
 running with some background tasks
Multithreading allows the faster execution of tasks, as threads execute independently.
Multithreading provides better utilization of cache memory as threads share the common memory resources.
Multithreading reduces the number of the required server as one server can execute multiple
 threads at a time.
 
states in the lifecycle of a Thread:A thread can have one of the following states during its lifetime:

New: In this state, a Thread class object is created using a new operator, but the thread is not alive.
 Thread doesn't start until we call the start() method.
Runnable: In this state, the thread is ready to run after calling the start() method. However, the thread
 is not yet selected by the thread scheduler.
Running: In this state, the thread scheduler picks the thread from the ready state, and the thread is
 running.
Waiting/Blocked: In this state, a thread is not running but still alive, or it is waiting for the other
 thread to finish.
Dead/Terminated: A thread is in terminated or dead state when the run() method exits.
https://www.javatpoint.com/java-multithreading-interview-questions

difference between preemptive scheduling and time slicing?
Under preemptive scheduling, the highest priority task executes until it enters the waiting or dead
 states or a higher priority task comes into existence. Under time slicing, a task executes for a
 predefined slice of time and then reenters the pool of ready tasks. The scheduler then determines
 which task should execute next, based on priority and other factors.

In Context switching the state of the process (or thread) is stored so that it can be restored and
 execution can be resumed from the same point later. Context switching enables the multiple processes
 to share the same CPU.

Differentiate between the Thread class and Runnable interface for creating a Thread?
The Thread can be created by using two ways:
By extending the Thread class
By implementing the Runnable interface
However, the primary differences between both the ways are given below:
By extending the Thread class, we cannot extend any other class, as Java does not allow multiple
 inheritances while implementing the Runnable interface; we can also extend other base class(if required).
By extending the Thread class, each of thread creates the unique object and associates with it
 while implementing the Runnable interface; multiple threads share the same object
Thread class provides various inbuilt methods such as getPriority(), isAlive and many more while
 the Runnable interface provides a single method, i.e., run().
 
The join() method waits for a thread to die. In other words, it causes the currently running threads
to stop executing until the thread it joins with completes its task. Join method is overloaded in
Thread class in the following ways:
public void join()throws InterruptedException
public void join(long milliseconds)throws InterruptedException

The sleep() method in java is used to block a thread for a particular time, which means it pause the
 execution of a thread for a specific time. There are two methods of doing so.

public static void sleep(long milliseconds)throws InterruptedException
public static void sleep(long milliseconds, int nanos)throws InterruptedException

When we call the sleep() method, it pauses the execution of the current thread for the given time and
 gives priority to another thread(if available). Moreover, when the waiting time completed then again
 previous thread changes its state from waiting to runnable and comes in running state, and the whole
 process works so on till the execution doesn't complete.

difference between wait() and sleep() method?
1) The wait() method is defined in Object class.	The sleep() method is defined in Thread class.
2) The wait() method releases the lock.	The sleep() method doesn't release the lock.

we cannot restart the thread, as once a thread started and executed, it goes to the Dead state.
Therefore, if we try to start a thread twice, it will give a
runtimeException "java.lang.IllegalThreadStateException". 
public class Multithread1 extends Thread  
{  
   public void run()  
    {  
      try {  
          System.out.println("thread is executing now........");  
      } catch(Exception e) {  
      }   
    }  
    public static void main (String[] args) {  
        Multithread1 m1= new Multithread1();  
        m1.start();  
        m1.start();  
    }  
}  

call the run() method instead of start() directly is valid, but it will not work as a thread instead
it will work as a normal object. There will not be context-switching between the threads. When we
 call the start() method, it internally calls the run() method, which creates a new stack for a thread
 while directly calling the run() will not create a new stack.

The daemon threads are the low priority threads that provide the background support and services to the
 user threads. Daemon thread gets automatically terminated by the JVM if the program remains with the
 daemon thread only, and all other user threads are ended/died. There are two methods for daemon thread
 available in the Thread class:
public void setDaemon(boolean status): It used to mark the thread daemon thread or a user thread.
public boolean isDaemon(): It checks the thread is daemon or not.

if we make the user thread as daemon thread if the thread is started it will throw
 IllegalThreadStateException. Therefore, we can only create a daemon thread before starting the thread.
class Testdaemon1 extends Thread{    
public void run(){  
          System.out.println("Running thread is daemon...");  
}  
public static void main (String[] args) {  
      Testdaemon1 td= new Testdaemon1();  
      td.start();  
      setDaemon(true);// It will throw the exception: td.   
   }  
}  

The shutdown hook is a thread that is invoked implicitly before JVM shuts down. So we can use it to perform
 clean up the resource or save the state when JVM shuts down normally or abruptly. We can add shutdown
 hook by using the following method:
public void addShutdownHook(Thread hook){}    
Runtime r=Runtime.getRuntime();  
r.addShutdownHook(new MyThread());  
Shutdown hooks initialized but can only be started when JVM shutdown occurred.
Shutdown hooks are more reliable than the finalizer() because there are very fewer chances that shutdown
 hooks not run.
The shutdown hook can be stopped by calling the halt(int) method of Runtime class.

We should interrupt a thread when we want to break out the sleep or wait state of a thread. We can
 interrupt a thread by calling the interrupt() throwing the InterruptedException.

Synchronization is the capability to control the access of multiple threads to any shared resource.
 It is used:
To prevent thread interference.
To prevent consistency problem.
When the multiple threads try to do the same task, there is a possibility of an erroneous result
, hence to remove this issue, Java uses the process of synchronization which allows only one thread
 to be executed at a time. Synchronization can be achieved in three ways:
by the synchronized method
by synchronized block
by static synchronization

The Synchronized block can be used to perform synchronization on any specific resource of the method.
 Only one thread at a time can execute on a particular resource, and all other threads which attempt
 to enter the synchronized block are blocked.
Synchronized block is used to lock an object for any shared resource.
The scope of the synchronized block is limited to the block on which, it is applied. Its scope is smaller
 than a method.

Java object can be locked down for exclusive use by a given thread by putting it in a "synchronized" block.
 The locked object is inaccessible to any thread other than the one that explicitly claimed it.

static synchronization?
If you make any static method as synchronized, the lock will be on the class not on the object.
 If we use the synchronized keyword before a method so it will lock the object (one thread can
 access an object at a time) but if we use static synchronized so it will lock a class (one thread
 can access a class at a time). More details.

The notify() is used to unblock one waiting thread whereas notifyAll() method is used to unblock all
 the threads in waiting state.

Deadlock is a situation in which every thread is waiting for a resource which is held by some other
 waiting thread. In this situation, Neither of the thread executes nor it gets the chance to be executed.
 Instead, there exists a universal waiting state among all the threads. Deadlock is a very complicated
 situation which can break our code at runtime.

We can detect the deadlock condition by running the code on cmd and collecting the Thread Dump, and if
 any deadlock is present in the code, then a message will appear on cmd.

Ways to avoid the deadlock condition in Java:

Avoid Nested lock: Nested lock is the common reason for deadlock as deadlock occurs when we provide locks
 to various threads so we should give one lock to only one thread at some particular time.
Avoid unnecessary locks: we must avoid the locks which are not required.
Using thread join: Thread join helps to wait for a thread until another thread doesn't finish its execution
 so we can avoid deadlock by maximum use of join method.
 
In Java, when we create the threads, they are supervised with the help of a Thread Scheduler, which is the
 part of JVM. Thread scheduler is only responsible for deciding which thread should be executed. Thread
 scheduler uses two mechanisms for scheduling the threads: Preemptive and Time Slicing.
Java thread scheduler also works for deciding the following for a thread:
It selects the priority of the thread.
It determines the waiting time for a thread
It checks the Nature of thread

Yes, in multithreaded programming every thread maintains its own or separate stack area in memory due to
 which every thread is independent of each other.

safety of a thread achieved?
If a method or class object can be used by multiple threads at a time without any race condition, then
 the class is thread-safe. Thread safety is used to make a program safe to use in multithreaded programming.
 It can be achieved by the following ways:

Synchronization
Using Volatile keyword
Using a lock based mechanism
Use of atomic wrapper classes

A Race condition is a problem which occurs in the multithreaded programming when various threads execute
 simultaneously accessing a shared resource at the same time. The proper use of synchronization can
 avoid the Race condition.

Volatile keyword is used in multithreaded programming to achieve the thread safety, as a change in one
 volatile variable is visible to all other threads so one variable can be used by one thread at a time.

Java Thread pool represents a group of worker threads, which are waiting for the task to be allocated.
Threads in the thread pool are supervised by the service provider which pulls one thread from the pool
 and assign a job to it.
After completion of the given task, thread again came to the thread pool.
The size of the thread pool depends on the total number of threads kept at reserve for execution.
The advantages of the thread pool are :
Using a thread pool, performance can be enhanced.
Using a thread pool, better system stability can occur.

Concurrency API can be developed using the class and interfaces of java.util.Concurrent package.
 There are the following classes and interfaces in java.util.Concurrent package.
Executor
FarkJoinPool
ExecutorService
ScheduledExecutorService
Future
TimeUnit(Enum)
CountDownLatch
CyclicBarrier
Semaphore
ThreadFactory
BlockingQueue
DelayQueue
Locks
Phaser

The Executor Interface provided by the package java.util.concurrent is the simple interface used to execute
 the new task. The execute() method of Executor interface is used to execute some given command. The syntax
 of the execute() method is given below.

void execute(Runnable command)

example:
import java.util.concurrent.Executor;  
import java.util.concurrent.Executors;  
import java.util.concurrent.ThreadPoolExecutor;  
import java.util.concurrent.TimeUnit;  
public class TestThread {  
   public static void main(final String[] arguments) throws InterruptedException {  
      Executor e = Executors.newCachedThreadPool();  
      e.execute(new Thread());  
      ThreadPoolExecutor pool = (ThreadPoolExecutor)e;  
      pool.shutdown();  
   }  
   static class Thread implements Runnable {  
      public void run() {  
         try {  
            Long duration = (long) (Math.random() * 5);  
            System.out.println("Running Thread!");  
            TimeUnit.SECONDS.sleep(duration);  
            System.out.println("Thread Completed");  
         } catch (InterruptedException ex) {  
            ex.printStackTrace();  
         }  
      }  
   }  
}     

The java.util.concurrent.BlockingQueue is the subinterface of Queue that supports the operations such as
 waiting for the space availability before inserting a new value or waiting for the queue to become
 non-empty before retrieving an element from it. 
example.
      
import java.util.Random;  
import java.util.concurrent.ArrayBlockingQueue;  
import java.util.concurrent.BlockingQueue;  
public class TestThread {  
   public static void main(final String[] arguments) throws InterruptedException {  
      BlockingQueue<Integer> queue = new ArrayBlockingQueue<Integer>(10);  
      Insert i = new Insert(queue);  
      Retrieve r = new Retrieve(queue);  
      new Thread(i).start();  
      new Thread(r).start();  
      Thread.sleep(2000);  
   }  
   static class Insert implements Runnable {  
      private BlockingQueue<Integer> queue;  
      public Insert(BlockingQueue queue) {  
         this.queue = queue;  
      }  
      @Override  
      public void run() {  
         Random random = new Random();  
         try {  
            int result = random.nextInt(200);  
            Thread.sleep(1000);  
            queue.put(result);  
            System.out.println("Added: " + result);  
              
            result = random.nextInt(10);  
            Thread.sleep(1000);  
            queue.put(result);  
            System.out.println("Added: " + result);  
              
            result = random.nextInt(50);  
            Thread.sleep(1000);  
            queue.put(result);  
            System.out.println("Added: " + result);  
         } catch (InterruptedException e) {  
            e.printStackTrace();  
         }  
      }      
   }  
   static class Retrieve implements Runnable {  
      private BlockingQueue<Integer> queue;  
      public Retrieve(BlockingQueue queue) {  
         this.queue = queue;  
      }        
      @Override  
      public void run() {           
         try {  
            System.out.println("Removed: " + queue.take());  
            System.out.println("Removed: " + queue.take());  
            System.out.println("Removed: " + queue.take());  
         } catch (InterruptedException e) {  
            e.printStackTrace();  
         }  
      }  
   }  
}  

The producer-consumer problem can be solved by using BlockingQueue in the following way.      
import java.util.concurrent.BlockingQueue;  
import java.util.concurrent.LinkedBlockingQueue;  
import java.util.logging.Level;  
import java.util.logging.Logger;  
public class ProducerConsumerProblem {  
    public static void main(String args[]){  
     //Creating shared object  
     BlockingQueue sharedQueue = new LinkedBlockingQueue();  
     //Creating Producer and Consumer Thread  
     Thread prod = new Thread(new Producer(sharedQueue));  
     Thread cons = new Thread(new Consumer(sharedQueue));  
     //Starting producer and Consumer thread  
     prod.start();  
     cons.start();  
    }  
   
}  
class Producer implements Runnable {  
  
    private final BlockingQueue sharedQueue;  
  
    public Producer(BlockingQueue sharedQueue) {  
        this.sharedQueue = sharedQueue;  
    }  
    @Override  
    public void run() {  
        for(int i=0; i<10; i++){  
            try {  
                System.out.println("Produced: " + i);  
                sharedQueue.put(i);  
            } catch (InterruptedException ex) {  
                Logger.getLogger(Producer.class.getName()).log(Level.SEVERE, null, ex);  
            }  
        }  
    }  
  
}  
class Consumer implements Runnable{  
  
    private final BlockingQueue sharedQueue;  
  
    public Consumer (BlockingQueue sharedQueue) {  
        this.sharedQueue = sharedQueue;  
    }  
    
    @Override  
    public void run() {  
        while(true){  
            try {  
                System.out.println("Consumed: "+ sharedQueue.take());  
            } catch (InterruptedException ex) {  
                Logger.getLogger(Consumer.class.getName()).log(Level.SEVERE, null, ex);  
            }  
        }  
    }  
}  

The Callable interface and Runnable interface both are used by the classes which wanted to execute with
 multiple threads. However, there are two main differences between the both :
A Callable <V> interface can return a result, whereas the Runnable interface cannot return any result.
A Callable <V> interface can throw a checked exception, whereas the Runnable interface cannot throw checked exception.
A Callable <V> interface cannot be used before the Java 5 whereas the Runnable interface can be used.

The Atomic action is the operation which can be performed in a single unit of a task without any
 interference of the other operations.
The Atomic action cannot be stopped in between the task. Once started it fill stop after the completio
n of the task only.
An increment operation such as a++ does not allow an atomic action.
All reads and writes operation for the primitive variable (except long and double) are the atomic operation.
All reads and writes operation for the volatile variable (including long and double) are the atomic operation.
The Atomic methods are available in java.util.Concurrent package.

The java.util.concurrent.locks.Lock interface is used as the synchronization mechanism. It works similar
 to the synchronized block. There are a few differences between the lock and synchronized block that are
 given below.

Lock interface provides the guarantee of sequence in which the waiting thread will be given the access,
 whereas the synchronized block doesn't guarantee it.
Lock interface provides the option of timeout if the lock is not granted whereas the synchronized block
 doesn't provide that.
The methods of Lock interface, i.e., Lock() and Unlock() can be called in different methods whereas single
 synchronized block must be fully contained in a single method.
 
The ExecutorService Interface is the subinterface of Executor interface and adds the features to manage
 the lifecycle. Consider the following example.      
import java.util.concurrent.ExecutorService;  
import java.util.concurrent.Executors;  
import java.util.concurrent.TimeUnit;   
public class TestThread {  
   public static void main(final String[] arguments) throws InterruptedException {  
      ExecutorService e = Executors.newSingleThreadExecutor();  
      try {  
         e.submit(new Thread());  
         System.out.println("Shutdown executor");  
         e.shutdown();  
         e.awaitTermination(5, TimeUnit.SECONDS);  
      } catch (InterruptedException ex) {  
         System.err.println("tasks interrupted");  
      } finally {  
         if (!e.isTerminated()) {  
            System.err.println("cancel non-finished tasks");  
         }  
         e.shutdownNow();  
         System.out.println("shutdown finished");  
      }  
   }  
   static class Task implements Runnable {  
        
      public void run() {  
           
         try {  
            Long duration = (long) (Math.random() * 20);  
            System.out.println("Running Task!");  
            TimeUnit.SECONDS.sleep(duration);  
         } catch (InterruptedException ex) {  
            ex.printStackTrace();  
         }  
      }  
   }         
}  

Synchronous programming: In Synchronous programming model, a thread is assigned to complete a task and hence
 thread started working on it, and it is only available for other tasks once it will end the assigned task.
Asynchronous Programming: In Asynchronous programming, one job can be completed by multiple threads and
 hence it provides maximum usability of the various threads.

Java Callable interface: In Java5 callable interface was provided by the package java.util.concurrent.
It is similar to the Runnable interface but it can return a result, and it can throw an Exception. It
also provides a run() method for execution of a thread. Java Callable can return any object as it uses
Generic.Syntax:
public interface Callable<V>

Java Future interface: Java Future interface gives the result of a concurrent process. The Callable interface returns the object of java.util.concurrent.Future.

Java Future provides following methods for implementation.

cancel(boolean mayInterruptIfRunning): It is used to cancel the execution of the assigned task.
get(): It waits for the time if execution not completed and then retrieved the result.
isCancelled(): It returns the Boolean value as it returns true if the task was canceled before the completion.
isDone(): It returns true if the job is completed successfully else returns false.
44. What is the difference between ScheduledExecutorService and ExecutorService interface?
ExecutorServcie and ScheduledExecutorService both are the interfaces of java.util.Concurrent package but scheduledExecutorService provides some additional methods to execute the Runnable and Callable tasks with the delay or every fixed time period.

45) Define FutureTask class in Java?
Java FutureTask class provides a base implementation of the Future interface. The result can only be obtained if the execution of one task is completed, and if the computation is not achieved then get method will be blocked. If the execution is completed, then it cannot be re-started and can't be canceled.

Syntax

public class FutureTask<V> extends Object implements RunnableFuture<V>

 What is the Collection framework in Java?
Collection Framework is a combination of classes and interface, which is used to store and manipulate the data in the form of objects. It provides various classes such as ArrayList, Vector, Stack, and HashSet, etc. and interfaces such as List, Queue, Set, etc. for this purpose.

2) What are the main differences between array and collection?
Array and Collection are somewhat similar regarding storing the references of objects and manipulating the data, but they differ in many ways. The main differences between the array and Collection are defined below:

Arrays are always of fixed size, i.e., a user can not increase or decrease the length of the array according to their requirement or at runtime, but In Collection, size can be changed dynamically as per need.
Arrays can only store homogeneous or similar type objects, but in Collection, heterogeneous objects can be stored.
Arrays cannot provide the ?ready-made? methods for user requirements as sorting, searching, etc. but Collection includes readymade methods to use.
3) Explain various interfaces used in Collection framework?
Collection framework implements various interfaces, Collection interface and Map interface (java.util.Map) are the mainly used interfaces of Java Collection Framework. List of interfaces of Collection Framework is given below:

1. Collection interface: Collection (java.util.Collection) is the primary interface, and every collection must implement this interface.

Syntax:

public interface Collection<E>extends Iterable  
Where <E> represents that this interface is of Generic type

2. List interface: List interface extends the Collection interface, and it is an ordered collection of objects. It contains duplicate elements. It also allows random access of elements.

Syntax:

public interface List<E> extends Collection<E>  
3. Set interface: Set (java.util.Set) interface is a collection which cannot contain duplicate elements. It can only include inherited methods of Collection interface

Syntax:

public interface Set<E> extends Collection<E>  
Queue interface: Queue (java.util.Queue) interface defines queue data structure, which stores the elements in the form FIFO (first in first out).

Syntax:

public interface Queue<E> extends Collection<E>  
4. Dequeue interface: it is a double-ended-queue. It allows the insertion and removal of elements from both ends. It implants the properties of both Stack and queue so it can perform LIFO (Last in first out) stack and FIFO (first in first out) queue, operations.

Syntax:

public interface Dequeue<E> extends Queue<E>  
5. Map interface: A Map (java.util.Map) represents a key, value pair storage of elements. Map interface does not implement the Collection interface. It can only contain a unique key but can have duplicate elements. There are two interfaces which implement Map in java that are Map interface and Sorted Map.

4) What is the difference between ArrayList and Vector?
No.	ArrayList	Vector
1)	ArrayList is not synchronized.	Vector is synchronized.
2)	ArrayList is not a legacy class.	Vector is a legacy class.
3)	ArrayList increases its size by 50% of the array size.	Vector increases its size by doubling the array size.
4)	ArrayList is not ?thread-safe? as it is not synchronized.	Vector list is ?thread-safe? as it?s every method is synchronized.
5) What is the difference between ArrayList and LinkedList?
No.	ArrayList	LinkedList
1)	ArrayList uses a dynamic array.	LinkedList uses a doubly linked list.
2)	ArrayList is not efficient for manipulation because too much is required.	LinkedList is efficient for manipulation.
3)	ArrayList is better to store and fetch data.	LinkedList is better to manipulate data.
4)	ArrayList provides random access.	LinkedList does not provide random access.
5)	ArrayList takes less memory overhead as it stores only object	LinkedList takes more memory overhead, as it stores the object as well as the address of that object.
6) What is the difference between Iterator and ListIterator?
Iterator traverses the elements in the forward direction only whereas ListIterator traverses the elements into forward and backward direction.

No.	Iterator	ListIterator
1)	The Iterator traverses the elements in the forward direction only.	ListIterator traverses the elements in backward and forward directions both.
2)	The Iterator can be used in List, Set, and Queue.	ListIterator can be used in List only.
3)	The Iterator can only perform remove operation while traversing the collection.	ListIterator can perform ?add,? ?remove,? and ?set? operation while traversing the collection.
7) What is the difference between Iterator and Enumeration?
No.	Iterator	Enumeration
1)	The Iterator can traverse legacy and non-legacy elements.	Enumeration can traverse only legacy elements.
2)	The Iterator is fail-fast.	Enumeration is not fail-fast.
3)	The Iterator is slower than Enumeration.	Enumeration is faster than Iterator.
4)	The Iterator can perform remove operation while traversing the collection.	The Enumeration can perform only traverse operation on the collection.
8) What is the difference between List and Set?
The List and Set both extend the collection interface. However, there are some differences between the both which are listed below.

The List can contain duplicate elements whereas Set includes unique items.
The List is an ordered collection which maintains the insertion order whereas Set is an unordered collection which does not preserve the insertion order.
The List interface contains a single legacy class which is Vector class whereas Set interface does not have any legacy class.
The List interface can allow n number of null values whereas Set interface only allows a single null value.

9) What is the difference between HashSet and TreeSet?
The HashSet and TreeSet, both classes, implement Set interface. The differences between the both are listed below.

HashSet maintains no order whereas TreeSet maintains ascending order.
HashSet impended by hash table whereas TreeSet implemented by a Tree structure.
HashSet performs faster than TreeSet.
HashSet is backed by HashMap whereas TreeSet is backed by TreeMap.
10) What is the difference between Set and Map?
The differences between the Set and Map are given below.

Set contains values only whereas Map contains key and values both.
Set contains unique values whereas Map can contain unique Keys with duplicate values.
Set holds a single number of null value whereas Map can include a single null key with n number of null values.
11) What is the difference between HashSet and HashMap?
The differences between the HashSet and HashMap are listed below.

HashSet contains only values whereas HashMap includes the entry (key, value). HashSet can be iterated, but HashMap needs to convert into Set to be iterated.
HashSet implements Set interface whereas HashMap implements the Map interface
HashSet cannot have any duplicate value whereas HashMap can contain duplicate values with unique keys.
HashSet contains the only single number of null value whereas HashMap can hold a single null key with n number of null values.
12) What is the difference between HashMap and TreeMap?
The differences between the HashMap and TreeMap are given below.

HashMap maintains no order, but TreeMap maintains ascending order.
HashMap is implemented by hash table whereas TreeMap is implemented by a Tree structure.
HashMap can be sorted by Key or value whereas TreeMap can be sorted by Key.
HashMap may contain a null key with multiple null values whereas TreeMap cannot hold a null key but can have multiple null values.
13) What is the difference between HashMap and Hashtable?
No.	HashMap	Hashtable
1)	HashMap is not synchronized.	Hashtable is synchronized.
2)	HashMap can contain one null key and multiple null values.	Hashtable cannot contain any null key or null value.
3)	HashMap is not ?thread-safe,? so it is useful for non-threaded applications.	Hashtable is thread-safe, and it can be shared between various threads.
4)	4) HashMap inherits the AbstractMap class	Hashtable inherits the Dictionary class.
14) What is the difference between Collection and Collections?
The differences between the Collection and Collections are given below.

The Collection is an interface whereas Collections is a class.
The Collection interface provides the standard functionality of data structure to List, Set, and Queue. However, Collections class is to sort and synchronize the collection elements.
The Collection interface provides the methods that can be used for data structure whereas Collections class provides the static methods which can be used for various operation on a collection.
15) What is the difference between Comparable and Comparator?
No.	Comparable	Comparator
1)	Comparable provides only one sort of sequence.	The Comparator provides multiple sorts of sequences.
2)	It provides one method named compareTo().	It provides one method named compare().
3)	It is found in java.lang package.	It is located in java.util package.
4)	If we implement the Comparable interface, The actual class is modified.	The actual class is not changed.
16) What do you understand by BlockingQueue?
BlockingQueue is an interface which extends the Queue interface. It provides concurrency in the operations like retrieval, insertion, deletion. While retrieval of any element, it waits for the queue to be non-empty. While storing the elements, it waits for the available space. BlockingQueue cannot contain null elements, and implementation of BlockingQueue is thread-safe.

Syntax:

public interface BlockingQueue<E> extends Queue <E>  
17) What is the advantage of Properties file?
If you change the value in the properties file, you don't need to recompile the java class. So, it makes the application easy to manage. It is used to store information which is to be changed frequently. Consider the following example.

import java.util.*;  
import java.io.*;  
public class Test {  
public static void main(String[] args)throws Exception{  
    FileReader reader=new FileReader("db.properties");  
      
    Properties p=new Properties();  
    p.load(reader);  
      
    System.out.println(p.getProperty("user"));  
    System.out.println(p.getProperty("password"));  
}  
}  

What does the hashCode() method?
The hashCode() method returns a hash code value (an integer number).

The hashCode() method returns the same integer number if two keys (by calling equals() method) are identical.

However, it is possible that two hash code numbers can have different or the same keys.

If two objects do not produce an equal result by using the equals() method, then the hashcode() method will provide the different integer result for both the objects.

19) Why we override equals() method?
The equals method is used to check whether two objects are the same or not. It needs to be overridden if we want to check the objects based on the property.

For example, Employee is a class that has 3 data members: id, name, and salary. However, we want to check the equality of employee object by the salary. Then, we need to override the equals() method.

20) How to synchronize List, Set and Map elements?
Yes, Collections class provides methods to make List, Set or Map elements as synchronized:

public static List synchronizedList(List l){}
public static Set synchronizedSet(Set s){}
public static SortedSet synchronizedSortedSet(SortedSet s){}
public static Map synchronizedMap(Map m){}
public static SortedMap synchronizedSortedMap(SortedMap m){}
21) What is the advantage of the generic collection?
There are three main advantages of using the generic collection.

If we use the generic class, we don't need typecasting.
It is type-safe and checked at compile time.
Generic confirms the stability of the code by making it bug detectable at compile time.
22) What is hash-collision in Hashtable and how it is handled in Java?
Two different keys with the same hash value are known as hash-collision. Two separate entries will be kept in a single hash bucket to avoid the collision. There are two ways to avoid hash-collision.

Separate Chaining
Open Addressing
23) What is the Dictionary class?
The Dictionary class provides the capability to store key-value pairs.

24) What is the default size of load factor in hashing based collection?
The default size of load factor is 0.75. The default capacity is computed as initial capacity * load factor. For example, 16 * 0.75 = 12. So, 12 is the default capacity of Map.

25) What do you understand by fail-fast?
The Iterator in java which immediately throws ConcurrentmodificationException, if any structural modification occurs in, is called as a Fail-fast iterator. Fail-fats iterator does not require any extra space in memory.

26) What is the difference between Array and ArrayList?
The main differences between the Array and ArrayList are given below.

SN	Array	ArrayList
1	The Array is of fixed size, means we cannot resize the array as per need.	ArrayList is not of the fixed size we can change the size dynamically.
2	Arrays are of the static type.	ArrayList is of dynamic size.
3	Arrays can store primitive data types as well as objects.	ArrayList cannot store the primitive data types it can only store the objects.
27) What is the difference between the length of an Array and size of ArrayList?
The length of an array can be obtained using the property of length whereas ArrayList does not support length property, but we can use size() method to get the number of objects in the list.

Finding the length of the array

Int [] array = new int[4];  
System.out.println("The size of the array is " + array.length);  
          
Finding the size of the ArrayList

ArrayList<String> list=new ArrayList<String>();    
list.add("ankit");    
list.add("nippun");  
System.out.println(list.size());  
          
28) How to convert ArrayList to Array and Array to ArrayList?
We can convert an Array to ArrayList by using the asList() method of Arrays class. asList() method is the static method of Arrays class and accepts the List object. Consider the following syntax:

Arrays.asList(item)  
We can convert an ArrayList to Array using toArray() method of the ArrayList class. Consider the following syntax to convert the ArrayList to the List object.

List_object.toArray(new String[List_object.size()])  
29) How to make Java ArrayList Read-Only?
We can obtain java ArrayList Read-only by calling the Collections.unmodifiableCollection() method. When we define an ArrayList as Read-only then we cannot perform any modification in the collection through  add(), remove() or set() method.

30) How to remove duplicates from ArrayList?
There are two ways to remove duplicates from the ArrayList.

Using HashSet: By using HashSet we can remove the duplicate element from the ArrayList, but it will not then preserve the insertion order.
Using LinkedHashSet: We can also maintain the insertion order by using LinkedHashSet instead of HashSet.
The Process to remove duplicate elements from ArrayList using the LinkedHashSet:

Copy all the elements of ArrayList to LinkedHashSet.
Empty the ArrayList using clear() method, which will remove all the elements from the list.
Now copy all the elements of LinkedHashset to ArrayList.
31) How to reverse ArrayList?
To reverse an ArrayList, we can use reverse() method of Collections class. Consider the following example.

import java.util.ArrayList;  
import java.util.Collection;  
import java.util.Collections;  
import java.util.Iterator;  
import java.util.List;  
public class ReverseArrayList {  
public static void main(String[] args) {  
     List list = new ArrayList<>();  
     list.add(10);  
     list.add(50);  
     list.add(30);  
     Iterator i = list.iterator();  
     System.out.println("printing the list....");  
     while(i.hasNext())  
     {  
         System.out.println(i.next());  
     }  
     Iterator i2 = list.iterator();  
     Collections.reverse(list);  
     System.out.println("printing list in reverse order....");  
     while(i2.hasNext())  
     {  
         System.out.println(i2.next());  
     }  
    }  
}  

 How to sort ArrayList in descending order?
To sort the ArrayList in descending order, we can use the reverseOrder method of Collections class. Consider the following example.

import java.util.ArrayList;  
import java.util.Collection;  
import java.util.Collections;  
import java.util.Comparator;  
import java.util.Iterator;  
import java.util.List;  
  
public class ReverseArrayList {  
public static void main(String[] args) {  
     List list = new ArrayList<>();  
     list.add(10);  
     list.add(50);  
     list.add(30);  
     list.add(60);  
     list.add(20);  
     list.add(90);  
       
     Iterator i = list.iterator();  
     System.out.println("printing the list....");  
     while(i.hasNext())  
     {  
         System.out.println(i.next());  
     }  
      
    Comparator cmp = Collections.reverseOrder();  
    Collections.sort(list,cmp);  
     System.out.println("printing list in descending order....");  
     Iterator i2 = list.iterator();  
     while(i2.hasNext())  
     {  
         System.out.println(i2.next());  
     }  
       
}  
}  

 How to synchronize ArrayList?
We can synchronize ArrayList in two ways.

Using Collections.synchronizedList() method
Using CopyOnWriteArrayList<T>
34) When to use ArrayList and LinkedList?
LinkedLists are better to use for the update operations whereas ArrayLists are better to use for the search operations.
















       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       
       

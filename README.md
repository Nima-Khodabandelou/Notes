# java_core

Core concepts of Java SE
##
- SOLID Principles (not specific to Java)

      1- Single Responsibility for Each class <-> Just one reason needed
      to change that class.

		Advantages:

			Testing –> fewer test cases for each class.
			Lower coupling –> fewer dependencies.
			Smaller and well-organized classes
		 
      2- Class shoud be Opened for Extension and Closed for Modification.
	
	   Otherwise -> modifying the existing code -> potential new bugs.
	   
	   If fixing bugs -> extend the class

      3- Liskov Substitution: if class A is a subtype of class B, one should
      be able to replace B with A without disrupting the behavior of the program.
	   
	   A popular Example:
	   
		public interface Vehicle {
			void turnOnICEngine();
			void accelerate();
		}
		public class Mustang implements Vehicle {
			private Engine engine;
			//Constructors, getters + setters
			public void turnOnICEngine() {
				engine.on();
			}
			public void accelerate() {
				engine.powerOn(5000);
			}
		}
		public class Tesla implements Vehicle {
			public void turnOnICEngine() 
				// This new Vehicle is electric -> changes the
				// program behavior!
				//-> Liskov Substitution violated!
				throw new AssertionError("Tesla doesn't have
				Internal Combustion (IC) engine!");
			}
			public void accelerate() {
				//Too much for Tesla!
			}
			// Possible Soultion -> Code another interface for
			//taking into account the non-ICEngine ones.
		}

      4- Interface Segregation: larger interfaces be splited into smaller
      ones -> More specific methods in each interface.
	   
      5- Dependency Inversion: Decoupling software modules
      -> high-level/low-level modules and details depend on abstractions.
	   
		example:
	
			public class SalesDepartment {
				public void customerSupport() {
				}
			}   
			public class WarehouseDepartment {
				public void qualityControl() {
				}
			}
			public class Manager {
				private SalesDepartment salesDepartment =
				new SalesDepartment();
				private WarehouseDepartment warehouseDepartment =
				new WarehouseDepartment();
				public void OrderInquiry() {
					salesDepartment.customerSupport();
					warehouseDepartment.qualityControl();
				}
			}

			Manager class depends on low-level modules
			-> refactor using abstraction: 

			public interface Departments {
				void department();
			}
			public class SalesDepartment implements Departments {
				@Override
				public void department() {
					customerSupport();
				}
				private void customerSupport() {}
			}
			public class WarehouseDepartment implements Departments {
				@Override
				public void department() {
					qualityControl();
				}
				public void qualityControl() {}
			}
			public class Manager {
				private List<Departments> departments;
				public Manager(List<Departments> departments) {
					this.departments = departments;
				}
				public void OrderInquiry() {
					departments.forEach(d->d.department());
				}
			}
##
- Main Java features

      Used for Desktop, Mobile, and Web application development

      Platform-independent

      Robust

      Secure

      High-level

      Multi-threaded
##    
- Java Does not support

      pointers (Handles it internally)
    
      goto
    
      operator overloading
    
      call by reference
    
      structures and unions
##
- Super keyword

       A reference variable used for refering to the immediate parent
       class object
       
       Called implicitly by the class constructor if not provided  
       
       Can refer to immediate parent class instance variable
       
       For immediate parent class method invocation
       
       To differentiate between local and instance variables in the class
       constructor
       
       Must be the first statement in constructor
##       
- Path and Classpath

       PATH: An environment variable used by the operating system to locate the
       executables

       Classpath: Java specific used to locate class files. it can be a directory,
       ZIP, JAR, etc.
## 
- Source files

      Each source Java file may have multiple classes among which only one shall
      be public.

      Source file name shall be the same as class name.
## 
- OS Architecture

      Java is neutral w.r.t to OS architecture (32 bit or 64 bit).
## 
- Interpreter/Compiler

      Just-in-time (JIT): To improve performance by compiling parts of the bytecode
                        having similar functionality, and therefore reducing
			compilation time.  

      Compiler: transforms instruction set of a Java virtual machine (JVM) to
      the instruction set of a specific CPU (Java code to Bytecode).      

      Classloader: Part of the Java Runtime Environment for loading class files.
      Three built-in classloaders:				   
		Bootstrap ClassLoader: The first classloader in native code
		(e.g. c++) which loads rt.jar file containing all core
		libraries and class files of Java SE There are various
		implementations of this Bootstrap class loader for
		various platforms.

		Extension ClassLoader: Its parent is Bootstrap classloader loads
		core extension classes to be available to all applications running
		on each platform. 

		System/Application ClassLoader: Loads files in the classpath.
##             
- Local variables

      not initialized to any default value.
## 
- Acccess modifiers

      Default: accessible within the package only.
      
      Protected: accessible by the class and sub-class of the same package, or by
      the sub-class in another packages.
      
      Public: accessible anywhere
      
      Private: accessible within the class
## 
- delete, next, main, exit or null are not keyword
##
- Final keyword

      A final class cannot be subclassed.
	
      A final method cannot be overridden.
	
      create and document a class carefully or declare it final for safety reasons.
	
      making a class final: no other programmer can improve it. can’t fix any
      problem with it --> lose extensibility
	
      If methods of class called by other methods, should consider making the
      called methods final. Otherwise, overriding them can affect the work of callers.
	
      If constructor calls other methods, should generally declare these methods final.
	
      making all methods of the class final -> can extend the class
	
      marking the class itself final -> can't extend the class
	
      can’t reassign final reference variable, But the object it refers to is mutable.
      
      ex:
	      final Cat cat = new Cat();
	      cat.setWeight(5) -> valid
	 
      class constants should be uppercase nad final, with components separated by
      underscore:
	
      static final int MAX_WIDTH = 999;
	 
      static final fileds -> initialize them	upon declaration in the static
      initializer block
	
      instance final fields -> initialize them upon declaration in the instance
      initializer block in the constructor
	
      A final argument can’t be changed inside a method
      
		public void methodWithFinalArguments(final int x) {
			x=1;
		}
##
- Immutability

      once create an object, not allowed to change the content. If try to change
      and alteration successfully done -> a new object will be created.
	
      immutable obj --> its state doesn’t change after it has been initialized.
      ex -> String class instantiated, value never changes.
	
      immutable object can’t be updated -> programs need to create a new object
      for every change of state.
	
      benefits of immutable obj:
	
		good for caching purposes <--> don’t have to worry about the
		value changes
		
		inherently thread-safe	
		
      create immutable class:
	
		Declare class as final
		
		all fields private
		
		No setter
		
		all mutable fields final
		
		Initialize all fields using constructor performing deep copy
		
		return copy of obj by cloning it rather than returning the
		actual object reference
		
		Ex:
		
		public final class FinalClassExample {
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
			public FinalClassExample(int i, String n,
			HashMap<String,String> hm){
				this.id=i;
				this.name=n;
				HashMap<String,String> tempMap=
				new HashMap<String,String>();
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
				HashMap<String, String> h1 =
				new HashMap<String,String>();
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
				System.out.println("ce id after local variable change:
				"+ce.getId());
				System.out.println("ce name after local variable change:
				"+ce.getName());
				System.out.println("ce testMap after local variable
				change: "+ce.getTestMap());		
				HashMap<String, String> hmTest = ce.getTestMap();
				hmTest.put("4", "new");		
				System.out.println("ce testMap after changing variable
				from getter methods: "+ce.getTestMap());
			}
		}
		
		output shows HashMap values didn’t change because constructor uses
		deep copy and getter function returns a clone of original object.
		
		can make changes to the FinalClassExample.java file to show what
		happens when use shallow copy and return object insetad of a copy.
		
		Make the following changes:
		
		// Getter function for mutable objects
			public HashMap<String, String> getTestMap() {
				return testMap;
			}
			//Constructor method performing shallow copy
			public FinalClassExample(int i, String n,
			HashMap<String,String> hm){
				System.out.println("Performing Shallow
				Copy for Object initialization");
				this.id=i;
				this.name=n;
				this.testMap=hm;
			}
##
- static methods/variables -> shared among all the objects of the class. 
##
- static variables stored in class area, do not need to create the object to
 access such variables.
##
- packages

      avoid the name clashes.
      
      provides easier access control.
      
      can  have the hidden classes.
      
      easier to locate the related classes.
##
- Object

      real-time entity having state and behavior.
      
      an instance of class
      
      instance variables <-> state of object
      
      methods <-> behavior of object.
      
      created using new keyword.
      
      All object references <-> initialized to null.
##
- constructor

      special type of method to initialize the state
      
      invoked when  class is instantiated,and memory allocated for object
      
      Every time an object created using new keyword, default constructor
      is called 
      
      must not have explicit return type.
      
      is not inherited.
      
      can't be final.
##
- parameterized constructor

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
##
- copy values of one object into another

      By constructor

      By assigning the values of one object into another

      By clone() method of Object class

      ex: 
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
##
- method

      exposes behavior of object

      must have a return type

      is invoked explicitly

      is not provided by the compiler in any case.

      method name may or may not be same as class name.
## 
- Type promotion in Java

      Byte -> Short -> Int 

      Char -> Int

      Int -> Long -> Float -> Double

      Ex:
      public class Test	{  
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

      ex:
      class Test {  
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

      ex:
      class Test {  
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
##
- Static variable

      gets memory only once in the class area at the time of class loading.

      makes your program more memory efficient. 

      belongs to the class rather than the object
## 
- static method

      can't use non-static data member

      can't call non-static method directly.
## 
- this and super

      cannot be used in static context as they are non-static.

      ex:
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
##
- main method

      static -> Because object not required to call the static method.

      non-static main method -> JVM have to create its object first then
      call main() -> extra memory allocation.
##
- can't override static methods.
##
- Static block

      to initialize the static data member.

      executed before the main method at the time of classloading.
## 
- Constructors

      invoked when object created -> no sense to make constructors static.
## 
- abstract methods

      -> static -> become part of the class -> can directly call it which
      is unnecessary.
## 
- can declare static variables and methods in abstract class
## 
- this

      Call to this() must be the first statement in constructor
 
      to distinguish local variable and instance variable   
 
      to invoke method of current class. If don't use this keyword, compiler
      automatically adds
 
      ex:
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

      used for constructor chaining
	
      ex:
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

      ex:
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

      ex:
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

      to pass as an argument in the method. used in the event handling
	
      ex:
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

      to pass as argument in the constructor call. useful if have to use one
      object in multiple classes
	
      ex:
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

      as statement from method -> return type of method must be class type
      
      ex: 
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
		
      is the final reference in Java.
	
      ex:
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
		
      possible but not good to refer static members <--> it is unnecessary to
      access static variables through objects
	
      to perform constructor chaining within the same class
 
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
		System.out.println("ID: "+emp.id+" Name:"+emp.name+" age:"+
		emp.age+" address: "+emp.address);  
	    }      
      }
## 
- advantages of passing this into method instead of current class object

      this is final -> cannot be assigned to any new value whereas current
      class object might not be final.
 
      this can be used in the synchronized block.
## 
- Inheritance

      code reusability -> sub-class need not to redefine method of super-class
      unless it needs to provide specific implementation.

      Runtime polymorphism -> simulate inheritance with real-time objects
      -> makes OOPs more realistic. 

      provides data hiding -> super-class can hide data from sub-class.

      makes Method overriding possible
## 
- Aggregation (has-a)

      relationship between two classes -> aggregate class contains a reference
      to the class it owns

      ex:
      public class Address {  
		...		  
      }  
      public class Emp {  
		int id;  
		String name;  
		Address address; 
		...	
      }  
## 
- composition

      When an object contains other object, if contained object cannot
      exist without existence of container object

      particular case of aggregation representing stronger relationship
      between two objects.

      Ex: class contains students. student cannot exist without a class.
## 
- pointer

      variable refers to memory address. not used in Java
## 
- super keyword

      to refer to immediate parent class.
	
      instance of subclass created -> instance of parent class created
      implicitly referred by super
	
      called in constructor implicitly by compiler if no super or this. 
	
      to refer to immediate parent class instance variable.
	
      to invoke the immediate parent class method.
	
      to invoke immediate parent class constructor.
	
      for initializing super-class variables within sub-class constructor 
	
      must be first statement in constructor
	
      for constructor chaining
	
      ex:
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
			public Employee(int age, String name, String address,
			float salary)  
			{  
				super(age,name,address);  
				this.salary = salary;  
			}  
		}  
		public class Test  
		{  
			public static void main (String args[])  
			{  
				Employee e = new Employee(22, "Mukesh",
				"Delhi", 90000);  
				System.out.println("Name: "+e.name+" Salary:
				"+e.salary+" Age: "+e.age+" Address: "+e.address);  
			}  
      }  

      Can't use this() and super() both in constructor
## 
- object cloning

      create exact copy of object -> clone() method -> java.lang.Cloneable
      interface 

      syntax -> protected Object clone() throws CloneNotSupportedException 

      clone() method saves extra processing compared to new keyword
 
      Advantage

		don't need to write lengthy and repetitive codes.

		easiest -> Just define parent class, implement Cloneable
		in it, provide clone().

		fastest way to copy array  

      Disadvantage

		have to change a lot of syntaxes

		have to implement cloneable interface while it doesn't
		have any methods. just to tell JVM.

		is protected -> have to provide our own clone() and
		indirectly call Object.clone()

		doesn't invoke constructor -> no control over object
		construction  

		If clone method in child class -> all of its superclasse
		s should define clone() or inherit. 

		supports only shallow copying -> need to override it if
		need deep cloning.
	
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
## 
- Method overloading

      multiple methods with same name but different signatures.

      ways:
		Changing number of arguments
		
		Changing data type of arguments
		
      increases readability
	
      Type promotion is method overloading
	
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
		void method(int a){  
			System.out.println("Base class method called with
			integer a = "+a);  
		}  

		void method(double d){System.out.println("Base class
		method called with double d ="+d);}  
      }    
      class Derived extends Base  
      {  
		@Override  
		void method(double d) {System.out.println("Derived class
		method called with double d ="+d);}  
      }    
      public class Main  
      {      
		public static void main(String[] args)  
		{  
			new Derived().method(10);  
		}  
      } 

- static method -> part of the class not the object -> can't be overridden
## 
- override any overloaded method

      Override <--> IS-A (super/sub relationship)
## 
- change scope of overridden method in subclass to be less
 restricitve <-> (public < default < protected < private)
## 
- modify superclass throws while override in subclass

      No exception in superclass & checked exception in subclass -> error

      No exception in superclass & unchecked exception in subclass

      exception in superclass (exc1) & exception other than exc1, exc1 child,
      and runtime exception in SubClass -> error

      exception in superclass (exc1) & child exception of exc1 in SubClass

      exception in superclass & no exception in SubClass
##   
- covariance

      how subtype is accepted when only supertype is defined
	
      covariant return type: the overriden method return type may vary in
      the same direction as the subclass ->
                       override method by changing return type if return
		       type of subclass overriding method is subclass type.
		       
      class A{  
		A get(){return this;}  
	}   
      class B1 extends A{  
		B1 get(){return this;}  
	    void message(){System.out.println("welcome to covariant return
	    type");}  
      public static void main(String args[]){  
		new B1().get().message();  
		}  
	}  
	
      ex:
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
	
      Object as return type in super -> more concrete return type in child ->
      covariant return type -> produce numbers from characters
	
      ex:
      class Base   
	{  
	    public void baseMethod(){System.out.println("BaseMethod
	    called ...");}  
	}  
      class Derived extends Base   
	{  
	    public void baseMethod() {System.out.println("Derived method
	    called ...");}  
	}  
      public class Test   
	{  
	    public static void main (String args[])  
	    {  
		    // Runtime polymorphism between Base and Derived
			// presence of baseMethod checked in Base
			//-> compiled successfully
			// at runtime, checks baseMethod overridden by
			//Derived -> if yes Derived method is called
		// reference variable b (of type Base) refers to instance
		//of Derived.
		Base b = new Derived();  
		b.baseMethod();  
	    }  
      }
##
- final

      cannot override inherited final method. 

      can't inherit final class

      constructor can never be final

      interface can never be final

      ex:	
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
	   final int i; // can be initialized only once 
	   i = 20;  
	   System.out.println(i);  
	 }  
      }  
## 
- compile-time polymorphism (static binding, early binding, or overloading)

      (object type determined/call to method resolved) at
      compile-time -> fast execution
##	
- runtime polymorphism (dynamic binding, late binding, overriding,
-  dynamic method dispatch)

      (object type determined/call to overridden method resolved) at runtime.
##
- overridden method

      called through reference variable of superclass

      determination of the method to be called is based on object being
      referred to by reference variable.

	ex: 
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

	data members cannot be overridden -> no Runtime Polymorphism by data members 

	ex:
	class Bike{  
	 int speedlimit=90;  
	}  
	class Honda3 extends Bike{  
	 int speedlimit=150;  
	public static void main(String args[]){  
	  Bike obj=new Honda3();  
	  System.out.println(obj.speedlimit);
	}  
	private, final or static method in class -> static binding.
	class Animal{  
	 void eat(){System.out.println("animal is eating...");}  
	}  
	class Dog extends Animal{  
	 void eat(){System.out.println("dog is eating...");} 
	 public static void main(String args[]){  
	  Animal a=new Dog(); //instance of Dog is also an instance of
	  Animal -> object type cannot determined by compiler because ->
			      //compiler knows only its base type
	  a.eat();  
	 }  
	}  
## 
- instanceof

	compares the instance with type
	
	ex:
		Simple1 s=new Simple1();
		System.out.println(s instanceof Simple1);//true
## 
- Abstraction

	help focus on what object does instead of how it does
##	
- encapsulation

	wraps code and data into single unit
## 
- abstract class

	can have abstract and non-abstract methods, data member, constructor,
	and even main()

	can have constructors and static methods

	can have final methods -> force subclass not to change method body 

	can never be instantiated even if it contains constructor and
	implemented methods

	can provide implementation of interface

	can extend another Java class
##  
- interface methods -> abstract by default

- static + abstract -> not allowed
## 
- Marker interface

	interface with no data member and member functions -> Serializable,
	Cloneable.
##
- Interface

	can't provide implementation of abstract class.
	
	can extend another interface
	
	Members of interface are public by default
	
	object reference can be cast to interface reference when it
	implements referenced interface
	
	ex:
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
##
- Encapsulation

	read-only  class -> all fields private. only getter returning private
	property of class to main method 

	write-only class -> all fields private. only setter setting value
	passed from main to private fields
##
- package

	group of similar type of classes, interfaces, and sub-packages.

	access protection

	removes naming collision
##
- try block followed by either catch OR finally block
##
- Exceptions

	Checked Exception

		checked at compile-time. SQLException, ClassNotFoundException, etc.

	Unchecked Exception

		handled at runtime. ArithmaticException, NullPointerException,
		ArrayIndexOutOfBoundsException, etc.

	Error: not recoverable -> cause program to exit. OutOfMemoryError,
	AssertionError, etc.

	advantage of exception handling:  maintain normal flow of application.
##
- throw -> to throw exception

- throws -> to declare possible exceptions that may occure in method
##
- Hierarchy of Java Exception classes

	Throwable -> Exception, Error
	
	Exception -> IOException, SQLException, ClassNotFoundException,
	RuntimeException
	
	RuntimeException -> ArithmeticException, NullPointerException,
	NumberFormatException, IndexOutOfBoundsException
						
	IndexOutOfBoundsException -> ArrayIndexOutOfBoundsException,
	StringIndexOutOfBoundsException
	
	Error -> StackOverflowError, VirtualMachineError, OutOfMemoryError	
##	
- Common exception Scenarios

	divide number by zero -> ArithmeticException.
	
	performing operation on null variable -> NullPointerException	
	
	variable formatting mismatched -> NumberFormatException
	
	array size exceed -> ArrayIndexOutOfBoundsException
##	
- Exception Propagation

	[thrown from top -> not caught -> drops down previous]
	--> continues until caught or reach the very bottom of call stack
	
	Unchecked -> propagated by default
	
	ex: 
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
	
	ex:
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
## 
- Nested try block

	[sub-block -> one error & entire block -> another error]
	-> nested exception
## 
- Finally:

	executes after try-catch

	not executes if program exits
##
- custom exceptions: extends Exception

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
	class MyCustomException extends Exception { } 

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
##
- One can not throw basic data type from a block

	ex:
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
	
	ex: // throw a custom exception class from try block and catch
	//it in catch block
	class Calculation extends Exception  // class type is throwable
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
##
- String pool

	space reserved in heap used to store strings
	
 	create string literal -> JVM checks string pool ->
	
		If exists -> a reference returns
		
		If not    ->  new string instance creates 
	ex:													
	class Testimmutablestring{  
	 public static void main(String args[]){  
	   String s="Sachin";  
	   s.concat(" Tendulkar"); 
	   System.out.println(s); 
	 }  
	} 
##
- create string object

	String Literal
	
		String s ="welcome";
		
		String s2="Welcome";//It doesn't create a new instance
		
	new keyword
	
		//creates two objects and one reference variable
		String s=new String("Welcome");
		
		
		new object in heap refered by s,
		
		literal object "Welcome" in string pool
		
		The ref variable s
		
	ex:
	public class Test   
	{
	  public static void main (String args[])  
	  {  
	      String a = new String("Sharma is a good player");  
	      String b = "Sharma is a good player";  
	      if(a == b) // == -> references of two objects are equal or not
	      {  
		  System.out.println("a == b");  
	      }  
	      if(a.equals(b)) // checks for the content 
	      {  
		  System.out.println("a equals b");  
		  }	  
	  }  
	}
	
	ex:
	public class Test   
	{  
	    public static void main (String args[])  
	    {  
		String s1 = "Sharma is a good player";  
		String s2 = new String("Sharma is a good player");  
		 // returns object reference from string
		 //pool -> s2 changes to reference of s1
		s2 = s2.intern();
		System.out.println(s1 ==s2);  
	    }  
	}  
##
- String disadvantages compare to StringBuffer

	String  immutable
	
	String  slow creates a new instance on concatThe 
	
	String  overrides  equals()  
##
- StringBuffer

	synchronized -> thread safe -> two StringBuffer methods
	can't be called simultaneously

	less efficient than StringBuilder.	
##
- immutable class and all its members are final
##
- toString(): returns string representation of object ->
-  overriding -> desired output
##
- String is in string pool until garbage collection -> not good
-  for stornjng password -> CharArray() is better and can be set to blank 
##
- java.util.regex

	MatchResult Interface
	
	Matcher class
	
	Pattern class
	
	PatternSyntaxException class
##
- Metacharacters

	^, $, ., *, +, etc. <- not regular characters fro regex
	engine -> use backslash to treat them ordinary.
##
- Nested classes

	can access all members of outer class including private
	->  used for readability and maintainability
	
	static nested class
	
	non-static nested class (inner-class)
	
	disadvantages
	
		Inner classes increase total number of classes
		and workload of JVM less support by IDEs to inner class
##
- inner class

	Member Inner Class
	
		created within class and outside method.
		
	Anonymous Inner Class
	
		created for implementing an interface or extending class.
		
		name is decided by compiler
		
	Local Inner Class
	
		created within the method.
		
		local variable must be constant to access it in local
		inner class
		
	ex:
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
##
- nested interface

	interface within class
	public if declared inside interface
	any access modifier if declared within class
	static

	ex:
	interface Showable{  
	  void show();  
	  interface Message{  // cannot be accessed directly
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
## 
- class inside interface -> static nested class by compiler
##
- Garbage Collection

	removing unused objects from memory

	gc() to garbage collect -> depends on JVM whether to perform

	ex:
	public class TestGarbage1{  
	 public void finalize(){System.out.println("object is
	 garbage collected");}  
	 public static void main(String args[]){  
	  TestGarbage1 s1=new TestGarbage1();  
	  TestGarbage1 s2=new TestGarbage1();  
	  s1=null;  
	  s2=null;  
	  System.gc();  
	 }  
	}  
##
- unreferencing an object by

	nulling the reference
	
		Employee e=new Employee(); -> e=null; 
		
	assigning reference to another
	
		Employee e1=new Employee();  
		Employee e2=new Employee();  
		e1=e2;//e1 available for garbage collection
		
	anonymous object -> new Employee(); 
##
- An unreferenced object can be referenced again
##
- Java Runtime class

	-> to execute process, invoke GC, get total and free memory, ...

	only one instance of Runtime class

	Runtime.getRuntime() returns singleton instance of Runtime class.

	ex:
	public class Runtime1{  
	 public static void main(String args[])throws Exception{  
	  Runtime.getRuntime().exec("notepad");//will open a new notepad  
	 }  
	}  
##
- hierarchy of InputStream and OutputStream
	
	OutputStream -> FileOutputStream, ByteArrayOutputStream,
	                FilterOutputStream, PipedOutputStream
			ObjectOutputStream,
			FilterOutputStream -> DataOutputStream,
			BufferedOutputStream, PrintStream

	InputStream -> FileInputStream, ByteArrayInputStream,
	               FilterInputStream, PipedInputStream
		       ObjectInputStream

	FilterInputStream -> DataInputStream, BufferedInputStream,
	                     PushBackInputStream

	stream: sequence of data composed of bytes from source to destination

	three automatic streams:

		System.out: standard output 

		System.in: standard input 

		System.err: standard error

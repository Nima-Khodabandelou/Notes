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
	   
	   ex1:
	   
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
				accelValue=5000;
				engine.powerOn(accelValue);
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
				//Too much acceleration for Tesla!
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
				public void customerSupport() {}
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

      Secure

      High-level

      Multi-threaded
      
      Robust <- Memory Efficient and Multi-Threaded
      
##    
- Java Does not support

      pointers (Handles it internally)
    
      goto
    
      operator overloading
    
      call by reference
    
      structures and unions

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
- Inheritance

      code reusability -> sub-class need not to redefine method of super-class
      unless it needs to provide specific implementation.

      Runtime polymorphism -> simulate inheritance with real-time objects
      -> makes OOPs more realistic. 

      provides data hiding -> super-class can hide data from sub-class.

      makes Method overriding possible
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
      
      invoked when class instantiated, obj created, and memory
       allocated for object -> so no sense to make constructors static
      
      Every time an object created using new keyword, default constructor
      is called 
      
      must not have explicit return type.
      
      is not inherited.
      
      can't be final           
##	  
- method

      exposes behavior of object

      must have a return type

      is invoked explicitly

      is not provided by the compiler in any case.

      method name may or may not be same as class name      
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

      once create an object -> not allowed to change the content.
	  If try to change and alteration successfully done -> a
	  new object will be created.
	
      immutable obj -> its state doesn’t change after it has been initialized.
      ex: String class instantiated -> value never changes.
	
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
		
		public final class DeepOrShallowCopy
		{
			private final int id;	
			private final String name;	
			private final HashMap<String,String> hashMap;	
			public int getId()
			{
				return id;
			}
			
			public String getName()
			{
				return name;
			}
			
			public HashMap<String, String> getterForMutableObjects()
			{
				return (HashMap<String, String>) hashMap.clone();
			}
			
			//deep copy	
			public DeepOrShallowCopy(int i, String n,
			HashMap<String,String> hMap)
			{
				
				this.id=i;
				this.name=n;
				
				HashMap<String,String> hashMap=
				new HashMap<String,String>();
				
				String key;
				Iterator<String> it = hMap.keySet().iterator();
				
				while(it.hasNext())
				{
					key=it.next();
					hashMap.put(key, hMap.get(key));
				}
				
				this.hashMap=hashMap;
				
			}
			// Test the immutable class
			public static void main(String[] args)
			{
				HashMap<String, String> hashMapString1 =
				new HashMap<String,String>();
				
				hashMapString1.put("1", "first");
				hashMapString1.put("2", "second");
				
				String sampleString = "original";		
				int sampleInteger=10;		
				
				DeepOrShallowCopy deepOrShallowCopy =
     				new DeepOrShallowCopy(sampleInteger,sampleString,hashMapString1);
					
				System.out.println("deepOrShallowCopy id: "+
				 deepOrShallowCopy.getId());
				System.out.println("deepOrShallowCopy name: "+
				 deepOrShallowCopy.getName());
				System.out.println("deepOrShallowCopy hashMap: "+
				 deepOrShallowCopy.getterForMutableObjects());
				
				sampleInteger=20;
				sampleString="modified";
				hashMapString1.put("3", "third");
				
				System.out.println("deepOrShallowCopy id after local variable change:
				"+deepOrShallowCopy.getId());
				
				System.out.println("deepOrShallowCopy name after local variable change:
				"+deepOrShallowCopy.getName());
				
				System.out.println("deepOrShallowCopy hashMap after local variable
				change: "+deepOrShallowCopy.getterForMutableObjects());
				
				HashMap<String, String> hmTest =
    				deepOrShallowCopy.getterForMutableObjects();
					
				hmTest.put("4", "new");		
				System.out.println("deepOrShallowCopy hashMap after changing variable
				from getter methods: "+deepOrShallowCopy.getterForMutableObjects());
			}
		}
		
		deep copy -> getter function returns a clone of original object ->
		             HashMap values didn’t change 
		
		shallow copy:
		
			public HashMap<String, String> getterForMutableObjects()
			{
				return hashMap;
			}
			public DeepOrShallowCopy(int i, String n,
			HashMap<String,String> hMap)
			{
				System.out.println("Performing Shallow
				 Copy for Object initialization");
				 
				this.id=i;
				this.name=n;
				this.hashMap=hashMap;
			}
##
- static 

 static methods/variables -> shared among all the objects of the class. 

 static variables

  stored in class area, do not need to create the object to
  access such variables.

  gets memory only once in the class area at the time of class loading.

  makes your program more memory efficient. 

  belongs to the class rather than the object
 
 static method

  can't use non-static data member

  can't call non-static method directly
  can't override static method
  
 Static block

  to initialize the static data member.

  executed before the main method at the time of classloading. 
## 
- Type promotion in Java

      Byte -> Short -> Int 

      Char -> Int

      Int -> Long -> Float -> Double

      Ex:
      public class TestClass	{  
	    TestClass(int a, int b)  
	    {  
		System.out.println("a = "+a+" b = "+b);  
	    }  
	    TestClass(int a, float b)  
	    {  
		System.out.println("a = "+a+" b = "+b);  
	    }  
	    public static void main (String args[])  
	    {  
		byte a = 10;   
		byte b = 15;  
		TestClass testClass = new TestClass(a,b);  
	    }  
      }

      ex:
      class TestClass
	  {  
	    int i;   
	  }  
	  
	  public class Main   
	  {  
	    public static void main (String args[])   
	    {  
		TestClass testClass = new TestClass();   
		System.out.println(testClass.i);  
	    }  
      }  

      ex:
      class TestClass
	  {  
	    int test_a, test_b;  
	    TestClass(int a, int b)   
	    {  
	    test_a = a;   
	    test_b = b;   
	    }  
	    public static void main (String args[])   
	    {  
		TestClass testClass = new TestClass();   
		System.out.println(testClass.test_a+" "+testClass.test_b);  
	    }  
      } 


## 
- this and super

      cannot be used in static context as they are non-static. 

      Can't use this() and super() both in constructor
	  
      this:	  
	   
       possible but not good to refer static members <--> it is unnecessary to
        access static variables through objects
	
       to perform constructor chaining within the same class
	  
       to pass as an argument in the method. used in the event handling 

       must be the first statement in constructor

       to pass as argument in the constructor call. useful if have to use one
       object in multiple classes
	  
       as statement from method -> return type of method must be class type
 
       to distinguish local variable and instance variable   
 
       to invoke method of current class. If don't use 'this' keyword, compiler
       automatically adds
	  
       advantages of passing this into method instead of current class object

         this is final -> cannot be assigned to any new value whereas current
         class object might not be final.
 
         this can be used in the synchronized block.
		 
       is the final reference in Java

      super:

        to refer to immediate parent class obj
	
	to refer to immediate parent class instance variable
	
        to invoke the immediate parent class method.
	
        to invoke immediate parent class constructor.	
	
        instance of subclass created -> instance of parent class created
        implicitly referred by super   
	
        for initializing super-class variables within sub-class constructor 
	
        must be first statement in constructor
	
        for constructor chaining
		
        Called implicitly by the class constructor if not provided 
       
        To differentiate between local and instance variables in class
        constructor		
		
      ex:
      class Employee
	  {  
	   int number;  
	   String name;  
	   static String company ="ITS";
       
	   Employee(int r,String n)
	   {  
		number = r;  
		name = n;  
	   } 
	   
	   void show (){System.out.println(number+" "+name+" "+company);} 
	   
	   public static void main(String args[])
	   {  
		Employee s1 = new Employee(111,"Karan");  
		Employee s2 = new Employee(222,"Aryan");     
		s1.show();  
		s2.show();  
	   }  
      } 		
	
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
			
			public Employee(int age, String name,
                			String address, float salary)  
			{  
				super(age,name,address);  
				this.salary = salary;  
			}  
	  }  
	  public class TestClass  
	  {  
			public static void main (String args[])  
			{  
				Employee e = new Employee(35, "Sina",
				                   "Karaj", 150000);  
				System.out.println("Name: "+e.name+" Salary:
				"+e.salary+" Age: "+e.age+" Address: "+e.address);  
			}  
      }      
	  
      ex:
      class A{  
		void m(){System.out.println("hello m");}  
		void n(){  
			System.out.println("hello n");  
			//m();//same as this.m()  
			this.m();  
		}  
      }  

      class TestThis{  
		public static void main(String args[]){  
		A a=new A();  
		a.n();  
      }}      
	
      ex:
      class A{  
		A(){System.out.println("hello a");}  
		A(int x){  
		this();  
		System.out.println(x);  
		}  
	}  
      class TestThis{  
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
      class TestThis{  
		public static void main(String args[]){  
		A a=new A();  
      }}  

      ex:
      class Employee{  
		int number;  
		String name,course;  
		float fee;  
		Employee(int number,String name,String course){  
			this.number=number;  
			this.name=name;  
			this.course=course;  
		}  		
		Employee(int number,String name,String course,float fee){  
			this(number,name,course);//reusing constructor  
			this.fee=fee;  
		}  
		void show(){System.out.println(number+" "+name+" "+course+" "+fee);}  
      }  
      class TestThis
	  {  
		public static void main(String args[])
		{  
			Employee s1=new Employee(111,"ankit","java");  
			Employee s2=new Employee(112,"sumit","java",6000f);  
			s1.show();  
			s2.show();  
        }
	  }     
	
      ex:
      class S
	  {  
		void m(S obj)
		{  
		  System.out.println("method is invoked");  
		}  
		void p()
		{  
		  m(this);  
		}  
		public static void main(String args[])
		{  
		  S s = new S();  
		  s.p();  
		}  
      }       
	
      ex:
      class B
	  {  
		  A obj;  
		  B(A obj)
		  {  
			this.obj=obj;  
		  }  
		  void show()
		  {  
			System.out.println(obj.data);
		  }  
      }  	  
      class A
	  {  
		  int data=10;  
		  A()
		  {  
		   B b=new B(this);  
		   b.show();  
		  }  
		  public static void main(String args[])
		  {  
		   A a=new A();  
		  }  
      }       
      
      ex: 
      class A{  
		void m()
		{  
		System.out.println(this);  
		}  
		public static void main(String args[])
		{  
			A obj=new A();  
			System.out.println(obj); 
			obj.m();  
		}  
      }      
	
      ex:
      public class TestClass  
	{  
		public TestClass()  
		{  
			this = null;   
			System.out.println("TestClass class constructor called");  
		}  
		public static void main (String args[])  
		{  
			TestClass t = new TestClass();  
		}  
      }       
 
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
		  Employee e = new Employee(105, 22, "Vikas", "Delhi");  
		  System.out.println("ID: "+emp.id+" Name:"+e.name+" age:"+
		  e.age+" address: "+e.address);  
	    }      
      }
	  
##
- main method

      static -> Because object not required to call the static method.

      non-static main method -> JVM have to create its object first then
      call main() -> extra memory allocation
## 
- abstract

      method -> static -> become part of the class -> can directly call it which
      is unnecessary.
      
      class -> can declare static variables and methods
##
- copy values of one object into another

      By constructor

      By assigning the values of one object into another

      By clone() method of Object class

      ex: 
      class Employee{  
	    int id;  
	    String name; 
		
	    Employee(int i,String n)
		{  
	    id = i;  
	    name = n;  
	    }  
		
	    Employee(Employee s)
		{  
	    id = s.id;  
	    name =s.name;  
	    }  
		
	    void show(){System.out.println(id+" "+name);}   
		
	    public static void main(String args[])
		{  
			Employee s1 = new Employee(111,"Karan");  
			Employee s2 = new Employee(s1);
			
			s1.show();  
			s2.show();  
	    }  
      }  
## 
- object cloning <--> shallow copy

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
      class Employee implements Cloneable{  
			int number;  
			String name;  

			Employee(int number,String name){  
			this.number=number;  
			this.name=name;  
		}  
		public Object clone()throws CloneNotSupportedException{  
			return super.clone();  
      }  
      public static void main(String args[]){  
			try{  
				Employee s1=new Employee(101,"amit");  

				Employee s2=(Employee)s1.clone();  

				System.out.println(s1.number+" "+s1.name);  
				System.out.println(s2.number+" "+s2.name);  

			}catch(CloneNotSupportedException c){}  

			}  
      }      
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

      Ex: class contains Employees. Employee cannot exist without a class.
## 
- pointer

      variable refers to memory address. not used in Java

## 
- Method overloading

      multiple methods with same name but different signatures.

      ways:
		Changing number of arguments
		
		Changing data type of arguments
		
      increases readability
	
      Type promotion is method overloading
	
      ex:
      class OverloadingCalculation1
	  {  
		void sum(int a,long b){System.out.println(a+b);} 
	  
		void sum(int a,int b,int c){System.out.println(a+b+c);} 
	  
		  public static void main(String args[])
		  {  
			  OverloadingCalculation1 obj=
			      new OverloadingCalculation1();  
			  obj.sum(20,20);  
			  obj.sum(20,20,20);  
		  }  
      } 

      ex:
      class OverloadingCalculation{
		  
		  void sum(int a,long b)
		  {
			  System.out.println("a method invoked");
		  }    
		  void sum(long a,int b)
		  {
			  System.out.println("b method invoked");
		  }    

		  public static void main(String args[])
		  {    
		  OverloadingCalculation obj=new OverloadingCalculation();    
		  obj.sum(20,20);//now ambiguity    
		  }    
      }

      ex:
      class Base  
      {  
		void method(int a)
		{  
			System.out.println("Base class method called with
			integer a = "+a);  
		}  

		void method(double d)
		{
			System.out.println("Base class
		    method called with double d ="+d);
		}  
      }   
	  
      class Derived extends Base  
      {  
		@Override  
		void method(double d)
		{
			System.out.println("Derived class
		    method called with double d ="+d);
		}  
      }    
      public class Main  
      {      
		public static void main(String[] args)  
		{  
			new Derived().method(10);  
		}  
      } 

      static method -> part of the class not the object -> can't be overridden
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
		       
      class A
	  {  
		A get(){return this;}  
	  }   
      class B extends A
	  {
		  
		B get(){return this;} 

		void message()
		{
			System.out.println("welcome to covariant return
			type");
		}  
		public static void main(String args[])
		{  
		    new B().get().message();  
		}
	  
	  }  
	
      ex:
      public class Producer
	  {
	    public Object produce(String input)
		{
		Object result = input.toLowerCase();
		return result;
	    }
      }
      public class IntegerProducer extends Producer
	  {
	    @Override
	    public Integer produce(String input)
		{
		return Integer.parseInt(input);
	    }
      }
	
      Object as return type in super -> more concrete return type in child ->
      covariant return type -> produce numbers from characters
	
      ex:
		class Base   
		{  
			public void baseMethod()
			{
				System.out.println("BaseMethod
			    called ...");
			}  
		}  
		class Derived extends Base   
		{  
			public void baseMethod() {System.out.println("Derived method
			called ...");}  
		}  
		public class TestClass   
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
		class Bike
		{  
			final int speedlimit;
			
			Bike()
			{  
				speedlimit=70;  
				System.out.println(speedlimit);  
			}
			
			public static void main(String args[])
			{  
			  new Bike();  
			}  
		}
	
      ex:
      class Main
	  {  
	   public static void main(String args[]){  
	    final int i;  
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
	class Bike
	{  
	  void run()
	  {
		  System.out.println("running");
	  }  
	}  
	class Splendor extends Bike
	{  
	  void run()
	  {
		  System.out.println("running safely with 60km");
	  }  
	  public static void main(String args[])
	  {  
	    Bike b = new Splendor();//upcasting  
	    b.run();  
	  }  
	}

	data members cannot be overridden -> no Runtime Polymorphism by data members 

	ex:
	class Bike
	{  
	 int speedlimit=90;  
	}  
	class Honda3 extends Bike
	{  
	 int speedlimit=150;  
	 public static void main(String args[])
	 {  
	  Bike obj=new Honda3();  
	  System.out.println(obj.speedlimit);
	}
	
	private, final or static method in class -> static binding.
	
	class Animal
	{  
	 void eat()
	 {
		 System.out.println("animal is eating...");
	 }  
	}  
	class Dog extends Animal
	{  
	 void eat()
	 {
		 System.out.println("dog is eating...");
	 } 
	 public static void main(String args[])
	 {  
	  Animal a=new Dog(); //instance of Dog is also an instance of
	  //Animal -> object type cannot determined by compiler because ->
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
	abstract class Bike
	{  
		Bike()
		{
			System.out.println("bike is created");
		}  
		
		abstract void run();
		
		void changeGear()
		{
			System.out.println("gear changed");
		}  
	}  
	class Honda extends Bike
	{  
		void run()
		{
			System.out.println("running safely..");
		}  
	}  
	class TestAbstraction
	{  
		public static void main(String args[])
		{  
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
	
	abstract class B implements A
	{  
		public void c(){System.out.println("I am c");}  
	}   
	
	class M extends B
	{  
		public void a(){System.out.println("I am a");}  
		public void b(){System.out.println("I am b");}  
		public void d(){System.out.println("I am d");}  
	} 
	
	class TestClass
	{  
		public static void main(String args[])
		{  
			A a=new M();  
			a.a();  
			a.b();  
			a.c();  
			a.d();  
		}
	} 

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
	class TestExceptionPropagation
	{  
	
	  void m()
	  {  
	    int data=50/0;  
	  }  
	  
	  void n()
	  {  
	    m();  
	  }  
	  
	  void p()
	  {  
	   try{  
	    n();  
	   }catch(Exception e){System.out.println("exception handled");}  
	  }  
	  
	  public static void main(String args[])
	  {  
	   TestExceptionPropagation obj=new TestExceptionPropagation();  
	   obj.p();  
	   System.out.println("normal flow...");  
	  }  
	}  
	
	ex:
	class TestExceptionPropagation
	{  
	
	  void m()
	  {  
	    throw new java.io.IOException("device error");//checked exception  
	  }  
	  
	  void n(){  
	    m();  
	  }  
	  
	  void p()
	  {  
	   try
	   {  
	    n();  
	   }
	   catch(Exception e)
	   {
		   System.out.println("exception handeled");
	   }  
	  } 
	  
	  public static void main(String args[])
	  {  
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
	
	public class TestCustomException  
	{  
	    static void validate (int age) throws InvalidAgeException
		{    
	       if(age < 18)
		   {  
		   throw new InvalidAgeException("age is not valid to vote");    
	       }  
	       else
		   {   
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

	public class TestCustomException  
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
	    public static void main(String []args)
		{  
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
	
	public class Main
	{  
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
			try
			{  
			System.out.println("a(): Main called");  
			b();  
			}
			catch(Exception e)  
			{  
				System.out.println("Exception is caught");  
			} 
		
	    }  
		
	    void b() throws Exception  
	    {  
			 try
			 {  
			 System.out.println("b(): Main called");  
			 c();  
			 }
			 catch(Exception e)
			 {  
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
				}
				catch(Exception e)
				{  
					a = a - 10;  
				}  
			}
			catch(Exception e)  
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
		
		If not ->  new string instance creates 
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
	public class TestClass   
	{
	  public static void main (String args[])  
	  {  
	      String a = new String("Nima is a good player");  
	      String b = "Nima is a good player";  
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
	public class TestClass   
	{  
	    public static void main (String args[])  
	    {  
		String s1 = "Nima is a good player";  
		String s2 = new String("Nima is a good player");  
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
	class TestNestedInterface1 implements Showable.Message
	{  
	 public void msg(){System.out.println("Hello nested interface");}  

	 public static void main(String args[])
	 {  
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
	public class TestGarbage
	{  
	 public void finalize()
	 {
		 System.out.println("object is
		 garbage collected");
	 }  
	 
	 public static void main(String args[])
	 {  
		TestGarbage s1=new TestGarbage();  
		TestGarbage s2=new TestGarbage();  
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


##
Reader/Writer class hierarchy  character-oriented,
InputStream/OutputStream class hierarchy is byte-oriented.
##
ByteStream:  input-output of 8-bit 

CharacterStream: input/output for 16-bit
 
Important ByteStream class: FileInputStream and FileOutputStream.
Important CharacterStream class:  FileReader and FileWriter.

ByteStream : InputStream classes and OutputStream

CharacterStream : Reader classes and Writer classes.

reading streams of characters -> FileReader
   
    
##
BufferedOutputStream
 internally uses buffer to store data.
 more efficiency than writing data directly into stream.
 
BufferedInputStream
 read information from stream
##
FilePermission: alter permissions of a directory or file related to a path. -> two path types:
 all subdirectories and files 
 all directory and files within directory excluding subdirectories.
  
##
FilterStream: filters read data, adds line numbers,...
##
I/O filter:
 reads one stream and writes to another,
 usually altering data


##
take input from console:
 BufferedReader (efficient): use InputStreamReader to take input from console -> pass input to BufferedReader.
	

 Scanner class:
	 breaks input into tokens 
	 provides many methods to read
	 parse various primitive values.
	 widely used with regex
##    
Using Console class:
 read console input, texts, passwords (not be displayed to user).
     
##
Serialization

 writing state of object into byte stream
 used in Hibernate, RMI, JPA, EJB and JMS
 used to travel object's state on network (known as marshaling).

 to save state to storage for later restoration

 Serializable interface -> to serialize (super-)class ->
 to prevent  child class serialization ->
 implement writeObject()/readObject() along with throw NotSerializableException in subclass. 
 
  ex:
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
	public class TestClass   
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

##
Deserialization:
 
	class Depersist
	{  
	 public static void main(String args[])throws Exception
	 {  
		
	  ObjectInputStream in=new ObjectInputStream(new FileInputStream("f.txt"));  
	  Employee s=(Employee)in.readObject();  
	  System.out.println(s.id+" "+s.name);  
	  
	  in.close();  
	 }  
	} 
	
##
transient data member can not be serialized
##
Externalizable interface: write state of object into byte stream in compressed format


	Serializable -> marker interface -> no methods
                    No class constructor is called
					better performance
	
	Externalizable: easy to implement
                    performance cost
					must call public default constructor
					contains two methods -> writeExternal and readExternal

##
Socket programming
 socket: endpoint for communications between machines -> connection mechanism: TCP
 communication between applications running on different JRE.
 connection-oriented -> Socket and ServerSocket classes
 connectionless -> DatagramSocket
 
	client needs:
		server IP address
		port number

 steps for TCP connection:
  server -> ServerSocket instantiation -> port number
 
 server -> accept() method -> wait until client attempts to connect 

 client creats socket 

 connection established -> socket object for client 

 server uses accept() to return a reference to new socket 


	public class MyServer {  
		public static void main(String[] args){  
		try
		{  
			ServerSocket ss=new ServerSocket(6666);
			
			Socket s=ss.accept();//establishes connection
			
			DataInputStream dis=new DataInputStream(s.getInputStream()); 
			
			String  str=(String)dis.readUTF(); 
			
			System.out.println("message= "+str); 
			
			ss.close();  
			
		}
		catch(Exception e)
		{
			System.out.println(e);
		}  
		}  
	}  
  
	public class MyClient {  
		public static void main(String[] args) {  
			try
			{    
				Socket s=new Socket("localhost",6666);  
				DataOutputStream dout=new DataOutputStream(s.getOutputStream());  
				dout.writeUTF("Hello Server");  
				dout.flush();  
				dout.close();  
				s.close();  
			}
			catch(Exception e)
			{
				System.out.println(e);
			}  
		}  
	}  

##
Reflection
 examining/ modifying runtime behavior of class 
 
##
java.lang.Class:
 get metadata of class at runtime
 change runtime behavior
 instantiate:
  forName() -> load class dynamically <- if know fully qualified name of class (not for primitive types)
 
  getClass() -> returns instance of java.lang.Class <- if know type (also for primitives)
  
  .class -> If no instance but type available -> append ".class" to name of type (also for primitives)


	class Simple
	{ 
	
	 public Simple()  
	 {  
	   System.out.println("Constructor of Simple class is invoked");  
	 } 
	 
	 void message()
	 {
		 System.out.println("Hello Java");
	 }    
	} 
	
	class TestClass{    
	 public static void main(String args[])
	 {    
	  try
	  {    
	  Class c=Class.forName("Simple");    
	  Simple s=(Simple)c.newInstance();    
	  s.message();    
	  }
	  catch(Exception e)
	  {System.out.println(e);
	  }    
	 }    
	}
    
##
newInstance():
 invoke constructor at runtime. 
##
javap:
 disassembles class file -> gives info about fields/constructors/ methods

(java.lang.Class + java.lang.reflect.Method) -> change class runtime behaviour
 -> access private method from outside <-
	1) setAccessible(boolean status) throws SecurityException
	  
	2) invoke(Object method, Object... args) throws IllegalAccessException,
					  IllegalArgumentException, InvocationTargetException
	1) getDeclaredMethod(String name,Class[] parameterTypes)throws NoSuchMethodException,
	   SecurityException
ex:
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
ex:
class A{  
	private void cube(int n)
	{
		System.out.println(n*n*n);
	}  
}  

class M{  
	public static void main(String args[])throws Exception
	{  
		Class c=A.class;  
		Object obj=c.newInstance();  
		Method m=c.getDeclaredMethod("cube",new Class[]{int.class});  
		
		m.setAccessible(true);  
		m.invoke(obj,4);  
	}
}  

##
access private constructor -> getDeclaredConstructor()

ex:  

class Vehicle   
{     
	private Integer vId;  
	private String vName;  
	private Vehicle()  
	{} 
	
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
##
Wrapper classes

  conversion of objects to primitives (unboxing) and primitives to objects (autoboxing)

##
Unboxing and autoboxing -> automatic in Java
 valueOf()/xxxValue() for manual conversion

public class TestClass  
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
##
native method implemented in another language
##
strictfp: get same floating-point arithmetic result on all platforms
##
System class
 cannot be instantiated.
 used for
	Standard input
	Error output streams
	Standard output
	utility method to copy the portion of an array
	utilities to load files and libraries
	
 fields:
	 static printstream err,
	 static inputstream in,
	 standard output stream.
##
Singleton class:
 instantiates only once
 make by
  private constructor
  static getInstance

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
      
##
Locale:
 
public class LocaleExample
{  
	public static void main(String[] args)
	{  
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

ResourceBundle.getBundle -> specific locale 
##
JavaBean:
 reusable software component
 encapsulates many objects into one in order to access it from multiple
  places. 
 easy maintenance. 
ex:
  
public class Employee implements java.io.Serializable
{  
	private int id;  
	private String name;
	
	public Employee(){}  
	
	public void setId(int id)
	{
		this.id=id;
	}  
	public int getId()
	{
		return id;
	}  
	public void setName(String name)
	{
		this.name=name;
	}  
	public String getName()
	{
		return name;
	}  
} 
##
RMI (Remote Method Invocation)
 for distributed application
 allows object -> invoke methods on object in another JVM by stub (for client side) and skeleton
 stub: for client side
       outgoing requests are routed through it
       tasks:
		initiates connection
		writes and transmits (marshals) parameters
		waits for result.
		reads (unmarshals) result
		returns result to caller

 skeleton: gateway for server side
        incoming requests routed through it 
       tasks:
		reads parameter for remote method
		invokes method on actual remote object
		writes and transmits (marshals) result to caller

	RMI in programs:
		Create remote interface.
		Provide implementation of remote interface
		Compile implementation class and create stub and skeleton
		 using rmic
		Start registry service by rmiregistry
		Create and start remote application
		Create and start client application
		HTTP-tunneling: doesn't need setup to work within firewall
		 handles HTTP through proxy servers
		 not allow outbound TCP
##
JRMP (Java Remote Method Protocol) Java-specific,
 stream-based protocol -> looks up and refers to remote objects
 requires both client and server to use objects
 wire level -> runs under RMI and over TCP/IP
##
Multitasking -> to utilize CPU


 Process-based Multitasking (Multiprocessing) ->
  an address for each process in memory

 Thread-based Multitasking (Multithreading) ->
  same address space for threads
##  
Multithreading
 
 thread: lightweight sub-process
 smallest unit of processing
 multithreading better than multiprocessing:
  threads use shared memory area
  context-switching between threads takes less time than process

 Advantages:
  threads are independent
    no user block
    doesn't affect other threads in case of exception  
  saves time
##
Life cycle of a Thread (Thread States):
 New: thread created -> new state -> code not run yet
 Active: start() -> two states within: runnable and running
  ready to run thread moved to runnable state -> time to run <- thread scheduler
##
fixed time to each thread -> time over -> voluntarily gives up CPU to other thread

threads wait for their turn to run

 
Blocked/ Waiting <->  thread inactive 

ex:
class ABC implements Runnable  
{  
	public void run()  
	{  
		try {  
	// moving thread t2 to the state timed waiting  
			Thread.sleep(100);}  
		catch (InterruptedException ie) { 
			ie.printStackTrace();}    
		System.out.println("The state of thread t1 while it invoked the method join() on thread t2 -"+
		ThreadState.t1.getState());  
		try {Thread.sleep(200);}  
		catch (InterruptedException ie) {  
			ie.printStackTrace();}     
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
		try  {  
		// moving the thread t1 to the state timed waiting   
		Thread.sleep(200);}  
		catch (InterruptedException ie)  {  
		ie.printStackTrace();}  
		System.out.println("The state of thread t2 after invoking the method sleep() on it - "+ t2.getState());  
		// try-catch block for the smooth flow of the  program  
		try  {  
		// waiting for thread t2 to complete its execution  
		t2.join();}  
		catch (InterruptedException ie) {  
		ie.printStackTrace();}  
		System.out.println("The state of thread t2 when it has completed it's execution - " + t2.getState());  
	}  
}  
##
two ways to create a thread:
Thread class:
 provide constructors/methods to create
 perform operations on a thread.
              extends Object class and implements Runnable interface.

	Commonly used Constructors:
		Thread()
		Thread(String name)
		Thread(Runnable r)
		Thread(Runnable r,String name)



ex: extending Thread class
class Multi extends Thread
{  
	public void run()
	{  
		System.out.println("thread is running...");  
	}  
	public static void main(String args[])
	{  
		Multi t1=new Multi();  
		t1.start();  
	}  
}  

ex: implementing Runnable interface
class Multi3 implements Runnable
{  
	public void run()
	{  
	System.out.println("thread is running...");  
	}    
		public static void main(String args[])
	{  
		Multi3 m1=new Multi3();  
		Thread t1 =new Thread(m1);   // Using the constructor Thread(Runnable r)  
		t1.start();  
	}  
} 
##
Synchronization:
 control access of multiple threads to any shared resource To prevent
  thread interference
  consistency problem 
 allows only one thread to be executed at a time 
 ways:
	synchronized method
	synchronized block
    	for specific resource of method
		scope is smaller than method
	static synchronization:	 synchronized static method -> lock will on class not object
 notify(): unblock waiting thread
 notifyAll(): unblock all threads in waiting state
##
Deadlock: every thread waiting for resource held by some other waiting thread ->
          Neither of thread executes nor gets chance to execute -> code breaks

detect deadlock: run code on cmd -> collect Thread Dump, possible deadlock message 

avoid deadlock:
	no Nested lock: when provide locks to threads to give one lock to only one thread at particular time
	no unnecessary locks
    Use thread join: wait for thread til another thread finishes
##
method/class used by multiple threads at time without any race condition -> class is thread-safe
 ways:
	Synchronization
	Volatile keyword
	ock based mechanism
	atomic wrapper classes
##
Java Thread pool
 threads group, supervised by service provider, waiting for task
 size depends on number of threads kept at reserve
 advantages:
  performance
  stability
##
Concurrency:
 Executor Interface to execute new task
	example:
	public class TestThread
	{  
	   public static void main(final String[] arguments) throws InterruptedException
	   {  
		  Executor e = Executors.newCachedThreadPool();  
		  e.execute(new Thread());  
		  ThreadPoolExecutor pool = (ThreadPoolExecutor)e;  
		  pool.shutdown();  
	   }  
	   static class Thread implements Runnable
	   {  
		  public void run()
		  {  
			 try
			 {  
				Long duration = (long) (Math.random() * 5);  
				System.out.println("Running Thread!");  
				TimeUnit.SECONDS.sleep(duration);  
				System.out.println("Thread Completed");  
			 } 
			 catch (InterruptedException ex)
			 {  
				ex.printStackTrace();  
			 }  
		  }  
	   }  
	}     
##
BlockingQueue subinterface: for operations
	ex:      
	public class TestThread {  
	   public static void main(final String[] arguments) throws InterruptedException
	   {  
		  BlockingQueue<Integer> queue = new ArrayBlockingQueue<Integer>(10);  
		  Insert i = new Insert(queue);  
		  Retrieve r = new Retrieve(queue);  
		  new Thread(i).start();  
		  new Thread(r).start();  
		  Thread.sleep(2000);  
	   }  
	   static class Insert implements Runnable
	   {  
		  private BlockingQueue<Integer> queue;  
		  public Insert(BlockingQueue queue)
		  {  
			 this.queue = queue;  
		  }  
		  @Override  
		  public void run()
		  {  
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
			 }
			 catch (InterruptedException e)
			 {  
				e.printStackTrace();  
			 }  
		  }      
	   }  
	   static class Retrieve implements Runnable
	   {  
		  private BlockingQueue<Integer> queue;  
		  public Retrieve(BlockingQueue queue)
		  {  
			 this.queue = queue;  
		  }        
		  @Override  
		  public void run()
		  {           
			 try
			 {  
				System.out.println("Removed: " + queue.take());  
				System.out.println("Removed: " + queue.take());  
				System.out.println("Removed: " + queue.take());  
			 }
			 catch (InterruptedException e)
			 {  
				e.printStackTrace();  
			 }  
		  }  
	   }  
	}  

	ex:     
	public class ProducerConsumerProblem {  
		public static void main(String args[])
		{  
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
	  
		public Producer(BlockingQueue sharedQueue)
		{  
			this.sharedQueue = sharedQueue;  
		}  
		@Override  
		public void run()
		{  
			for(int i=0; i<10; i++)
			{  
				try
				{  
					System.out.println("Produced: " + i);  
					sharedQueue.put(i);  
				} catch (InterruptedException ex)
				{  
					Logger.getLogger(Producer.class.getName()).log(Level.SEVERE, null, ex);  
				}  
			}  
		}  
	  
	}  
	class Consumer implements Runnable{  
	  
		private final BlockingQueue sharedQueue;  
	  
		public Consumer (BlockingQueue sharedQueue)
		{  
			this.sharedQueue = sharedQueue;  
		}  
		
		@Override  
		public void run()
		{  
			while(true)
			{  
				try
				{  
					System.out.println("Consumed: "+ sharedQueue.take());  
				}
				catch (InterruptedException ex)
				{  
					Logger.getLogger(Consumer.class.getName()).log(Level.SEVERE, null, ex);  
				}  
			}  
		}  
	}
##
Callable interface can but Runnable can't:
 return result
 throw checked exception
##
Atomic action:
 operation in a single unit of task without interference of other operations
 cannot be stopped between task
 Once started it fill stop after the completion of task
 examples: reads and writes operation for the primitive variable (except long and double)
##
java.util.concurrent.locks.Lock pros over synchronized block:
 guarantee of sequence in which waiting thread given access
 timeout option if lock not granted 
 Lock()/Unlock()/... can be called in different methods
##
ExecutorService subinterface -> to managee lifecycle
ex:      
public class TestThread {  
   public static void main(final String[] arguments) throws InterruptedException {  
      ExecutorService e = Executors.newSingleThreadExecutor();  
      try
	  {  
         e.submit(new Thread());  
         System.out.println("Shutdown executor");  
         e.shutdown();  
         e.awaitTermination(5, TimeUnit.SECONDS);  
      }
	  catch (InterruptedException ex)
	  {  
         System.err.println("tasks interrupted");  
      }
	  finally
	  {  
         if (!e.isTerminated())
    	 {  
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
##
Asynchronous Programming: one job completed by multiple threads -> maximum usability
##
Java Future interface: result of concurrent process
##
Array/Collection:
 store references
 manipulate data
 Arrays: fixed size, store homogeneous, no ready-made methods   
 Collections: variable size, heterogeneous, readymade methods 
##
1)	ArrayList not synchronized.	Vector: synchronized.
2)	ArrayList not a legacy class.	Vector: legacy class.
3)	ArrayList increases its size by 50% of the array size.
	Vector increases its size by doubling the array size.
4)	ArrayList not ?thread-safe? as not synchronized.
	Vector list thread-safe as it's every method is synchronized.
##
1)	ArrayList uses a dynamic array.	LinkedList uses a doubly linked list.
2)	ArrayList not efficient for manipulation because too much is required.
	LinkedList efficient for manipulation.
3)	ArrayList better to store and fetch data.	LinkedList better to manipulate data.
4)	ArrayList provides random access.	LinkedList does not provide random access.
5)	ArrayList takes less memory overhead as it stores only object
	LinkedList takes more memory overhead as it stores object and address
    Iterator traverses elements in forward direction only whereas ListIterator
     traverses elements into forward and backward direction.
##
1)	Iterator traverses elements in forward direction only.
	ListIterator traverses elements in backward and forward directions both.
2)	Iterator can be used in List, Set, and Queue.
	ListIterator can be used in List only.
3)	Iterator can only perform remove operation while traversing collection.
	ListIterator can perform add, remove, and
     set operation while traversing collection.
1)	Iterator traverse legacy and non-legacy elements.
	Enumeration traverse only legacy elements.
2)	Iterator is fail-fast.	Enumeration is not fail-fast.
3)	Iterator is slower than Enumeration.
	Enumeration is faster than Iterator.
4)	Iterator can perform remove operation while traversing collection.
	The Enumeration can perform only traverse operation on collection.
##
List contain duplicate elements
List is ordered collection maintains insertion order 
List contains single legacy class which is Vector class whereas Set interface does not have any legacy
 class.
List allow n number of null values whereas Set only allows single null value.
##
HashSet maintains no order, TreeSet maintains ascending order.
HashSet impended by hash table, TreeSet implemented by Tree structure.
HashSet performs faster than TreeSet.
HashSet backed by HashMap, TreeSet backed by TreeMap.
##
Set contains values only, Map contains key and values.
Set contains unique values, Map contain unique Keys with duplicate values.
Set holds single number of null value, Map include single null key with n number of null values.
##
HashSet contains only values whereas HashMap includes entry (key, value).
HashSet can iterate, HashMap needs to convert into Set to iterate.
HashSet implements Set, HashMap implements Map
HashSet no duplicate value, HashMap contain duplicate values with unique keys.
HashSet contains only single number of null value whereas HashMap hold single null key
 with n number of null values.
##
HashMap maintains no order, TreeMap maintains ascending order.
HashMap implemented by hash table, TreeMap implemented by Tree 
HashMap sorted by Key or value, TreeMap sorted by Key.
HashMap contain null key with multiple null values, TreeMap cannot hold null key
 but can have multiple null values.
##
1)	HashMap not synchronized.
	Hashtable synchronized.
2)	HashMap contain one null key and multiple null values.
	Hashtable cannot contain any null key or null value.
3)	HashMap not thread-safe -> useful for non-threaded applications.
	Hashtable is thread-safe, and it can be shared between various threads.
4)	HashMap inherits AbstractMap class,	Hashtable inherits Dictionary class.
##
Collection is interface, Collections is class.
Collection -> List, Set, Queue. Collections -> sort and synchronize collection elements.
##
hashCode() -> same integer if two keys by calling equals() are identical.
##
possible that two hash code numbers have different or same keys
##
equals() -> override to check objects based on property.
##
synchronize List, Set and Map by Collections
##
generic collection:
 not need typecasting if using generic class
 type-safe
 checked at compile time
 makes code bug detectable at compile time -> more stable code
##
hash-collision: Two keys with same hash value
 to avoid -> keep Two separate entries in a single hash bucket
             Separate Chaining
             Open Addressing
##			 
Dictionary: key-value pairs.
##
load factor default size: 0.75.
default capacity: initial capacity * load factor
##
Fail-fast iterator: throws ConcurrentmodificationException in case of structural modification 
                    not require any extra space in memory.
##
unmodifiableCollection() -> make Java ArrayList Read-Only
##
remove duplicates from ArrayList:
 by HashSet: not preserve insertion order.
 by LinkedHashSet: maintain insertion order
ex:
public class ReverseArrayList
{  
	public static void main(String[] args)
	{  
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
##
ex: sort ArrayList in descending order:

public class ReverseArrayList
{  
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
##
synchronize ArrayList:
 Using Collections.synchronizedList() 
 Using CopyOnWriteArrayList<T>


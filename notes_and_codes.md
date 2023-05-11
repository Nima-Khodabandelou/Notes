##
- Liskov substitution 
   
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
   
- Dependency Inversion
	
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
- Final keyword
   
      can’t reassign final reference variable, But the object it refers to is mutable.
      
      ex:
	      final Cat cat = new Cat();
	      cat.setWeight(5) -> valid	 
      interface can never be final      
      
		public void methodWithFinalArguments(final int x) {
			x=1;
		}

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
- Immutability

      create immutable class
	
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
- Type promotion in Java

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
- copy values of one object into another

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
- Method overloading

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

##   
- covariant return type: 
		       
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
- overridden method

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
	
	ex:
		Simple1 s=new Simple1();
		System.out.println(s instanceof Simple1);//true
##
- Interface

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
- Exception Propagation

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
- inner class

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
- Garbage Collection

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
- Java Runtime class

	ex:
	public class Runtime1{  
	 public static void main(String args[])throws Exception{  
	  Runtime.getRuntime().exec("notepad");//will open a new notepad  
	 }  
	}  
##
- Serialization

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
Socket programming

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
java.lang.Class:

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
javap

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
access private constructor

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
Unboxing and autoboxing -> 
	
  
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
Singleton class:
	
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

##
JavaBean:

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
threads:

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
Concurrency:

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
ExecutorService subinterface 
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
remove duplicates from ArrayList:

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



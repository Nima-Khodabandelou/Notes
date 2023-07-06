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
 
	}  
	// the craeteObjByConstructorName() method is used to create an 
			constt.setAccessible(true);      
			Object exception  
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





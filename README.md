# java_core

Core concepts of Java SE

- First of all SOLID Principles (not specific to Java):

	1- Single Responsibility for Each class <-> Just one reason needed to change that class.
		 Advantages:
			 Testing –> fewer test cases for each class.
			 Lower coupling –> fewer dependencies.
			 Smaller and well-organized classes
		 
	2- Class shoud be Opened for Extension and Closed for Modification. Otherwise, modifying
	   the existing code -> potential new bugs.
	   If fixing bugs -> extend the class

	3- Liskov Substitution: if class A is a subtype of class B, one should be able to replace B with A
	   without disrupting the behavior of the program.
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
			// This new Vehicle is electric -> changes the program behavior!
			//-> Liskov Substitution violated!
			throw new AssertionError("Tesla doesn't have Internal Combustion (IC) engine!");
		}
		public void accelerate() {
			//Too much for Tesla!
		}
		// Possible Soultion -> Code another interface for taking into account the non-ICEngine ones.
	}

	4- Interface Segregation: larger interfaces be splited into smaller ones -> More specific
	   methods in each interface.
	5- Dependency Inversion: Decoupling software modules -> high-level/low-level modules and details
	   depend on abstractions.
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
		private SalesDepartment salesDepartment = new SalesDepartment();
		private WarehouseDepartment warehouseDepartment = new WarehouseDepartment();
		public void OrderInquiry() {
			salesDepartment.customerSupport();
			warehouseDepartment.qualityControl();
		}
	}
	Manager class depends on low-level modules -> refactor using abstraction: 
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

       Classpath: Java specific used to locate class files. it can be a directory, ZIP, JAR, etc.

- Source files: 

       Each source Java file may have multiple classes among which only one shall be public.
       
       Source file name shall be the same as class name.

- OS Architecture: Java is neutral w.r.t to OS architecture (32 bit or 64 bit).

- Interpreter/Compiler:

      Just-in-time (JIT): An interpreter to improve performance by compiling parts of the bytecode
                        having similar functionality, and therefore reducing compilation time.  

      Compiler: transforms instruction set of a Java virtual machine (JVM) to the instruction set
                of a specific CPU (Java code to Bytecode).      

      Classloader: Part of the Java Runtime Environment for loading class files. Three built-in
                   classloaders:
				   
						Bootstrap ClassLoader: The first classloader in native code (e.g. c++) which
                                               loads rt.jar file containing all core libraries and
											   class files of Java SE There are various implementations
											   of this Bootstrap class loader for various platforms.

						Extension ClassLoader: Its parent is Bootstrap classloader loads core extension
    						                   classes to be available to all applications running on
											   each platform. 

						System/Application ClassLoader: Loads files in the classpath.
            
- Local variables not initialized to any default value.

- Acccess modifiers:

      Default: accessible within the package only.
      
      Protected: accessible by the class and sub-class of the same package, or by the sub-class in another packages.
      
      Public: accessible anywhere
      
      Private: accessible within the class

##
- SOLID Principles (not specific to Java)
###
      1- Single Responsibility for Each class: There should be just one reason to change the class.	 
      1-1- Advantages:
           Fewer tests for each class.
           Lower coupling –> fewer dependencies.
           Smaller and well-organized classes		 
      2- Class shoud be Opened for Extension and Closed for Modification. Otherwise, modifying the existing code -> potential new bugs.	If fixing bugs -> extend the class.
      3- Liskov Substitution: If class A is a subtype of class B, one should be able to replace B with A without disrupting the behavior of the program.	
      4- Interface Segregation: larger interfaces be splited into smaller ones -> More specific methods in each interface	   
      5- Dependency Inversion. Decoupling software modules -> high/low-level modules and details depend on abstractions
## 
- OOP

      Obj:
	   real-time entity having state and behavior      
	   instance of class      
	   instance variables <-> obj state      
           methods <-> obj behavior      
           create using new keyword.      
           obj refs <-> init to null	 
      Inheritance:
           Code reusability -> sub need not redefine method of super unless need to provide specific impl.
           Runtime polymorphism -> simulate inheritance with real-time objs -> makes OOPs more realistic.
           Provides data hiding -> super hide data from sub
           Method overriding
      Abstraction:
          Focus on what obj does instead of how it does	
      Encapsulation:      
          Wraps code and data into single unit
	      Read-only class	
	          private fileds	
	          no setter	
	          getter return private fields to main method
	      Write-only class	
	          private fileds	
	          no getter	
	          setter set value passed from main to private fields	  
      Acccess modifiers:
	      Default: accessible within package
	      Protected: accessible by class and sub of same package, or by sub in another package
	      Public: accessible anywhere
	      Private: accessible within class	      
      Constructor:
	      special method to init state
	      invoke when class instantiate, obj created, and memory allocated for obj -> no sense to make it static
	      default constructor called on obj creation using new keyword
	      no explicit return type
	      not inherited
	      can't be final	      
##
- Main Java features

      Statically typed language -> inherently secure
      For Desktop, Mobile, and Web      
      Java compiler output is Bytecode (JVM specific set of instructions) rather than exe file -> secure and portable (Platform-independent)       
      JVM:
		Executes Bytecodes.
		Is part of JRE.
		Is implemented for various platforms.
		Can create a restricted execution environment (sandbox) preventing unrestricted access to the machine.
      High-level
      Multi-threaded      
      Memory Efficient and Multi-Threaded -> Robust     
      Local variables not init. to default value    
      Does not support:
	      pointers (Handles it internally)
	      goto
	      operator overloading
	      call by ref
	      structures and unions
##       
- Path and Classpath

       PATH: An environment variable used by the O.S. to locate the
       executables

       Classpath: Java specific used to locate class files/dir./
       ZIP/JAR/...
## 
- Source files

      Each Java file -> multiple classes -> only one public

      Source file name -> same as class name
## 
- O.S. Architecture

      Java is neutral w.r.t to O.S. architecture (32/64 bit)
## 
- Interpreter/Compiler

      Just-in-time (JIT): To improve performance by compiling parts of bytecode
                        having similar functionality -> reducing compilation time  

      Compiler: transforms instruction set of JVM to instruction set of specific
      CPU (Java code to Bytecode)      

      Classloader: Part of JRE for loading class files
      Built-in classloaders
      
		Bootstrap
		
		  First classloader in native code (e.g. c++)
		
		  loads Java SE core libs and class files
		
		  various implementations for various platforms

		Extension
		
		  Child of Bootstrap
		
		  Loads core extension classes to be available to all apps running
		  on each platform. 

		System/app: Loads files in classpath
##
- package

      group of similar classes/
      s/sub-packages

      no name clash
      
      easier access control.
      
      hidden classes
      
      easier to locate related classes   
##	  
- method

      exposes obj behavior

      must have a return type

      is invoked explicitly

      is not provided by the compiler in any case.

      method name may or may not be same as class name      
##
- Final keyword

      final class cannot be subclassed.
	
      final method cannot be overridden.
	
      create and document class carefully or declare it final for safety reasons.
	
      final class: can’t be improvede or fixed -> lose extensibility
	
      make called methods of class final. Otherwise, overriding can affect callers
	
      make constructor called methods final
	
      can extend class with all methods final
	
      can’t reassign final ref variable But obj it refers to is mutable
      
      ex:
	      final Cat cat = new Cat();
	      cat.setWeight(5) -> valid
	 
      class constants: uppercaseو final, underscored:
	
         static final int MAX_WIDTH = 999;
	 
      static final fileds: init upon declaration in static init block
	
      instance final fields: init upon declaration in instance initializer
      block in constructor
	
      final argument can’t be changed inside method
      
      constructor and interface can never be final      
 ##
- Immutability

      create immut. obj -> not allowed to change/update content ->
	  If try to change and alteration successfully done -> 
	  create new obj
	
      immut. obj -> state doesn’t change after init
	
      benefits:
	
		for caching 
		
		inherently thread-safe	
		
      create immut class:
	
		Declare class as final
		
		all fields private
		
		No setter
		
		all mutable fields final
		
		Init all fields using constructor performing deep copy
		
		return copy of obj by cloning rather than returning
		actual obj ref
		
		deep copy -> getter function returns clone of original obj ->
		             HashMap values don't change 
##
- static 

      static methods/variables -> shared among all objs of class 

      static vars

	  stored in class area, no need to create obj to access

	  get memory once in class area at time of class loading

	  maker program memory efficient 

	  belong to class rather than obj
 
      static methods

	  can't use non-static data member

	  can't call non-static method directly

	  can't be overriden
  
      Static block

	  to init static data members

	  execute before main method at time of class loading 
## 
- Type promotion in Java

      Byte -> Short (2 byte) -> Int (4 byte) -> Long (8 byte) -> Float (4 byte) -> Double (8 byte)

      Char (2 byte) -> Int      
## 
- this and super

      non-static -> cannot be used in static context 

      Can't use both in constructor
      
      must be first statement in constructor
	  
      this:	  
	   
       possible but not good to refer static members <--> it is unnecessary to
        access static variables through objs
	
       to perform constructor chaining within same class
	  
       to pass as arg in method -> used in event handling 

       to pass as arg in constructor call -> for one
       obj in multiple classes
	  
       to distinguish local/instance vars   
 
       to invoke method of current class -> If don't use 'this', compiler
       automatically adds
	  
       advantages of passing this into method instead of current class obj

         this is final -> cannot be assigned to any new value whereas current
         class obj might not be final
 
         this can be used in synchronized block
		 
       is final ref in Java

      super:

        to refer to immediate parent class obj/instance var
	
        to invoke immediate parent class method/constructor	
	
        instance of sub creates -> instance of parent creates
        implicitly referred by super   
	
        for init super vars within sub constructor 
	
        for constructor chaining
		
        Called implicitly by class constructor if not provided 
       
        To differentiate between local/instance vars in class
        constructor		
##
- main method

      is static -> Because obj not required to call static method

      non-static main method -> JVM creates obj first then
      calls main() -> extra memory allocation
## 
- abstract

      method -> if be static -> becomes part of the class -> can directly call it which
      is unnecessary.
      
      class -> can declare static vars/methods
##
- copy values of one obj into another

      By constructor

      By assigning values of one obj into another

      By clone() method of Obj class
## 
- obj cloning <--> shallow copy

      create exact copy of obj -> clone() -> java.lang.Cloneable      

      syntax -> protected obj clone() throws CloneNotSupportedException 

      clone() saves extra processing compared to new keyword
 
      Advantage

		no need to write lengthy and repetitive codes

		easiest -> define parent class, implement Cloneable

		fastest way to copy array  

      Disadvantage

		hange lots of syntaxes

		implement cloneable interface having no methods

		clone() is protected -> have to provide our own clone() and
		indirectly call obj.clone()

		no constructor invoke -> no control over obj
		construction  

		clone() in child -> all supers should define clone() or inherit it 

		only shallow copying -> need to override for deep copying
## 
- Aggregation (has-a)

      relationship between two classes -> aggregate class contains a ref
      to class it owns
## 
- composition

      When obj contains other obj, if contained obj cannot
      exist without existence of container obj

      particular case of aggregation representing stronger relationship
      between two objs
      
      Ex: Company contains Employees. Employee cannot exist without company
## 
- pointer

      var refering to memory address
      
      not used in Java

## 
- Method overloading

      multiple methods with same name but different signatures

      ways:
		Changing number of arguments
		
		Changing data type of arguments
		
      increases readability
	
      Type promotion is method overloading

      static method -> part of class not obj -> can't be overridden
## 
- exceptions in sub/super

      No exception in super & checked exception in sub -> error

      No exception in supe & unchecked exception in sub

      exception in super (exc1) & exception other than exc1, exc1's child,
      and runtime exception in Sub -> error

      exception in super (exc1) & child exception of exc1 in Sub

      exception in super & no exception in Sub
##   
- covariance

      how subtype is accepted when only supertype is defined
	
      covariant return type: overriden method return type may vary in
      same direction as sub 
		       
         no type casts in class hierarchy      
## 
- polymorphism

      compile-time: static binding, early binding, or overloading ->
       (obj type determined/call to method resolved) at
       compile-time -> fast execution
	
      runtime: dynamic binding, late binding, overriding, dynamic method
        dispatch -> (obj type determined/call to overridden
	 method resolved) at runtime.
##
- overridden method

      Override <--> IS-A (super/sub relationship)

      can override overloaded method      
 
      overridden method scope change in sub must be less
         restricitve <-> (public < default < protected < private)

      called through ref var of sup

      determination of method to be called is based on obj being
      referred to by ref var

      data members cannot be overridden -> no Runtime
        Polymorphism by data members 

      private, final or static method in class -> static binding
## 
- instanceof

	compares instance with type
## 
- abstract class

      can have (abstract and non-abstract methods)/data member/constructor/
	main()/static methods

      can have final methods -> forces sub not to change method body 

      can never be instantiated even if it contains constructor and
	implemented methods

      can provide implementation of interface

      can extend another class        

      static + abstract -> not allowed
##
- Interface

      can't provide impl of abstract class
	
      can extend another interface
	
      Members are public by default
	
      methods are abstract by default
	
      obj ref can be cast to interface ref when it
	implements referenced interface
	
      Marker interface: interface with no data member
	 and member functions -> Serializable, Cloneable
##
- Interface vs. Abstract class (note that some are rephrased of others)

      abstract class
		for inheritance concept

		to define default behavior for subs <-> childs should have same functionality
		to declare non-public members ( in interface all methods must be public)

		for situation when there are many methods in base and some are common in subs
		 (typically those common methods are implemented in abstract class and
		 other non-common ones remain abstract to later be implemented by subs)

		to add new (non-abstract) methods in the future for better forward compatibility (in case 
		 of interface if add new methods then all classes implementing that
		 interface should implement new methods)

		to create multiple versions of a component: by updating abstract class, all
		 childs automatically update but in case of interface if a new version
		 needed then a new interface should be created

		to partially implement class

		for objects that are closely related
		 has some default implementations in abstract class and some tools
		 for implementation in sub. every sub should use the base.
		 if one has developed their own class hierarchy then it's not
		 suitable to use base abstract class

		sub can extend only one abstract but impl many interfaces

		sub need not to provide impl for all methods of base (contrary
		to interface whose all methods should be implemented) 

      interface 
      
		 define a contract behavior between systems/codes/behaviors/services/...

		 has public methods -> bad choice if not want to expose everything

		 has default & static methods

		 for designing small, concise bits of functionality across range of
		  disparate & unrelated objects (i.e. a base for class hierarchy)

		 for situation when API not change for a while

		 for something similar to multiple inheritances since can impl multiple interfaces

		 interface default method
			helps to extend interface functionality without breaking subs
			to avoid utility classes
			to support lambda in Collections
			can't overr methods from java.lang.Object		
			if sub extends two interfaces with common default methods in each
			   interface, then sub should impl the default method as well

		  interface static method
			for utility like null check, collection sorting,...
			for security -> sub can't overr it

		  functional interface: has only one abstract method -> instantiate using lambda

      use both abstract and interface      
		 ex: a base interface with methods that every sub should impl
		     if there comes other methods that only some subs should impl -> extend
		     base interface and create a new interface containing those new methods.
		     subs can choose to impl inter1 or inter2. if the number of methods grows
		     a lot -> better to have an abstract class providing skeletal impl of inter2
		       -> sub has flexibility to choose abstract class or interface
       
##
- Exceptions

      Checked Exception -> checked at
	  compile-time: SQLException,
	  ClassNotFoundException, ...

      Unchecked Exception -> handled at
	  runtime: ArithmaticException,
	  NullPointerException,
	  ArrayIndexOutOfBoundsException, ...

      Error: not recoverable -> cause program 
	  to exit: OutOfMemoryError,
	  AssertionError, ...

      exception handling:  maintains normal flow
	 of app
	
      try block followed by either catch OR
	 finally block

      throw -> to throw exception

      throws -> to declare possible exceptions
	  that may occure in method

      Hierarchy of Java Exception classes:

	Throwable -> Exception, Error
	
	Exception -> IOException, SQLException, ClassNotFoundException,
	  RuntimeException
	
	RuntimeException -> ArithmeticException, NullPointerException,
	  NumberFormatException, IndexOutOfBoundsException
						
	IndexOutOfBoundsException -> ArrayIndexOutOfBoundsException,
	  StringIndexOutOfBoundsException
	
	Error -> StackOverflowError, VirtualMachineError, OutOfMemoryError	

      Common exception Scenarios:

	divide number by zero -> ArithmeticException.
	
	operation on null var -> NullPointerException	
	
	var formatting mismatched -> NumberFormatException
	
	array size exceed -> ArrayIndexOutOfBoundsException
	
      Exception Propagation:

	[thrown from top -> not caught -> drops down previous]
	--> continues until caught or reach very bottom of call stack
	
	Unchecked -> propagated by default
 
      Nested try block: one error in sub-block & another
       error in entire block
 
      Finally:

	executes after try-catch

	not executes if program exits

      custom exception -> extend Exception

      can not throw basic data type from block
##
- String pool

	space reserved in heap to store strings
	
 	when create string literal -> JVM checks
	 string pool:
	
		if exists -> a ref returns
		
		If not ->  new string instance creates 
##
- create string obj

	String Literal:
	
		String s ="welcome";
		
		String s2="Welcome";//It doesn't create a new instance
		
	new keyword:
	
	  String s=new String("Welcome");
	  //creates two objs and one ref var				
	  //new obj in heap refered by s		
	  //literal obj "Welcome" in string pool		
	  //ref var s
##
- String disadv. compare to StringBuffer

	String  immutable
	
	String  slow creates a new instance on concatThe 
	
	String  overrides  equals()  
##
- StringBuffer

	synchronized -> thread safe -> two StringBuffer methods
	can't be called simultaneously

	less efficient than StringBuilder.	
##
- toString(): returns string representation of obj ->
   overriding -> desired output
##
- String is in string pool until garbage collection -> not good
   for stornjng password -> CharArray() is better and can be set to blank 
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
##
- nested interface

	interface within class
	public if declared inside interface
	any access modifier if declared within class
	static
## 
- class inside interface -> static nested class by compiler
##
- Garbage Collection

	removing unused objs from memory

	gc() to garbage collect -> depends on JVM whether to perform
##
- unreferencing an obj by

	nulling the ref
	
		Employee e=new Employee(); -> e=null; 
		
	assigning ref to another
	
		Employee e1=new Employee();  
		Employee e2=new Employee();  
		e1=e2;//e1 available for garbage collection
		
	anonymous obj -> new Employee(); 
##
- An unreferenced obj can be referenced again
##
- Java Runtime class

	-> to execute process, invoke GC, get total and free memory, ...

	only one instance of Runtime class

	Runtime.getRuntime() returns singleton instance of Runtime class.
##
- hierarchy of InputStream and OutputStream
	
	OutputStream -> FileOutputStream, ByteArrayOutputStream,
	                FilterOutputStream, PipedOutputStream
			objOutputStream,
			
			FilterOutputStream -> DataOutputStream,
			BufferedOutputStream, PrintStream

	InputStream -> FileInputStream, ByteArrayInputStream,
	               FilterInputStream, PipedInputStream
		       objInputStream

	               FilterInputStream -> DataInputStream,
		          BufferedInputStream,
	                  PushBackInputStream

	stream: sequence of data composed of bytes from source to destination

	three automatic streams:

		System.out: standard output 

		System.in: standard input 

		System.err: standard error



      Reader/Writer class hierarchy -> character-oriented,
      InputStream/OutputStream class hierarchy -> byte-oriented.

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
FilePermission:

      alter permissions of a directory or file related to a path. -> two path types:
      
            all subdirectories and files 
 
            all directory and files within directory excluding subdirectories.
  
##
FilterStream: filters read data, adds line numbers,...
##
I/O filter

 reads one stream and writes to another,
 usually altering data

##
take input from console:

      BufferedReader (efficient): use InputStreamReader to
      take input from console -> pass input to BufferedReader.
	

      Scanner class
	 breaks input into tokens 
	 
	 provides many methods to read
	 
	 parse various primitive values
	 
	 widely used with regex
##    
Using Console class:

      read console input, texts, passwords (not be displayed to user).
     
##
Serialization

 writing state of obj into byte stream
 
 used in Hibernate, RMI, JPA, EJB and JMS
 
 used to travel obj's state on network (known as marshaling).

 to save state to storage for later restoration

 Serializable interface -> to serialize (super-)class ->
 to prevent  child class serialization ->
 implement writeobj()/readobj() along with throw NotSerializableException in sub. 
##
transient data member can not be serialized
##
Externalizable interface: write state of obj into byte stream in compressed format


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
 communication between apps running on different JRE.
 connection-oriented -> Socket and ServerSocket classes
 connectionless -> DatagramSocket
 
	client needs:
		server IP address
		port number

 steps for TCP connection:
  server -> ServerSocket instantiation -> port number
 
 server -> accept() method -> wait until client attempts to connect 

 client creats socket 

 connection established -> socket obj for client 

 server uses accept() to return a ref to new socket 
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
##
newInstance()

 invoke constructor at runtime. 
##
javap

 disassembles class file -> gives info about fields/constructors/ methods

(java.lang.Class + java.lang.reflect.Method) -> change class runtime behaviour
 -> access private method from outside <-
 
	1) setAccessible(boolean status) throws SecurityException
	  
	2) invoke(obj method, obj... args) throws IllegalAccessException,
					  IllegalArgumentException, InvocationTargetException
	1) getDeclaredMethod(String name,Class[] parameterTypes)throws NoSuchMethodException,
	   SecurityException
##
access private constructor -> getDeclaredConstructor()
##
Wrapper classes

  conversion of objs to primitives (unboxing) and primitives to objs (autoboxing)

##
Unboxing and autoboxing -> 
	
      automatic in Java
	
      valueOf()/xxxValue() for manual conversion
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
##
JavaBean:
	
 reusable software component
	
 encapsulates many objs into one in order to access it from multiple
  places. 
	
 easy maintenance. 

##
RMI (Remote Method Invocation)
	
      for distributed app
	
      allows obj -> invoke methods on obj in another JVM by stub (for client side) and skeleton
	
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
	
		invokes method on actual remote obj
	
		writes and transmits (marshals) result to caller

      RMI in programs:
	
		Create remote interface.
	
		Provide implementation of remote interface
	
		Compile implementation class and create stub and skeleton
		 using rmic
	
		Start registry service by rmiregistry
	
		Create and start remote app
	
		Create and start client app
	
		HTTP-tunneling:
	
	         doesn't need setup to work within firewall
	
		 handles HTTP through proxy servers
	
		 not allow outbound TCP
##
JRMP (Java Remote Method Protocol):
	
 Java-specific
	
 stream-based protocol -> looks up and refers to remote objs
	
 requires both client and server to use objs
	
 wire level -> runs under RMI and over TCP/IP
##
Multitasking 
	
     to utilize CPU


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
threads:
	
      Life cycle of a Thread (Thread States)
	
        New: thread created -> new state -> code not run yet
	
        Active: start() -> two states within: runnable and running
	
        ready to run thread moved to runnable state -> time to run <- thread scheduler

      fixed time to each thread -> time over -> voluntarily gives up CPU to other thread

      threads wait for their turn to run
 
      Blocked/ Waiting <->  thread inactive 

      two ways to create a thread:
	
        Thread class:
	
          provide constructors/methods to create
	
          perform operations on a thread.
              extends obj class and implements Runnable interface.

	Commonly used Constructors:
		Thread()
		Thread(String name)
		Thread(Runnable r)
		Thread(Runnable r,String name)
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

	static synchronization:	

 synchronized static method -> lock will on class not obj

 notify(): unblock waiting thread

 notifyAll(): unblock all threads in waiting state
##
Deadlock: every thread waiting for resource held by some other waiting thread ->
          Neither of thread executes nor gets chance to execute -> code breaks

detect deadlock: run code on cmd -> collect Thread Dump, possible deadlock message 

avoid deadlock:

	no Nested lock: when provide locks to threads to give one lock to only one thread at     particular time

	no unnecessary locks

Use thread join: wait for thread until another thread finishes
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
##
BlockingQueue subinterface: for operations
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
##
Asynchronous Programming: one job completed by multiple threads -> maximum usability
##
Java Future interface: result of concurrent process
##
Array/Collection:

 store refs

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

5)	ArrayList takes less memory overhead as it stores only obj
	LinkedList takes more memory overhead as it stores obj and address
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

List contains single legacy class which is Vector class whereas Set interface does not have any legacy class.

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

3)	HashMap not thread-safe -> useful for non-threaded apps.
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
equals() -> override to check objs based on property.
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
##
ex: sort ArrayList in descending order:
##
synchronize ArrayList:

 Using Collections.synchronizedList() 

 Using CopyOnWriteArrayList<T>


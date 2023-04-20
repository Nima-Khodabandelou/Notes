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

      - Just-in-time (JIT): An interpreter to improve performance 

      - Compiler: transforms instruction set of a Java virtual machine (JVM) to the instruction set of a specific
        CPU (Java code to Bytecode).

      - JIT compiles parts of the bytecode having similar functionality, and therefore reduces compilation time. 

      - Classloader: JVM subsystem  for loading class files using java.lang.ClassLoader.loadClass(). part of the
        Java Runtime Environment

      - Three built-in classloaders:

            Bootstrap ClassLoader: The first classloader in native code (e.g. c++) which loads rt.jar file
                                   containing all core libraries and class files of Java SE. There are various
                                   implementations of this Bootstrap class loader for various platforms.

            Extension ClassLoader: Its parent is Bootstrap classloader used for loading Java core extension
                                   classes in order to be available to all applications running on each platform. 

            System/Application ClassLoader: loads our files in the classpath.
            
- Local variables: not initialized to any default value.

- Acccess modifiers:

      - Default: accessible within the package only.
      
      - Protected: accessible by the class and sub-class of the same package, or by the sub-class in another
        packages.
      
      - Public: accessible anywhere
      
      - Private: accessible within the class
       

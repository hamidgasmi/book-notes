# Books Notes:

## 1. Write Great Code, Volume 1:
By Randall Hyde, 2004

<details>
<summary>1. What You Need to Know to Write Great Code</summary>
</details>

<details>
<summary>2. Numeric Presentation</summary>

- Radix: Base 
- Binary representation in programming languages: 
    - MASM t assembler adds a suffix: 
        - 1001b = 1001B = 10 base 10 
        - 1001 = One hundredand one base (radix) 10 
- Hexadecimal representation: 
    - How to make the difference between the numbers DEAD, BEEF, FEED, DEAF from standard program identifiers
    - C, C++, C#, Java add a prefix: 0xDEAD 
    - MASM adds a sufix h or H and should beggin with a digit (0-9): 
        - 0A001h, 234H
        - Something obiguous like "dead" would be written "0deadh" 
- Numeric String Presentation: 
    - Reading/writing a number from/to a user’s consol involve a string to number conversion (cin >> i in C++) 
    - A conversion from/to a string to/from a number is low 
    - It requires multiple steps
    - E.g., Conversation of a string to an unsigned integer: 
        - (1) Initialize an integer variable to 0 
        - (2) If there are no digits in the string, then the algorithm is complete and the variable holds the numeric value 
        - (3) Fetch the next digit (going from left to right) from the string 
        - (4) Multiply the variable by then and then add the digit fetched in step (3) 
        - Go to step (2) 
    - Converting an integer to a string takes even more effort 
        - It involves divisions by 10 
        - Division is very slow 
    - Great programmer will be careful the use of numeric/string conversions
        - Only use them when necessary 
- Internal numeric Representation: 
    - Make sure that your program use data objects that the machine can represent efficiently 
    - A Bit: 
    - A Nibble:
        - 4 bits  
        - Most computer systems don’t provide efficient access to nibbles in memory 
    - A byte: 
        - 8 bits 
        - The smallest addressable Data item on many CPUs 
        - The CPU can efficiently retrieve data on a 8-bit boundary from memory 
        - It’s the smallest unit of a storage on most machines 
        - Many languages use bytes to represent objects that require fewer than 8 bits such as Boolean 
        - To describe bits within a bytes, a bit number is used: 
        - Bit 0: LO, the Low Order bit or Least Significant bit 
        - Bit 1: 
        - ...
        - Bit 7: HO, Highest Order or Most Significant bit 
    - A word: 
        - It has a different meaning depending on the CPU 
        - On some CPU, it’s a 16-bit Object 
        - On other CPU, it’s a 32-bit or 64-bit Object 
        - In the 80x86 terminology, it’s 16-bits quantity 
        - Bit number 0… 15, LO, HO 
    - A double word: 
        - It's also called: dword 
        - In the 80x86 terminology, it’s a 32-bit Object 
        - CPU handles efficiently objects up to a certain size (typically 32 or 64 bits) 
        - This doesn’t mean that we can’t work with larger objects 
        - It simply becomes less efficient to do so 
        - This is why you typically won’t see programme handling numeric objects much higher than about 128 or 256 bits
    - A Quad word: 64 bits 
    - A Long word: 128 bits (a convention in the book only) 
    - A tbyte: 
        - An 80-bit type that is on Intel 80x86 platforms 
        - The 80x86 CPU family uses tbyte variables to hold extended precision floating-point values and certain binary-coded decimal (BCD) values
- Signed Numbers - The 2’s complement numbering system: 
    - It uses the HO bit as a sign bit 
    - With n digits, we can represent -2^[n -1] to +2^[n-1] - 1
    - E.g., with a 8-bit number 0x80 (10000000) is the smalled 16-bit negative number
    - Negation Algorithm:
        - Invert all the bits in the number 
        - Add +1 and Ignore any overflow 
        - E.g. 1, 0x05 (+5) => (Inversion) 0xFA =>(+1) 0xFB (-5) 
        - E.g. 2, 0xFB (-5) => 0x04 => 0x05 (+5) 
        - E.g. 3, 0x80 (smallest negative number in 8-bit representation) => 0x7F => 0x80
    - Smallest negative number in n-bit doesn't have a positive representation in n-bit representation (see n-bit representation limit above)
    - A single negative value will have different representations depending on size of the representation:
        - E.g. 1, -64:
            - It's 0xC0 in a 8-bit representation 
            - It's 0xFFC0 in a 16-bit representation
        - E.g. 2, -126: 
            - It's 0x82 in 8-bit representation
            - It's 0xFF82 in a 16-bit representation
- Some useful Properties of Binary Numbers: 
    - If LO bit = 1 in a binary (integer) => odd
    - If LO bit = 0 in a binary (integer) => even 
    - If the n LO bit of a binary number all contain 0 => the number is evenly divisible by 2^n
        - 00011000 (+24) => it's divisible by 2^3 (+8)
        - 00101000 (+40) => it's divisible by 2^3 (+8)
        - 10101000 (-88) => it's divisible by 2^3 (+8)
    - If a binary value contains a 1 in bit position p and 0s everywhere else => it’s equal to 2^p
        - 00001000 (p: 3) is equal to 2^3 (+8)
        - 01000000 (p: 7) is equal to 2^7 (+128)
    - If a binary value contains all 1s from Bit 0 to bit p - 1 and 0 elsewhere => it’s equal to 2^p - 1
        - 00001111 (p: 4) is equal to 2^4 - 1 (+15)
        - 01111111 (p: 7) is equal to 2^7 - 1 (+127) 
    - Shifting all bits in a number to the left by 1 position multiplies the binary value by 2
        - Shift(00001110, -1):(14*2) 00011100 (1C:28)
        - What about signed binary numbers?
    - Shifting all bits of an unsigned binary number to the right by 1 position divides the number by 2
        - Shift(00001110, +1) (14/2) 00000111 (+7)
        - Shift(00000111, +1) (7/2) 00000011 (+3)
    - Multiplying 2 n-bit binary values together may require as many as 2*n bits to hold the result
    - Adding or substracting 2 n-bit binary values never requires more than n+1 bits to hold the result
    - Inverting all bits in a binary number is the same thing as negating (changing the sign) and then substracting 1 from the result
        - Not n = n * (-1) - 1
    - Incrementing (adding 1 to) the largest unsigned binary value for a given number of bits always produces a value of 0
    - Decrementing (substracting 1 from) zero always produces the largest unsigned binary value for a given number of bits
    - An n-bit value provides 2^n unique combinations of those bits
    - The value 2^n - 1 contains n bits, each containing the value 1
    - You should memorize all the powers of 2 from 2^0 through 2^16, as these values come up in programs all the time
- Sign Extension, Zero Extension, and Contraction:
    - Extension of a non-negative value is different from the extension of a negative value:
        - E.g. of a non-negative value: 0x40 in 8-bit is 0x0040 in 16-bit
        - E.g. of a negative value: 0x82 in 8-bit is 0xFF82 in 16-bit (see 2's compliment numbering system above)
    - The sign extension:
        - It's extending a value from some number of bits to a greater number of bits
        - It requires to copy the sign bit (1) into the additional HO bits in the new format
        - E.g., Assigning a smaller integer to a larger integer
        - It never fails but...
        - It isn't always free even if it seems easy
        - It may require more machine instructions than using data with 2 like-sized integer variables
        - It never fails
    - The zero extension:
        - It's the sign extension for unsigned values
        - It requires to copy 0 into the additional HO bits in the new format
        - It never fails but it isn't always free... see sign extension above
    - The sign contraction:
        - It's converting a value with some number of bits to the same value with a few number of bits
        - It can fail or generate a completly different number
        - E.g., sign contract of -448 from a 16-bit representation 0xFE40 to a 8-bit can fail or generate a different number 0x40 (+64)
        - C language simply stores the LO portion of the number into a smaller variable and throws away the HO portion 
        - The algorithm is:
        - 1st Check All HO bytes that we want to discard 
        - If any HO bytes contain a value different from either 0x00 or OxFF (sign), conversion can't be done
        - 2nd Check the HO bit of the resulting value
        - It must match every bit removed in the previous step (either 0s or 1s)
        - E.g., sign contract 16-bit values to 8-bit values:
        - 0xFF80 is possible (0x80): discarded byte is 0xFF, HO bit in the resulting number (80) is equal to bits removed (1s of 0xFF byte)
        - 0x0040 is possible (0x40): discarded byte is 0x00, HO bit in the resulting number (40) is equal to bits removed (0s of 0x00 byte)
        - 0x0100 isn't possible: discarded byte 0x01 isn't 0x00 nor 0xFF
        - 0xFF40 isn't possible: discarded byte 0xFF, HO bit in the resulting number (40) isn't equal to bits removed (1 of 0xFF byte)
    - Recommendations:
        - Use sign extension carefully as it isn't always free
        - Avoid sign contraction as much as possible
        - Compare the number to contract with upper and lower bounds values before contraction
        - In low-level languages such as C/C++, turn this into a macro (#define) otherwise our code may become unreadble
        - In high-level languages, a check may be done automatically, handle exceptions
- Saturation:

</details>

<details>
<summary>3. Binary Arithmetic and Bit Operations</summary>


</details>

<details>
<summary>10. References</summary>

- Books:
- Whitepapers:
- Articles:
- Talks:

</details>

---

## 2. Web Scalability for Startup Engineers:
Tips and Technics for Scaling your Web Application
By Artur Ejsmont, 2005

<details>
<summary>1. Core Concepts</summary>

- Most scalability issues can be boiled down to just few measurements: 
    - Handling more data. 
    - Handling higher concurrency levels 
    - Handling higher interaction rate. 
- Vertical Scalability: 
    - Adding more I/O capacity by adding more hard drives in Redundant Array of Independent Disks (RAID) arrays 
    - I/O throughput and disk saturation are the main bottlenecks in database servers 
    - Adding more derived and setting up a RAID array can help to distribute reads and write across more devices 
    - RAID 10 
    - Improving I/O access times but switching to Solid-State drives (SSD). SSD and Sequential Read/write: The difference isn’t that big 
    - Even For some No SQL databases such as Cassandra, SSD is less attractive because of this sequential write/read. Pp. 23
    - Reducing I/O operations by increasing RAM => this means more space for the file system cache and more working memory for the application
    - Improving network throughput upgrading network interfaces or installing new ones: 
        - Upgrade network provider’s connection or even upgrade your network adapters to allow greater throughput
    - Switching to servers with more processors or more virtual core (threads). 
    - Limits of Vertical Scaling: 
        - Cost: Cost of RAM of 256GB >>> RAM of 128GB ($18,000.00 >>> $3,000.00)
        - Database and applications limits due to Locks of share memory (lock contention)
- Isolation of services: 
    - It is moving different parts of the system to separate physical servers by installing each type of service on a separate physical machine
    - A service is an application like:
        - A web server (Apache for example) or 
        - A database engine (MySQL), 
        - File Transfer Protocol (FTP), 
        - DNS, cache, etc. 
    - Functional Partitioning: Divide your web app into smaller independent pieces and host them on separate machines 
        - Admin console where customers can manage their accounts: Machine 1, 
        - Main application business in Machine 2 
        - Each part of the app would use a different subdomain so that traffic would be directed to it based simply on the IP address of the web server 
- Content Delivery Network (CDN): 
    - It is a pScalability for Static Content 
    - A CDN is a hosted service that takes care of global distribution of static files (images, JavaScript, CSS, videos) 
    - It works as an HTTP proxy: 
        - Clients that need to download static files connect to one of the servers owned by the CDN provider instead of your servers 
        - If the CDN server doesn’t have the requested content yet, it asks your server for it and caches it from then on
    - This will reduce the amount of bandwidth your servers need
    - CDN would serve static content from the closest data center
- Horizontal Scalability: 
    - Distribution of the Traffic
    - Horizontally Scalable systems don’t need strong servers; they usually run on lots of  cheap “commodity” servers
    - But it requires a specific architecture (different from 1 server system architecture)
    - Areas where it is easiest to achieve horizontally Scalability: Web Servers, Caches
    - Area where it is more difficult: databases, other persistence stores
    - Round-Robin DNS service: 
        - It used to distribute traffic among web servers 
        - It is a DNS server feature allowing you to resolve a single domain name to one of many IP addresses 
        - Once a client received an IP address, it will only communicate with the selected server 
- Web Services Layer (7): 
    - It contains our application logic (business)
    - It is decoupled from the front-end layer (presentation and business logic are decoupled)
    - It makes "Functional Partitions" easier to create
    - The communication protocol used between front-end app. and web services is usually "Representational State Transfer" (REST) or Simple Object Access Protocol (SOAP) 
    - They should be kept Stateless: this make easier to scale them horizontally
    - They're often deployed in parallel to front-end application servers rather than hidden behind them (because they're exposed to 3rd-Parties and directly to customers)
- Additional Components: Since frond-end servers and web services are stateless, web applications often deploy: 
    - Object caches (5): used by bother frond-end application servers and web services
    - Message queues (6): used to postpone some of the processing to a later stage and to delegate work to queue worker machines. 
    - Queue Worker Machines (10): they're offline job-processing servers providing high-latency functions (such as asynchronous notifications and order fulfillment
- Data Persistence Layer: 
    - Most difficult layer to scale horizontally
    - It is an area of polyglot persistence: 
        - Where multiple data stores are used by the same company to leverage their unique benefits
        - It allows better scalability
- Application Architecture: 
    - Domain-Driven Design: It should evolve around the business model (it shouldn't revolve around a framework or any particular technology)
    - Front-end:  
        - The layer translating between the public interface and internal service calls
        - It will live in Front-end Servers (should be as dumb as possible, see Front-end layer above)
        - It should allow communication over HTTP (AJAX, web sessions, for example)
        - It should be as a plugin that could be removed, replaced or plugged back in, plug mobile front-end or command line front-end
        - It should be decoupled from the web service layer (business logic) 
        - It shouldn't be aware of any databases/3rd-party services
        - It could send events to message queues and use cache back ends to increase the speed and scaling
        - Whenever we can cache an entire (fragment of) HTML page, we save much more processing time than caching just the related database query 
    - Web Services: 
        - This is called: Service-Oriented Architecture (SOA)
        - I don't consider SOAP, REST, JSON or XML in the definition of SOA, as they are implementation details
        - It will live only in the web services layer
        - It is where most of the processing has to happen
        - It is where most of the business logic should live
        - Multi-Layers Architecture, Hexagonal Architecture, Event-Driven Architecture
    - Supporting Technologies:  
        - Message queues, application cache and search engine
        - They are usually 3rd party software products configured to work with our system
        - They could be considered as black boxes in the context of architecture
        - Data stores (Databases): they should also be considered as black boxes and as plug-and-play extensions
        - 3rd-party services: 
            - They are put outside of our system boundary 
            - They should be isolated by wrapping them in a layer of indirection (a good way to minimize the risk and our dependency on their availability)
    - Figure 1-10 High-level overview of the data center infrastructure:
        - ![Figure 1-10 High-level overview of the data center infrastructure](https://s3-us-west-2.amazonaws.com/hamidgasmi.com/Books/WebScalabilityforStartupEngineers/1-CoreConcepts-01.png)

</details>

<details>
<summary>2. Principles of Good Software Design</summary>

- Simplicity: Keep thing simple but no simpler
- Hide Complexity and Build Abstraction 
    - Local simplicity is achieved by ensuring that you can look at any single class/module/application and quickly understand what its purpose is and how it works 
        - When we look at a class:
            - We should be able to quickly understand how it works without knowing all the details of how other remote parts of the system work
            - We should only have to comprehend the class at hand to fully understand its behavior 
        - When we look at a module, 
            - We should be able to disregard the methods and think of the module as a set of classes 
        - When we look at an application, 
            - We should be able to identify key modules and their higher-level functions, 
            - but without the need to know the classes’ details 
        - When we look at a System, 
            - We should be able to see only our top level applications and identify their responsibilities 
            - without having to care about how they fulfill them 
    - At module level: No class should depend on more than few other interfaces or classes 
    - Avoid over engineering: 
        - This means building a solution that is much more complex than is really necessary
        - When we try to predict every possible use case and every edge case, we lose focus on the most common use cases
        - Good design allows you to add details and features later. 
        - Build iteratively. 
    - Test-Driven Development: 
        - Write tests first then implement the actual functionality. 
        - Since we write tests first, we wouldn’t add unnecessary functionality as it would require us to write tests for it as well. 
        - This allow us to focus on the output first (in other words the clients needs) before jumping on the solution. 
        - Models of Simplicity in Software Design: 
            - Grails, Hadoop and Google Maps API are a few models of simplicity (great places for further study). 
            - Grails: Read Grails in Action and Spring Recipes 
            - Hadoop: (mapReduce paradigm, Hadoop platform). Open source.  
            - To read: MapReduce white paper and Hadoop in Action. 
- Loose Coupling: to keep coupling between parts of our system as low as necessary  
    - Avoiding unnecessary coupling by generating public getters/setters: never do it 
        - Make them protected/public only when it is really necessary 
        - Hide as much as we can and expose as little as possible 
    - Avoiding unnecessary coupling: 
        - When clients of a module/class need to invoke methods in a particular order for the work to be done correctly 
        - Often it's caused by bad api design, such as the existence of initialization functions 
        - Clients of modules/classes shouldn’t have to know how you expect them to use our code 
    - Avoiding unnecessary coupling by avoiding circular dependencies between layers of the same application/modules/classes 
    - A diagram of a well-designed module should look more like a tree (directed a cyclic graph) rather than a social network graph 
    - E.g. of loose coupling: the design of Unix command-line programs and their use of pipes
    - E.g. of loose coupling: Simple Logging Facade for Java (SLF4J). 
        - To check it’s structure and to compare to Log4J and Java Logging API 
    - Books to read regarding loose coupling: 1,2,10,12,14,22,27,31 
    - DRY - Don’t Repeat yourself: 
        - Avoid reimplementing functions that exists: hashing functions, sorting, b-trees, model view controller (MVC) frameworks, database abstraction layers. 
        - Use libraries/tools/frameworks that do exist. Start 1st by searching online if there are any open-source alternative available out there. 
        - Use Design Patterns. Books: 1, 7,10,36,1 
        - Create web services to avoid duplicating a functionality into each application. 
    - Coding to Contract or coding to interface: 
        - By creating explicit contracts, we extract the thing that clients are allowed to see and depend upon. 
        - For methods, the contract is their signature. 
        - For classes, the contract is the public interface of the class: all accessible method and their signatures. 
        - For modules, the contract includes all the publicly available classes/interfaces and their public method signatures. 
        - For applications, the contract means some form of a web service API specification. 
        - We should depend on the contracts instead of implementation whenever we can. 
        - Interfaces should only depend on other interfaces and never on concrete classes. 
        - Classes should depend on interfaces as much as possible. 
    - Draw Diagrams: 
        - Use case, class diagram, module diagrams. 
        - UML books: 1,7,10 
        - Tool: Cloud based too: draw.io 
- Single Responsibility: 
    - Classes should have one single responsibility and no more. 
    - This will let our module/application/system decoupled and makes easy our unit tests.  
    - Guidelines: If a class breaks any of the guidelines below, it is a good indicator that we may need to revisit and potentially refactor it. 
    - Class Length: Keep a class length below 2 to 4 screens of code. 
    - Dependency: Ensure that our class depend on no more than 5 other interfaces/classes 
    - Ensure that a class has a specific goal/purpose. 
    - Class Comment: 
        - Summarize the responsibility of the class in a single sentence
        - Put it in a comment on top of the class name 
        - If we find it hard to summarize the class responsibility, it usually means that our class does more than one thing 
    - On the higher level, module or application we should 
        - limit the scope of each of them 
        - Isolate them from the rest of the system by using an explicit interface (a web service, for example). 
        - summarize its responsibility in 1 or 2 sentences 
    - Helpful Concepts: 
        - Design Patterns as strategy, iterator, proxy and adapter (books: 5, 7) 
        - Domaine-driven design (book: 2) 
        - Good software design books (1, 3, 7)
- Open-Closed Principle: 
    - It stands for "open for extension and closed for modification". 
    - It "... Maximizes the number of decisions not made." - Robert Martin
    - It allows us to leave more options available and delay decisions about the details. 
    - It reduces the need to change existing code. 
    - We should make the code flexible: Generic types, Interfaces, Comparators
- Dependency Injection: 
    - It provides references to objects that the class depends on, instead of allowing the class to gather the dependencies itself 
    - It is about knowing as little as possible: 
        - It allows classes to "not know" how their dependencies are assembled, 
        - Where they come from, or what actual implementation are fulfilling their contracts 
    - It can be summarized as:
        - Not using the "new" keyword in our classes and 
        - Demanding instances of our dependencies to be provided to our class by its clients. 
        - We could use a constructor-based dependency injection. 
    - It is limited to object created and assembly of its dependencies. 
    - E.g., Java Spring framework or Grails framework. 
- Inversion of Control (IOC): 
    - It is a broad principle that includes Dependency Injection principle.  
    - It is a method of removing responsibilities of a class to make it simpler and less coupler to the rest of the system. 
    - It is not having to know who will create and use your objects, how, or when. 
    - Instead of us being in control of creating instances of our objects and invoking methods, 
    - We become the creator of plugins or extensions to the framework. 
    - IOC will look at the web request and figure out which classes should be instantiated and which components should be delegated to
    - E.g., Spring, Symfony, Rails, Java EE containers. 
    - Components of a good IOC framework include the following: 
        - We can create plugins for our framework. 
        - Each plugin is independent and can be added or removed at any time. 
        - Our framework can auto-detect these plugins, or there is a way of configuring which plugin should be used and how. 
        - Our framework defines the interface for each plugin type and it isn't coupled to plugins themselves. 
- Designing for Scale: 
    - It comes with costs: 
        - 90% of startups fail; 
        - 9% succeed moderately and have limited scalability need; 
        - < 1% of them ever grow to the size that requires horizontal scalability 
    - Do not overengineer by preparing for scale that we will never use
    - Estimate first carefully the most realistic scalability needs of our system and design accordingly
    - Could be broken down to 3 basic design techniques: 
        - Adding more clones: adding indistinguishable components. 
        - Functional partitioning: dividing the system into smaller subsystem based on functionality. 
        - Data partitioning: keeping a subset of the data on each machine. 
- Adding More Clones: 
    - It is the easiest and most common scaling strategy. 
    - It is design our application in a way that would allow to scale by simply adding more clones (an copy of a component or a server). 
    - It is to be able to send each request to a random clone and get a correct result. 
    - Pay attention to where you keep the application state and how we propagate state changes among our clones. 
        - It works best for stateless services: it doesn't depend on the local state of the server so processing the request doesn't affect the way the service behaves).
        - Not stateless services are also using this technique. It is challenging though because we need to find ways to synchronize (by using replication for example) all clones and make them interchangeable. 
    - Adding more Web Servers Clones: 
        - It is to distribute the load equally among the all web servers. 
        - It is done by a load balancer. 
- Functional Partitioning: 
    - It is about creating subsystems out of different parts of our system. 
    - From infrastructure perspective, functional partitioning is the isolation of different server roles. 
    - We divide our data centers into different server types: object cache servers, message queue servers, queue workers, web servers, data store engines, and load balancers. 
    - It is the key practices of SOA architecture. 
    - Our services could share underlying infrastructure (data store servers, for example) or they could be hosted separately. By giving our services more autonomy, we promote coding to contract and allow each service to make independent decisions as to what components are required and what the best way to scale them out is. 
- Data partitioning: 
    - It is to partition the data to keep subsets of it on each machine instead of cloning the entire data set onto each machine. 
    - It is the most complex and expensive technique because we need to be able to locate the partition on which the data lives before sending queries to the servers and that queries spanning multiple partitions may become very inefficient and difficult to implement. 
    - Share-nothing principle:  
        - each server has its own subset of data, which it can control independently. 
        - Each node (server) is autonomous and propagation (replication) and locking aren't needed. 
- Design for Self-Healing (Availability, monitoring): 
    - It is designing software for high availability and self-healing. 
    - A system is considered available as long as it performs its functions as expected from the client's perspective. 
    - It doesn't matter if the system is experiencing internal partial failure as long as it does not affect the behavior that clients depend on. 
    - Systems are measured in the "numbers of nines":  
        - A system with availability of 2 nines is available 99% of the time (3.5 days of outage per year). 
        - A system with availability of 5 nines is available 99.999% of the time (5 minutes of outage per year). 
    - Failure must be considered a norm, not a special condition (hope for the best but prepare for the worst): with 1000 servers can easily give us a few failing servers every single day. There're other reason for failure such as power outages, network failures (timeouts for example) and human errors. 
    - E.g.:  
        - Netflix's Chaos Monkey. Netflix decided that the best way to prove that the system can handle failures is to actually cause them on an ongoing basis and observe how the system responds. 
        - Crash-Only concept: the system should always be ready to crash, and whenever it reboots, it should be able to continue to work without human interaction (CouchDB implement this concept and doesn't even provide any shutdown functionality: if you want to stop a CouchDB instance, you just have to terminate it). 
    - In practice, it is mainly about removing single points of failure and graceful failover. 
        - Single point of failure is any piece of infrastructure that is necessary for the system to work properly. 
        - E.g., DNS server (Domain Name System) if we have only one; database master server; file store server. 
        - Solution 1: Redundancy (if it is a good investment): is having more than one copy of each piece of data or each component of the infrastructure. 
        - Solution 2: without a redundancy, special attention + prepare a disaster recovery plan (business continuity plan) for all pieces of infrastructures. 
    - Self-Healing example: it is about minimizing the mean time to recovery and automating the repair process. An example is: Cassandra. 
        - Mean time to recovery is the key component of the availability equation. Mean time to failure / (mean time to failure + mean time to recovery) 
        - So if you can't control mean time to failure (if you're using cloud infrastructure for example), we need to focus on mean time to recovery. In fact, Cloud hosting services like AWS use cheaper hardware, trading low failure rates for low price.

</details>

<details>
<summary>3. Building the Front-End Layer</summary>
</details>

<details>
<summary>4. Web Services </summary>
</details>

<details>
<summary>5. Data Layer</summary>
</details>

<details>
<summary>6. Caching</summary>
</details>

<details>
<summary>7. Asynchronous Processing</summary>
</details>

<details>
<summary>8. Searching for Data</summary>
</details>

<details>
<summary>9. Other Dimensions of Scalability</summary>
</details>

<details>
<summary>10. References</summary>

- Books:
    - Web Operation: Keeping the Data on Time (John Allspaw, Jesse Robbins, 2010)
    - Beautiful Architecture: Leading Thinkers Reveal the Hidden Beauty in Software Design (Diomidis Spinellis, Georgios Gousious, 2009) 
    - The Art of Capacity Planning: Scaling Web Resources (John Allspaw, 2008)
    - Design Patterns: Elements of Reusable O-O Software (Eric Gamma, Richard Helm, Ralph Jonhson, John Vlissides, 1994)
    - Web Sites: Performance Best Practices for Web Developers (Steve Souders, 2009)
    - The Art of Lean Software Development (Curt Hibbs, 2009)
    - Patterns of Entreprise Application Architecture (Martin Fowler, 2002)
    - Team Geek (Brian Fitzpatrick, Ben Collins-Sussman, 2012)
    - RabbitMQ in Action: Distributed Messaging for Everyone (Alvaro Videla, Jason Williams, 2012)
    - The Art of Application Performance Testing: Help for Programmers and Quality Assurance (Ian Molyneaux, 2009)
    - Spring Recipes: A Problem Solution Approach (Gary Mak, 2008)
- Whitepapers:
- Articles:
- Talks:

</details>

---

## 3. Designing data-Intensive Applications:
 by Martin Kleppmann, 2017

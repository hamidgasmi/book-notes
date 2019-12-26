# Books Notes:

## Write Great Code, Volume 1:
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
		- Bit 1: ...
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

## Web Scalability for Startup Engineers:
Tips and Technics for Scaling your Web Application
By Artur Ejsmont, 2005

<details>
<summary>1. Core Concepts</summary>

- Most scalability issues can be boiled down to just few measurements: 
	- Handling more data 
	- Handling higher concurrency levels 
	- Handling higher interaction rate 
- Vertical Scalability: 
	- Adding more I/O capacity by adding more hard drives in Redundant Array of Independent Disks (RAID) arrays 
	- I/O throughput and disk saturation are the main bottlenecks in database servers 
	- Adding more derived and setting up a RAID array can help to distribute reads and write across more devices 
	- RAID 10 
	- Improving I/O access times but switching to Solid-State drives (SSD). SSD and Sequential Read/write: The difference isn’t that big 
	- Even For some No SQL databases such as Cassandra, SSD is less attractive because of this sequential write/read
	- Reducing I/O operations by increasing RAM => this means more space for the file system cache and more working memory for the application
	- Improving network throughput upgrading network interfaces or installing new ones: 
		- Upgrade network provider’s connection or even upgrade your network adapters to allow greater throughput
	- Switching to servers with more processors or more virtual core (threads) 
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
	- Horizontally Scalable systems don’t need strong servers; they usually run on lots of cheap “commodity” servers
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
	- Message queues (6): used to postpone some of the processing to a later stage and to delegate work to queue worker machines 
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
		- Good design allows you to add details and features later 
		- Build iteratively 
	- Test-Driven Development: 
		- Write tests first then implement the actual functionality 
		- Since we write tests first, we wouldn’t add unnecessary functionality as it would require us to write tests for it as well 
		- This allow us to focus on the output first (in other words the clients needs) before jumping on the solution 
		- Models of Simplicity in Software Design: 
			- Grails, Hadoop and Google Maps API are a few models of simplicity (great places for further study) 
			- Grails: Read Grails in Action and Spring Recipes 
			- Hadoop: (mapReduce paradigm, Hadoop platform). Open source
			- To read: MapReduce white paper and Hadoop in Action 
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
	- E.g. of loose coupling: Simple Logging Facade for Java (SLF4J) 
		- To check it’s structure and to compare to Log4J and Java Logging API 
	- Books to read regarding loose coupling: 1,2,10,12,14,22,27,31 
	- DRY - Don’t Repeat yourself: 
		- Avoid reimplementing functions that exists: hashing functions, sorting, b-trees, model view controller (MVC) frameworks, database abstraction layers 
		- Use libraries/tools/frameworks that do exist. Start 1st by searching online if there are any open-source alternative available out there 
		- Use Design Patterns. Books: 1, 7,10,36,1 
		- Create web services to avoid duplicating a functionality into each application 
	- Coding to Contract or coding to interface: 
		- By creating explicit contracts, we extract the thing that clients are allowed to see and depend upon 
		- For methods, the contract is their signature 
		- For classes, the contract is the public interface of the class: all accessible method and their signatures 
		- For modules, the contract includes all the publicly available classes/interfaces and their public method signatures 
		- For applications, the contract means some form of a web service API specification 
		- We should depend on the contracts instead of implementation whenever we can 
		- Interfaces should only depend on other interfaces and never on concrete classes 
		- Classes should depend on interfaces as much as possible 
	- Draw Diagrams: 
		- Use case, class diagram, module diagrams 
		- UML books: 1,7,10 
		- Tool: Cloud based too: draw.io 
- Single Responsibility: 
	- Classes should have one single responsibility and no more 
	- This will let our module/application/system decoupled and makes easy our unit tests
	- Guidelines: If a class breaks any of the guidelines below, it is a good indicator that we may need to revisit and potentially refactor it 
	- Class Length: Keep a class length below 2 to 4 screens of code 
	- Dependency: Ensure that our class depend on no more than 5 other interfaces/classes 
	- Ensure that a class has a specific goal/purpose 
	- Class Comment: 
		- Summarize the responsibility of the class in a single sentence
		- Put it in a comment on top of the class name 
		- If we find it hard to summarize the class responsibility, it usually means that our class does more than one thing 
	- On the higher level, module or application we should 
		- limit the scope of each of them 
		- Isolate them from the rest of the system by using an explicit interface (a web service, for example) 
		- summarize its responsibility in 1 or 2 sentences 
	- Helpful Concepts: 
		- Design Patterns as strategy, iterator, proxy and adapter (books: 5, 7) 
		- Domaine-driven design (book: 2) 
		- Good software design books (1, 3, 7)
- Open-Closed Principle: 
	- It stands for "open for extension and closed for modification" 
	- It "... Maximizes the number of decisions not made." - Robert Martin
	- It allows us to leave more options available and delay decisions about the details 
	- It reduces the need to change existing code 
	- We should make the code flexible: Generic types, Interfaces, Comparators
- Dependency Injection: 
	- It provides references to objects that the class depends on, instead of allowing the class to gather the dependencies itself 
	- It is about knowing as little as possible: 
		- It allows classes to "not know" how their dependencies are assembled, 
		- Where they come from, or what actual implementation are fulfilling their contracts 
	- It can be summarized as:
		- Not using the "new" keyword in our classes and 
		- Demanding instances of our dependencies to be provided to our class by its clients 
		- We could use a constructor-based dependency injection 
	- It is limited to object created and assembly of its dependencies 
	- E.g., Java Spring framework or Grails framework 
- Inversion of Control (IOC): 
	- It is a broad principle that includes Dependency Injection principle
	- It is a method of removing responsibilities of a class to make it simpler and less coupler to the rest of the system 
	- It is not having to know who will create and use your objects, how, or when 
	- Instead of us being in control of creating instances of our objects and invoking methods, 
	- We become the creator of plugins or extensions to the framework 
	- IOC will look at the web request and figure out which classes should be instantiated and which components should be delegated to
	- E.g., Spring, Symfony, Rails, Java EE containers 
	- Components of a good IOC framework include the following: 
		- We can create plugins for our framework 
		- Each plugin is independent and can be added or removed at any time 
		- Our framework can auto-detect these plugins, or there is a way of configuring which plugin should be used and how 
		- Our framework defines the interface for each plugin type and it isn't coupled to plugins themselves 
- Designing for Scale: 
	- It comes with costs: 
		- 90% of startups fail; 
		- 9% succeed moderately and have limited scalability need; 
		- < 1% of them ever grow to the size that requires horizontal scalability 
	- Do not overengineer by preparing for scale that we will never use
	- Estimate first carefully the most realistic scalability needs of our system and design accordingly
	- Could be broken down to 3 basic design techniques: 
		- Adding more clones: adding indistinguishable components 
		- Functional partitioning: dividing the system into smaller subsystem based on functionality 
		- Data partitioning: keeping a subset of the data on each machine 
- Adding More Clones: 
	- It is the easiest and most common scaling strategy 
	- It is design our application in a way that would allow to scale by simply adding more clones (an copy of a component or a server) 
	- It is to be able to send each request to a random clone and get a correct result 
	- Pay attention to where you keep the application state and how we propagate state changes among our clones 
		- It works best for stateless services: it doesn't depend on the local state of the server so processing the request doesn't affect the way the service behaves)
		- Not stateless services are also using this technique. It is challenging though because we need to find ways to synchronize (by using replication for example) all clones and make them interchangeable 
	- Adding more Web Servers Clones: 
		- It is to distribute the load equally among the all web servers 
		- It is done by a load balancer 
- Functional Partitioning: 
	- It is about creating subsystems out of different parts of our system 
	- From infrastructure perspective, functional partitioning is the isolation of different server roles 
	- We divide our data centers into different server types: object cache servers, message queue servers, queue workers, web servers, data store engines, and load balancers 
	- It is the key practices of SOA architecture 
	- Our services could share underlying infrastructure (data store servers, for example) or they could be hosted separately. By giving our services more autonomy, we promote coding to contract and allow each service to make independent decisions as to what components are required and what the best way to scale them out is 
- Data partitioning: 
	- It is to partition the data to keep subsets of it on each machine instead of cloning the entire data set onto each machine 
	- It is the most complex and expensive technique because we need to be able to locate the partition on which the data lives before sending queries to the servers and that queries spanning multiple partitions may become very inefficient and difficult to implement 
	- Share-nothing principle:
		- each server has its own subset of data, which it can control independently 
		- Each node (server) is autonomous and propagation (replication) and locking aren't needed 
- Design for Self-Healing (Availability, monitoring): 
	- It is designing software for high availability and self-healing 
	- A system is considered available as long as it performs its functions as expected from the client's perspective 
	- It doesn't matter if the system is experiencing internal partial failure as long as it does not affect the behavior that clients depend on 
	- Systems are measured in the "numbers of nines":
		- A system with availability of 2 nines is available 99% of the time (3.5 days of outage per year) 
		- A system with availability of 5 nines is available 99.999% of the time (5 minutes of outage per year) 
	- Failure must be considered a norm, not a special condition (hope for the best but prepare for the worst): with 1000 servers can easily give us a few failing servers every single day. There're other reason for failure such as power outages, network failures (timeouts for example) and human errors 
	- E.g.:
		- Netflix's Chaos Monkey. Netflix decided that the best way to prove that the system can handle failures is to actually cause them on an ongoing basis and observe how the system responds 
		- Crash-Only concept: the system should always be ready to crash, and whenever it reboots, it should be able to continue to work without human interaction (CouchDB implement this concept and doesn't even provide any shutdown functionality: if you want to stop a CouchDB instance, you just have to terminate it) 
	- In practice, it is mainly about removing single points of failure and graceful failover 
		- Single point of failure is any piece of infrastructure that is necessary for the system to work properly 
		- E.g., DNS server (Domain Name System) if we have only one; database master server; file store server 
		- Solution 1: Redundancy (if it is a good investment): is having more than one copy of each piece of data or each component of the infrastructure 
		- Solution 2: without a redundancy, special attention + prepare a disaster recovery plan (business continuity plan) for all pieces of infrastructures 
	- Self-Healing example: it is about minimizing the mean time to recovery and automating the repair process. An example is: Cassandra 
		- Mean time to recovery is the key component of the availability equation. Mean time to failure / (mean time to failure + mean time to recovery) 
		- So if you can't control mean time to failure (if you're using cloud infrastructure for example), we need to focus on mean time to recovery. In fact, Cloud hosting services like AWS use cheaper hardware, trading low failure rates for low price

</details>

<details>
<summary>3. Building the Front-End Layer</summary>

- Approaches to building web application:
	- Traditional multipage web application: 
		- Each request result is the browser reloading an entire page with the response received from the server
		- 2 decade old but still used for its simplicity
		- In the scope of this book
	- Single-page application (SPAs):
		- These execute the most business logic in the browser
		- They built in JavaScript (mainly)
		- Web servers often reduced to providing a data api and security layer
		- Any action on user interface, JavaScript code may initiate asynchronous calls to the server to load/save data
		- Based on the response received, JavaScript code replaces parts of the user interface
		- Popular with AngularJS and mobile app framework like Sencha Touch and Ionic
		- It isn’t in this book scope
	- Hybrid applications:
		- They way modern web application are built
		- Hybrid of 2 approaches above
- Managing State
	- State: it is any data The would have to be synchronized between servers to make them identical
	- Stateless: property of a service/server/object 
		- It doesn’t hold any data (state)
		- It makes instances of the same type interchangeable
		- It allows better Scalability
		- They delegate to external services/servers/objects any data that need to be synchronized across other servers/services/objects
	- Stateful:
		- It does hold data that other instances can’t access
		- Examples: user session data, local files, local memory state, locks
- Types of states stored in the frontend layer:
	- Managing HTTP Session:
	- HTTP protocol is stateless
	- There’re techniques to create a concept of a session on top of HTTP so that sever could recognize multiple requests from the same user as parts of same session
	- HTTP Sessions are implemented using cookies
	- To make services dealing with sessions stateless, there’re 3 ways:
		- Store session state in cookies: simple but could reduce performance if session size is big
		- Delegate the session storage to an external data store: Memcached, Redis, DynamoDB, Cassandra, Teracotta an object-clustering technology for Java JVM-based languages (Groovy, Scala, Java) Teracostta allows for transparent object access from multiple machines by introducing synchronization, distributed locking , and consistency guarantees
		- Use a load balancer that supports sticky sessions: web servers are stateful but the load balancer assigns a web server for each client and by injecting a load balancer cookie (additional) to the responses, it allows to keep track of each user is assigned to which server It isn’t recommended!
- Managing files: there’re 2 types of files
	- User-generated content being uploaded to our servers
	- Files generated by our system that need to be downloaded by the user:
		- Sometimes, we can get away with generating files on the fly and avoid storing them
		- But in many cases, we need to store the files in their exact form to ensure they will never change (invoices)
	- Technology: Simple Storage Service (S3 private or public bucket), Azure Blob Storage as the distributed file storage for our files. Cheap and a good fit in the early stages of development, when it may not make sense to store all files internally on our infrastructure
	- Public files: We should always use a content delivery network (CDN) provider to deliver public files to our users. By setting a long expiration policy on public files, we’ll allow CDN to cache them effectively forever. Then, the original servers will receive less traffic, thereby making them easier to scale
	- Private files: CDN isn’t used. Simple storage service (S3 private bucket, for example)
	- Technology 2: 
		- build our own file storage and delivery solution 
		- Look for open source components, but we’ll most likely need to build and integrate the system ourself (considerable amount of work) 
		- To use Redundant Array of Independent Disk (RAID) controllers and distribute files among your file servers (if lot of files to store but do not need a lot of throughput) 
		- Think about high availability issues (Redundancy on 1 drive may not be enough, to store files on multiple physical servers) 
		- Think about a lot of concurrent reads and writes on the same files
		- We may then need to partition a larger number of smaller file servers or use SSDs to prove higher throughput and lower random access times
		- To consider partitioning our files by uploading them to a randomly selected server and then storing the location of the file in the metadata database. As we need more servers, we can then use weighted random server selection, which allows us to specify the % of new files written to each node
		- High availability can be achieved by RAID controllers, or make our application copy each file to 2 servers at same time or use something like rsync to keep each of our “master” file servers in sync with the slave
	- Technology 3: opt for an “out of the box”, open-source data store to store our files. MongoDB allows us to store files within a MongoDB cluster by using GridFS 
		- GridFS is a MongoDB extension that splits files into smaller chunks and stores them inside MongoDB collections as if they were regular documents
		- Benefit: we only need to scale 1 system, and we can leverage partitioning and replication provided by MongoDB instead of implementing our own
		- It may add some performance overhead
	- Technology 3 Similar: Astyanax Chunked Object Store release as open-source by Netflix
		- It uses Cassandra as the underlying data store
		- This allows us to leverage Cassandra’s core features like transparent partitioning, redundancy, and failover
		- It then adds file storage-specific features on top of Cassandra’s data model
		- It optimized access by randomizing the download order of chunks to avoid hotspots within the cluster
		- It may add some performance overhead
		- Learn more about distributed file systems like google file system (GFS), Hadoop Distributed File System (HDFS), ClusterFS, and fully distributed and fault-tolerant design
- Managing Other Types of State:
	- E.g., local server cache, application in-memory state, resource locks
	- Frontend cache could be inconsistent and application are sensitive to that (eCommerce cached prices)
		- if they’re in each web server. For example: real-time bidding application. Complexity to coordinate invalidation of old cached data in all caches
		- Solution (Stateless): Shared Object Cache: so there is only 1 copy of each object and it could invalidate more easily
		- Some use cases aren’t sensitive to cache inconsistency. For example, online blogging plateform like Tumblr.com
	- Resource Lock:
		- They’re used to prevent race conditions and sync access shared resources
		- In some cases, they’re used in frontend layer to guarantee exclusive access to some resources 
		- Distributed Lock System is needed here: 
		- lock state should be pushed out of the application server (same way as http state)
			Create an independent service for locks
			Used this service on all web app servers to share locks globally
			Downside: increases latency
			Tech related to Java: Zookeeper with Curator library developed by Netflix. 47, L16, L17
			Tech related to PHP or Ruby: simple lock based on atomic operations of NoSQL data stores (add operation in Memcached)
			Locks could be implemented with Redis, MySQL and postgreSQL
- Components of the Scalable Front End
	- DNS(Domain Name System):
	- It is to find the server IP address
	- It is recommended to use a 3rd party hosted service
	- Amazon Tech: Route 53 (it is seamlessly integrated with amazon ecosystem such as Elastic Load Balancer)
	- Amazon Tech: latency based routing of Route 53 to direct clients to the closest data center. L20-L21-L22. It works as GeoDNS but the data center is selected based on the latency measurement It is more robust than GeoDNS as measurements could change over time, depending on network congestion, outages, and routing pattern 
	- GeoDNS: Data center is chosen based on location of the client
	- Other tech: easydns.com, dnsmadeeasy.com, dnsimple.com, dyn.com: they all offer similar level of service, latencies and uptime guarantees (L23-L34)
	- Load Balancers:
		- Before, DNS used to be used as load balancers (Round-Robin DNS). It is not recommended now a days since they aren’t transparent for clients (removing or adding a web server isn’t good since clients may have cached the IP address and will still use the old ones + propagation delays)
		- It is recommended to use a load balancer. DNS will have 1 IP address. No dns change is load balancers are removed/added
		- Benefit 1: hidden server maintenance:
			Take a web server out or the load balancer pool
			Wait for all active connections to « drain » and the safety shut down the web server without affecting even a single client
			Good for « rolling updates » and deploy new software across the cluster without any downtime
		- Benefit 2: Seamlessly increase capacity:
			Add more web servers at any time: transparent for clients
		- Benefit 3: efficient failure management
			Quickly Remove any faulty server and replace it if needed
		- Benefit 4: automated scaling:
			If cloud based hosting with ability to configure auto-scaling 
			Amazon, open stack, rackspace
			Add/remove servers could be done automatically throughout the day
		- Benefit 4: effective resource management:
			To use Secure Sockets Layer (SSL) offloading to reduce web servers needs
			Also called SSL termination
			It is a load balancer feature allowing us to handle all SSL encryption/decryption work on the load balancer and use unencrypted connections internally »
			It is recommended
	- Load Balancer as a Hosted Service:
		- If web app is hosted on AmazonEC2 or Azure: this solution is then recommended
		- Elastic Load Balancer (ELB): it is cheapest and simplest solution to start with (one less component to manage)
		- ELB scales transparently (done by Amazon)
		- ELB has built-in high availability. Do not worry about it becoming a single point of failure
		- ELB is cost effective with minimal up-front costs
		- ELB integrates with auto scaling and allows for automatic EC2 instance replacement in case of web server failures
		- ELB can perform SSL termination
		- ELB supports graceful back-end server termination by use of the connection draining feature
		- ELB can be fully managed using Amazon SDK so that we can automate LB config changes 
		- Downside of ELB: it needs some time to « warm up » and scale out. If you get sudden spikes in traffic that requires doubling capacity in a matter of seconds or minutes, ELB may be be too slow
		- They (ELB or Azure’s LB) allow internal load balancers
	- Self-Managed Software-Based Load Balancer:
		- It is an open-source software-based LB
		- Good If hosted on a cloud with LB or doesn’t meet our requirements
		- Tech Reverse Proxy such as Nginx
		- Specialized open-source LB product like HAProxy
		- Nginx is also a reverse HTTP proxy: it can cache http responses from our servers. This quality makes it a great candidate for internal web service LB
		- HAProxy: simple. It has built-in High-Availability support. Could be configured either as a layer 4 or layer 7 LB
			When it is set up to be a Layer 4 proxy, it doesn’t inspect higher level protocols to distribute the traffic. This allow HAProxy to be a LB for any protocol, not just HTTP/HTTPs
			When it is set up to be a Layer 7 proxy, it supports sticky sessions and SSL termination but needs more resource in this case
	- Hardware Load Balancer:
		- A dedicated device for LB
		- Good if we’re hosting a high-traffic website in our own physical data center
		- Tech: devices like Big-IP from F5 or Netscaler from Citrix
		- Hardware optimized for LB: L25-L26
		- Expensive
- Web Server:
	- They shouldn’t have much business logic
	- They should be treated as a presentation and web service results aggregation Layer
	- Tech: dynamic languages: PHP, Python, Groovy, Ruby, JavaScript (Node.js). They make frontend problems easy to solve such as SEO, AJAX, internationalization, and daily template changes
	- Not recommended tech: pure java or C or a constraining framework like Java EE, JSF, or CGI
	- It is beneficial to have the same technology stack across all of our layers
	- How to choose a tech stack: L27-L28
- Caching:
	- 1st integrate a CDN: we can use it to proxy all of the web requests coming to our servers, or we can use it solely for static files like images, CSS, and JavaScript files Not all web app can use a CDN to effectively cache entire pages
	- 2nd implement reverse proxies: CDN isn’t always possible: more personalized our content is and the more dynamic the nature of our web app, the harder it becomes to cache entire http responses. In this case, we may be better off deploying our own reverse proxy servers to gain more control over what is cached and for how long Reverse proxies tech: Varnish, Nginx
	- 3rd Store data directly in the Browser: modern browsers allow us to store up to megabytes of data
		- Good for web app for mobile clients or SPAs
	- 4th Object Cache on Web Servers: if requests can’t be satisfied from browser caches or reverse proxies
		- Tech: Redis, Memcached
		- Examples: Facebook w62, Printerest L31, Reddit L32, Tumblr L33
- Auto-Scaling:
	- Scale out or scale down automatically depending on the volume of the traffic and server load
	- It is a technique rather than a component of our infrastructure
	- By using the history volume of the traffic (days, weekends, time of the day), scale out or scale down accordingly
	- Tech: Amazon, azure, Rackspace
	- For Amazon requirement for auto-scaling:
		- EC2, 
		- Create a web server image (Amazon Machine Image -AMI
		- Configure AMI to be able to bootstrap itself and join the cluster automatically
		- Everything needed for a new EC2 instance to be fully functional web server must be in the AMI file itself, passed in by AMI launch parameters, or fetched from a remote data store
		- We can also use Amazon storage services like SimpleDB to store bootstrap configuration for EC2 instances
		- Next, we can create an auto-scaling group to define scaling policies. It is a logical presentation of our web server cluster and it can have policies like « add 2 servers when CPU utilization is over 80% »
		- Amazon has a powerful policy framework, allowing us to schedule scaling events and set multiple threshold for different system metrics collected by Cloud Watch (a hosted service used to gather system-level metrics) »
		- When we create an auto-scaling group, we can also decide to use Amazon ELB. Then new instances added to the auto-scaling group will be automatically added to the LB pool as soon as they complete boostrapping
		- Peak: good user experience?
		- Trough: in a cost-effective manner
- Deployment Examples:
	- AWS Scenario:
		- Good for young startups
		- Amazon CloudFront: Amazon’s CDN
		- S3 buckets: location to store static files. It could be public or private
	- Private Data Center: 
		- CDN and DNS is recommended to use a 3rd party providers
	- Private data center good if:
		- We may require more predictable latencies and throughput. Hosting on our own hardware let’s us achieve submilisecond server-to-server round trips
		- Hardware servers are much more powerful than virtual servers. We’ll need many fewer machines when migrating from the cloud to bare hardware
		- Buying servers up front is expensive for a small company, but once it’s network engineering team grows and is managing over hundred servers, it may become cheaper to have our own servers rather than renting « compute units » Vertical scaling is in general more effective when done using our own hardware (RAM, I/O, SSD drives are still very expensive in the cloud when compared to regular servers)
		- Strict legal restrictions
	- Shared files deployment: depends on the throughput and data size. It is recommended solutions where the application doesn’t have to know how files are stores and replicated 
		- FTP server (File Transfer Protocol): simple
		- SAN (Storage Area Network): sophisticated
		- NoSQL data stores: sophisticated
	- We’ll need to be able to serve these files via a CDN:
		- We’ll need to put a layer of web servers in front of our file storage to allow public access to our files via the CDN
	- Books: 8, 48, 49
		- Modern web framework Spring: 14
		- Grails: 22,34: they promote good web app architecture
		- Cloud hosting: 29, w34-w36,w38

</details>

<details>
<summary>4. Web Services </summary>

- Designing Web Services:
	- Web Services an an Alternative Presentation Layer:
		- Oldest approach: Build web app 1st and then add web services on top of it
		- Monolithic approach
		- Easy to implement. Could be good for MVPs since business model isn’t tested. But not good from scalability perdpective	
	- The API-First Approach:
		- It is a new approach
		- It implies designing and building api contracts first and then building clients consuming that API
		- It came 1st as a solution to the problem of multiple user interfaces
		- It is usually much more difficult in practice than it might sound
		- It is better suited for more stable companies than it is for early-phase startups
		- It may be a cleaner way to build software, but it requires more planning, knowledge about your final requirements, and engineering resources as it takes more experience to design a scalable web service and make it flexible at the same time
	- Pragmatic Approach:
		- Learn and fail fast: no api first approach
		- Then once the idea is tested, implement a web service
		- As a result of this mixed approach, we’re likely going to end up with a combination of tightly coupled small web applucation of little business value and a set of web services fulfilling more significant and well-defined needs
- Types of Web Services:
	- Function-Centric Services:
		- The concept is to be able to call functions’ or objects’ methods on remote machines without the need to know how they are implemented (language, architecture)
		- All arguments and data needed to execute that function would be serialized and sent over the network to a machine that is supposed to execute it… serialize the result and send it back over the network
		- In practice, this was much more difficult to implement across programming languages, Central Processing Unit (CPU) architectures, run-time environments as everyone had to agree on a strict and precise way of passing arguments, converting values, and handling errors… additionally, we have to deal with resource locking, security, network latencies, concurrency, and contracts upgrades
		- There were a few types: Common Object Request Broker Architecture (CORBA), Extensible Markup Language - Remote Procédure Call (XML-RPC), Distributed Component Object Model (DCOM), and Simple Object Access Peotocol (SOAP)
		- SOAP became the dominant technology
		- SOAP implementation is to use XML to describe and encode messages and the HTTP to transport request and responses between clients and servers (WSDL and XSD files)
		- Impraticable with web technologies like PHP
		- We can’t use HTTP-level caching with SOAP: because soap requests are issued by sending XML documents (request parameters and method names are contained in the XML document itself The Uniform Resource Locator URL doesn’t contain all the information needed to perform the remote procedure call)
		- The fact above makes SOAP much less scalable in applucation where the web service response could be cached by a reverse proxy
		- Some SOAP ws-* are stateful
		- Not recommended!
	- Ressource-Centric Services
		- Each resource can be treated as a type of object, and there are only few operations that can be performed on the objects (create, delete, update, and fetch)
		- REST Framework: an HTTP service with a routing mechanism to map the URL patterns to our code
		- Drawbacks: Clients won't be able to auto-generate the client code or discover the web service behavior
		- Benefit: it is less strict, allowing nonbreaking changes to be released to the server side without the need to recompile and redeploy the clients
		- A way to go around the problem of discoverability is for the service provider to build and share libraries for common languages Client code needs to be written only once and then can be reused by multiple customers/partners This puts burden on the service provider, but allows you to reduce onboarding friction and create even better abstraction than autogenerated code would
		- Security: the client would 1st authenticate (often using Oauth 2) and then provide the authentication token in HTTP headers of each requests 
		- REST services depend on HTTPS
		- They're stateless and public operations performed using GET method could be cached transparently by HTTP caches
- Scaling REST Web Services - Keep Service Machines Stateless:
		- Push all shared state out of our web service machines onto shared data stores like object caches, databases, and message queues (see previous chapter)
		- The only type that is safe to keep on our web service machines are cached objects, which don't need to be synchronized or invalidated in any way. By definition, cache is disposable and can be rebuilt at any point of time, so server failure doesn't cause any data loss
		- Use cases where we'll need to share some state between our web service machines:
			- Security: as our web service is likely going to require clients to pass some authentication token with each web service request (token to be validated on the web service side). The best approach is to use a shared in-memory object cache by mapping the authentication token and have each web service machine reach out for data needed at request time (this makes easy to invalidate it when users' permissions change)
			- How to support resource Locking: this could be handled by distributed lock systems (Zookeeper) or develop our own lock service using a data store of our choice. To make sure our web services scale, we should avoid resource locks for as long as possible and look for alternative ways to synchronize parallel processes (it is challenging and creates an opportunity for our service to stall or fail) Alternatives of locks are sometimes possible: use optimistic concurrency control where we check the state before the final update; use message queues as a way to decouple components and remove the need for resource locking
			- How to avoid deadlocks: If we decide to use locks, it is important to acquire them in a consistent order. For example, if we're locking 2 user accounts to transfer funds between them, make sure we always lock them in the same order (the account with an alphanumerically lower account # gets locked first)
			- Lock granularity: if we go with locks, we need to strike a balance between having to acquire a lot of fine-grained locks and having coarse lock that block access to large sets of data 
			- Fine-grained locks increase latency as we keep sending requests to the distributed locks service. They may also increase the complexity and losing clarity as to how locks are being acquired and from where => source for deadlocks
			- Few coarse locks: may reduce the latency and risk of deadlocks, but we can hurt our concurrency at the same time, as multiple web service threads can be blocked waiting on the same resource lock		
		- Application-level transactions: transactions can become difficult to implement, especially if we want to expose transactional guarantees in our web service contract and then coordinate higher-level distributed transactions on top of these services
			- A distributed transaction is a set of internal service steps and external web service calls that either complete together or fail entirely (it is similar to database transaction). The most common method of implementing distributed transactions is the 2 Phase Commit (2 PC) algorithm Stay away from distributed transactions and consider alternatives instead
			- Alternative 1: is to not support them at all
			- Alternative 2: is to provide a mechanism of compensating transaction. A compensating transaction can be used to revert the result of an operation that was issued as part of a larger logical transaction that has failed
- Scaling REST Web Services - Caching Service Responses:
		- It is about using the power of HTTP protocol caching (Get requests: Make sure 1st than it doesn't cause any state change or data updates... Even logs that could be useful for BI and advertising teams)
		- Be careful to web servers' local object caches. This could make each local cache to have its version
		- Identify web services which require authentication and which do not 
			- Authenticated REST endpoints could make each user to see different data based on their permissions. This means that the URL isn't enough to produce the response for the particular user
			- Instead the HTTP cache would need to include the authentication headers when building the caching key
			- This cache separation (a separate cache for each user) is good if our users should see different data, but it is wasteful if they should actually see the same thing
			- Authenticated REST resources by using HTTP headers like Vary
			- To leverage HTTP caching: make as many of our resources public as possible. This allows us to have a single cached object for each URL
- Scaling REST Web Services - Functional Partitioning:
		- It is a way to split a service into a set of smaller, fairly independent web services, where each of them focuses on a subset of functionality of the overall system
		- For example for an e-Commerce website, we could have two functional partitioning. 1st one for products and the second one for customers
		- The 2 functional partitioning could have differences in access patterns (More reads for products; more write for customers) => this result in different scalability needs
		- Does it make sense to use the same caching for both services?
		- Does it make sense to use the same type of data store?
		- Are both services equally critical to the business, and is the nature of the data they store the same?
		- Do we need to implement both of these vastly different web services using the same technology stack?
		- It would be best if we could answer "No" to these questions
		- Be careful of performing functional partitioning too early or creating too many partitions: when new use cases arise that require a combination of data and features present in multiple web services. For example, what if we need to built a recommendation service where we need data from both services (products and customers)

</details>

<details>
<summary>5. Data Layer</summary>

- Scalling a relational database engine (MySQL):
	- Replication: have multiples copies (clones) of the same data stored on different machines
		- Master-Slaves replication:
			- 1 Master dedicated for clients' writes requests (CUD: Creates, Updates, Deletes)
			- N Slaves dedicated for clients' read requests (R: Reads)
			- Synchronization (Master - Slave servers) is done through a log file called a binlog
			- The master writes CUD binlog statements in with a statement sequence # 
			- Each Slave server copies statements from binlog file to its a relay log file. Then statements are executed on slave's dataset 
			- Each slave server maintains the offset of the most recently seen statement from which to execute next statements
			- Master and its Slaves servers replication is asynchronous: The master server writes on its own binglog file regardless if any slave servers are connected or not. The slave servers know where they left off and make sure to get the right updates
			- Therefore, Master and Slaves servers are decoupled	
			- Replication lag: it takes some time to a data to be replicated on all slave servers. It should take < 1 second
			- Reads could be distributed on slave server (a Slave 1 for regular application queries, a Slave 2 for slow read queries such as reporting queries)
			- Use it to perform zero-downtime backups
			- Slave failure: If a slave server dies, we can simply take it out of rotation (stop sending requests to that server). It isn't a big concern
			- Master failure: MySQL doesn't support automatic failover or any mechanism of automated promotion of slave to a master. It is a manual process (find out a slave that is most up to date. Then reconfigure it to become a master. Make sure that the remaining slave servers are identical to the new master. Reconfigure them to replicate from the new master) 
			- We have a single source of truth semantics
		- Master-Master replication:
			- 2 master servers that could accept writes
			- Circular Replication: Master A replicates from Master B and Master B replicates from Master A
			- Binlog stores: the server name the statement was originally written to. This way, a statement isn't executed twice on the same server
			- Complex but it is a could be used as a faster solution for master server failover: In case of Master A failure, our application can be quickly reconfigured to direct all writes to Master B
			- Masters can also have the same number of slave servers. Our application can be then running with equal capacity using either of the groups
			- This could be used to upgrade our software/hardware with minimal downtime (upgrade one group at a time)
			- It isn't recommended to let the application write on both masters at same time: higher complexity and risk of data inconsistency Use auto-increment and UUID() in a specific way to make sure we never end up with the same sequence # being generated on both masters at the same time (see below) 
			- It isn't a scalability tool: master servers perform all writes (they don't do less) + additional writes relay log. Master servers have the same data size (more memory, more disk...)
			- We lose a single source of truth semantics
		- Ring Replication:
			- When 3 or more master servers
			- It is the worst replication variants discussed so far
			- Reduce availability (higher chance of one of servers failing) and makes failure recovery more difficult
			- This increases replication lag: each write jumps from master to master until it makes a circle (if 4 master servers and 0.5 second for each replication then: 1.5 second for all replication)
			- We lose a single source of truth semantics
		- Replication challenges:
			- Rebuilding a MySQL slave is manual process: In fact, MySQL doesn't allow us to bootstrap a slave from an empty database. We need a consistent backup of all of the data and the corresponding sequence # of the last statement that was executed. From there, the slave server could be started and it will begin catching up with the replication backlog. It could be long for busy databases
			- Master failure management: see Master-Slaves replication above
			- Replication lag:
				- How to make sure that a read request that happen after a write get the most recent data?
				- No matter which server we ask, there may be an update on its way from the master that can't be seen yet
				- This is called eventual consistency
				- To prevent this timing issue, one approach is to cache the data that has been written on the client side so that we wouldn't need to read the data that we have just written
			- It isn't a way to scale data set size (since the whole data set is cloned in all servers)
			- There're many ways in which we can break MySQL replication or end up with inconsistent data: 
				- Using functions that generate random numbers or 
				- Executing an update statement with a limit clause may result in a different value written on the master and on its slaves 
				- Once master and slaves get out of sync, we are in serious trouble, as all of the following CUD statements may also behave differently on each of the servers
				- Open-Source tools that can help us to discover such problems: pt-table-checksum, pt-table-sync
			- Deploy multiple levels of slaves to increase the read capacity:
				- A good way to Scale the number of read queries per second
	- Data Partitioning (Sharding):
		- It is to divide the data set into smaller pieces so that it could be distributed across multiple machines
		- It is a scaling tool since none of the servers would need to deal with the entire data set
		- The servers become independent from one another, as they share nothing (in the simple sharding scenario)
		- Choosing the Sharding Key: It a way to find the server (the shard) where the data is stored by using the sharding key: 
		- Mapping with an Algorithm that allow us to map the sharding key value to the actual server number ()
			- This will make difficult to scale up: if new servers are added, the mapping algorithm will change and return wrong server # 
			- For example, modulo based mapping, with 3 servers (0, 1, 2), user id = 8 would return server 2
			- But with 4 servers (0, 1, 2, 3), user id = 8 would return 0
		- The mapping should allow servers to end up with roughly the same amount of data
			- For example, Sharding based on country of origin won't assure an equal distribution
			- Some servers will have large data sets
			- Eventually, they will end up in situation where one bucket becomes so large that it can't be handled by a single machine any more!
		- Mapping with a separate database: 
			- We could look up at the server # based on the sharding key value
			- It fix the issue above of adding new shards
			- Data could be migrated incrementally from one server to another, one account at a time
			- To migrate a user, we need to lock their account, migrate the data, update data mapping table and then unlock the user account
			- Migrate top sales clients to separate dedicated database instances to give them more capacity (sales scenario)
			- Or in another scenario, if activity isn't a good thing, migrate top noise clients into a database with all noisy users to punish them for consuming too many resources
			- Implementation: We could use a MySQL database and use Master server that would be the source of truth + replicate that data to all of the shards + Cache to prevent any replication lag issue
		- Mapping modulo function + logical database number:
			- We use the modulo function to map from the sharding key value to the database #, but each database is just a logical MySQL database rather that a physical machine
			- Low cost and minimal increase of complexity
			- 1st, we decide how many machines we want to start with (let's say: 2)
			- Then, we forecast how many machines, we may need down the road (let's say: 32)
			- In the example above (2 initial machines and 32 forecasted ones), we create 16 databases on each of the physical server
			- In server A, we could name the databases: db-00 to db-15 and in server B: db-16 to db-31
			- We deploy the exact same schema to each of these databases so that they're identical (see schema below)
			- At the same time, we implement the mapping function in our code that allow us to find the database # and the physical server # based on the sharding key value
			- When we need to scale out, we simply split our physical server in two and modify our mapping server function
			- Data migrations aren't needed (save time)
			- Small downtime for scaling out
		- Ids aren't unique across shards (since they're generated using auto increment and databases don't know anything about one another) 
			- It may be acceptable
			- Or if we wanted to have a globally unique IDS, we could use: auto_increment_offset
		- Implementation:
			- It could be done on our application layer on top of any data store
			- Some data stores provide automatic sharding and data distribution out of the box
		- Challenges:
			- We can't execute queries spanning multiple shards (databases are independent). Execute on each shard then reprocess (merge, aggregate or group) on top of all sub results. For example, the product with TOP sales on each shard isn't necessary the product with TOP sales for the whole application!
			- We lose the ACID properties of our database as a whole. For example, if an update is needed on all shards, it could succeed on 1 share and it is committed but could fail on another shard and rolledback!
			- Get unique Ids globally: the application may need to enforce these rules 
				□ MySQL: use auto-increment with an offset to ensure that each shard generates different #
				□ Redis: use INCR command to increase the value of selected counter and return it in an atomic fashion. This way, we could have multiple clients requesting a new identifier in parallel and each of them would end up with a different value (guaranteeing global uniqueness)
			- Lot of extra work to scale out (add new servers): see above
			- A solution of all challenges above is to use a cloud hosting provider (Azure SQL Database Elastic Scale is set of libraries and supporting services that take responsibility for sharding, shard management, data migration, mapping, and even cross-shard query execution)
	- Put it all together:
		- Situation	How to scale
		- Many more reads than writes	1. Replication: Scale reads by adding read replica servers
			- They've the exact copy of the data that the master database has
			- The reads will be done then from the slave databases
			- The writes will be done in the master database
		- If it ins't enough	1. Functional partitioning: Split the database into 2 functional components
			- Example: 
			- Store all of the user-centric data on one database and the rest of the data in a separate database
			- At the same time, we could split the functionality of our web services layer into 2 independent web services. Each of them will deal with one of the servers above
			- Functional partitioning + Replication (situation 1 and 2):
				- A functional server could be replicated (Master/Slaves) if needed
				- A slave could be used as a backup: failover slave
- Scalling with No SQL:
	- Eric Brewer's CAP theorem: it is impossible to build a distributed system that would simultaneously guarantee Consistency, availability and Partition tolerance
	- Consistency ensures that all of the nodes see the same data at the same time
	- Availability guarantees that any available node can server client requests even when other nodes fail
	- Partition tolerance ensures that the system can operate even in the face of network failures where communication between nodes is impossible
	- CAP theorem was popularized under a simplified label: "Consistency, Availability, or Partition tolerance: Pick 2"
	- Eventual Consistency:
		- A property of a system where different nodes may have different versions of the data,
		- But where state changes eventually propagate to all of the servers
		- Conflicts could happen: an item updated in 2 different servers at the same time
		- A conflict could be resolved by "The most recent write wins" policy. It is simple but it may lead to some data being lost
		- Dynamo: A conflict could also be resolved by clients: all conflicting values are kept. When a client asks for that data, it would then return the conflicted version of the data, letting the client decide how to resolve the conflict. For example for Amazon shopping card, if there're 2 shopping cards version, the client service will merge them
		- Cassandra: employs self-healing strategies. 10% of reads sent to Cassandra nodes trigger a background read repair mechanism: After a response is sent to the client, the Cassandra node fetches the requested data from all of the replicas, compares their values, and sends updates back to any node with inconsistent or stale data
		- Some eventually consistent systems, such as Cassandra, allow clients to fine-tune the guarantees and tradeoffs made by specifying the consistency level of each query independently. We can choose which queries require more consistency and which ones can deal with stale data
	- Quorum Consistency: means the majority of the replicas agree on the result 
		- When we write using quorum consistency, the majority of the servers need to confirm that they have persisted our change
		- Reading using quorum means that the majority of the replicas need to respond so that the most up-to-date copy of the data can be found and returned to the client
		- Good to trade latency for consistency: we need to wait longer for the majority of the servers to respond but we get the freshest data
	- Faster Recovery to Increase Availability:
		- A good example is MongoDB
		- Data is automatically sharded and distributed among multiple servers. Each piece of data belongs to a single server, and anyone who wants to update data needs to talk to the server responsible for that data
		- Any time a severs becomes unavailable, MongoDB rejects all writes to the data that the server was responsible for
		- MongoDB supports replica sets and it is recommended to setup each of the shards as a replica set
		- In replica sets, multiple servers share the same data, with a single server being elected as a primary. Whenever the primary node fails, an election process is initiated to decide which of the remaining nodes should take over the primary role. Once the new primary node is elected, replication within the replica set resumes and the new primary node's data is replicated to the remaining nodes. This way, the window of unavailability can be minimized by automatic and prompt failover
		- MongoDB is "more" to CP: Consistency and Partition Tolerance. But: if the primary node failed before our changes got replicated to secondary nodes, our changes would be permanently lost	
	- Cassandra Topology:
		- It is built at facebook and could be seen as a merger of design patterns borrowed from BigTable (google) and Dynamo (Amazon)
		- All its nodes are functionally equal
		- It doesn't have a single point of failure, and all of its nodes perform the exact same functions 
		- Clients can connect to any of Cassandra's nodes 
		- When they connect to one, that node becomes the client's session coordinator
		- Clients send all of their requests to the session coordinator and the coordinator takes responsibility for all of the internal cluster activities like replication or sharding
		- Although Cassandra nodes have same function in the cluster, they are not identical: each node has a dataset it is responsible for
		- Cassandra data model is based on a wide column: we create tables and then each table can have an unlimited number of rows
		- Different rows may have different columns (fields) and they may live on different servers in the cluster
		- Downside (searching): to access data in any of the columns, we need to know which row are we looking for. And to locate the row, we need to know its row key
		- It supports a form of replication (different from replication in MySQL): there is no master-slave relationship between servers. Each copy of the data is equal important
		- Administration is done automatically: for example replacement of a node that is down because all the data that is in this server is also stored on multiple servers

</details>

<details>
<summary>6. Caching</summary>

- It is used in numerous technologies: 
	- CPU memory caches, 
	- hard drive caches, 
	- Linux OS file caches, 
	- DNS client caches, 
	- HTTP proxies and reverse proxies, and 
	- different types of application object caches
- Definition:
	- Each object in the cache is identified by its cache key
	- The only way to locate an object is by performing an extract match on the cache key
	- It is usually stored in memory
	- If we try to cache more objects than can fit in our cache, we’ll need to remove older objects before we can add new ones
	- Objects are cached for a predefined amount of time called Time To Live (TTL)
- Cache Hit Ration:
	- It is the single most important metric 
	- It is the number of requests served by the same cached result
	- E.g., if we can serve the same cached result to satisfy 10 requests on average, our cache hit ratio is 90%. This is because we need to generate each object once instead of 10 times
- 3 Factors that are affecting the cache hit ratio:
	- Cache key space:
		- It is the number of all possible cache keys our application could generate
		- Statistically, the more unique cache keys our application generates, the less chance we have to reuse ant one of them
		- We should always consider ways to reduce the number of possible cache keys
	- Cache Space:
		- Items # that we can store in our cache before running out of space
		- It depends directly on the average size of our objects and the size of our cache
		- The size is limited since the cache is usually in the memory
		- It is expensive (since the memory is expensive)
		- Replacing (evicting) objects reduces our cache hit ratio
	- Longevity (TTL):
		- It is how long, on average, each object can be stored in cache before expiring or being invalidated
		- The longer we can cache our object for, the higher the chance of reusing each cached object
		- However, be careful to stale data when data is cached for too long!		
	- Use cases with a high ratio of reads to writes are good candidates
	- Use cases with data updating very often may render cache useless
- Caching based on HTTP:
	- Its type is: read-through cache
	- This means that the application isn’t aware of the existence of this cache
	- It is positioned transparently between the application and its data sources 
	- Few extensions have been added to the HTTP specification, allowing different parts of the web infrastructure to cache HTTP responses
	- There’re many different HTTP headers related to caching, and
	- There’re HTML metatags related to caching,
	- This makes understanding HTTP caching a bit more difficult
	- Related technologies work as read-through caches: if the request can’t be satisfied from cache, the client connects to the read-through cache rather than to the origin server that generates the actual response
	- Read-Through cache are transparent to the client since it is using the same interface as the service
	- This give the flexibility of allowing to add layers (chains) of caching to the HTTP stack without needing to modify any of the clients
	- We can use the same http headers to control caching of our web, static resources such as images, and web service responses (REST-ful services)
	- HTTP Caching Headers:
		- "Pragma: no-cache": can be interpreted differently by different implementations
		- "Cache-Control": 
			- It was added to the HTTP 1.1 specification
			- It is supported by most browsers and caching packages
			- It allows to specify multiple options: no-cache, private, public, no-store, max-age, must-revalidate...
			- private: Indicates the result is specific to the user who requested it. Only browsers will be able to cache it because intermediate caches would not have the knowledge of what identifies a use)
			- public: Indicates the response can be shared between users as long as it has not expired. The response is either public or private
			- no-store: Indicates the response should not be stored/persisted on disks by any of the
			intermediate caches. The response can only be cached in memory. We should include this option any time our response contains sensitive user information so that neither the browser nor other intermediate caches store this data on disk
			- no-cache: Indicates the response should not be cached. Actually, it states that the cache needs to ask the server whether this response is still valid every time users request the same resource
			- max-age (not recommended): Indicates the TTL of the response. It can be expressed in a few ways, causing potential inconsistency It is less backwards compatible and depend on the Expires HTTP
			header instead (see below)
			- no-transform: Indicates the response should be served without any modifications such as CDN provider image transcoding to reduce their size
			- must-revalidate: Indicates that once the response becomes stale, it cannot be returned to clients without revalidation. Although caches may return stale objects under certain conditions, for example, if the client explicitly allows it or if the cache loses connection to the origin server. By using must-revalidate, we tell caches to stop serving stale responses no matter what. Any time a client asks for a stale object, the cache will then be forced to request it from the origin server
			- The Cache-Control header is rarely used by the clients (it is possible though) and it has slightly different semantics when included in the request. For example, the max-age option included in the requests tells caches that the client cannot accept objects that are older than max-age seconds, even if these objects were still considered fresh by the cache
		- Expires Header (recommended): 
			- It allows to specify an absolute point in time when the object becomes stale
			- A cached object is considered fresh as long as its expiration time has not passed
		- Vary header: 
			- It is to tell caches that we may need to generate multiple variations of the response based on some HTTP request headers
			- For example Vary: Accept-Encoding: indicates that we may return responses encoded in different ways depending on the Accept-Encoding header that the client sends to our web server. Clients who accept gzip encoding will get a compressed response, whereas others who cannot support gzip will get an uncompressed response
			
	- Cache Scenarios:
		- The best scenario is allowing our clients to cache a response forever. We may want to apply it for all of our static content (images, CSS, or JavaScript files)
- Custom object Cache:
	- It’s type is cache-aside cache
	- This means that the application is aware of its existence
	- The application actively uses it to store and retrieve objects (it isn’t transparent)
	- It could be imagined as key-values stores with support of object expiration
	- Client-Side Caches:
		- It is the cache that is located directly in the client's device
		- Did
- Scaling Object Caches:
	- Client-Side caches: can not be scaled, as there is no way to affect the amount of memory that browsers allow us to use
	- The web server local caches:
		- They’re usually scaled by falling back to the file system, as there is no other way to distribute or grow cache that, by definition, lives on a single server
		- In some scenarios, 
			- we may have a very Data pool where each cached object can be cached for a long period of time but objects are accessed relatively rarely
			- It may be good idea to use the local file system of our web servers to store cached objects as serialized files rather than storing them in the memory of the shared cache cluster
		- Accessing cached objects stored on the file system is slower, but it doesn’t require remote connections, 
		- So the web server becomes more independent and insulated from the other subsystem’ failures
		- File-based caches can also be cheaper because the disk storage is much cheaper than operating memory and we don’t need to create a separate cluster just for the shared object cache
		- Given the rising popularity of SSD drives, file system-based caches may be a cheap and fast random access memory (RAM) alternative
	- Distributed object caches:
		- It may scaled in different way depending on the technology used
		- Data partitioning (see Chapter 2 & 5) is the best way to go
		- It allows to scale the throughput and the overall memory pool of our cluster
		- Some tech’ like Oracle Coherence support data partitioning out of the box
		- Most open-source solutions like Memcached and Redis are simpler than that and rely on client-side partitioning 
			- For example, Memcached’s libMemcached client library’s built-in features to partition the data among multiple servers (each cache object is assigned to a single server without any redundancy or coordination between cache servers). This is an example of the share-nothing approach
			- Using consistent hashing is very important here (like libMemcached one):
			- All possible cache keys are represented as a range of numbers, with the beginning and end joined to create a circle
			- Then we place all of our servers on the circle, an equal distance from one another
			- Then we declare that each server is responsible for the cache keys sitting between it and the next server (moving clockwise along the server)
			- This way, by knowing the cache key and how many servers we have in the cluster, we can always find out which server is responsible for the data we’re looking for
			- Scaling our cache cluster horizontally (add a new server), causes each server to move slightly on the ring. This was, only a small subset of the cache keys get reassigned between servers, causing a relatively small cache-miss wave
			- A naive mapping approach like a modulo function that would map a cache key to a server # will reassign our cache keys (purging our entire cache) each time a server is added or removed from the cluster
	- Data Replication:
		- Some caches, like Redis, allow for master-slave replication deployment
		- Use case: one of our cache key became so “hot” that all web servers needed to fetch it concurrently, we could benefit from read replicas 
		- Rather than all clients needing the cache object connecting to a single server, we could scale the cluster by adding read-only replicas of each node in the cluster
- Caching Rules of Thumb:
	- Cache High Up the Call Stack:
		- The higher up the call stack we can cache, the more resources we can save
		- Client Caches (http and object caches): saved 100% of resources
		- HTTP reverse Proxies/CDN: saved 98% of resources
		- Web App Servers local caches / Distributed Caches: saves 75% of resources
		- HTTP Reverse Proxies: saved 66% of resources
		- Web Service Servers (local caches/Distributed Caches): saved 50% of resources
		- Main Data Store: Saved 0% of resources
		- The same principle applies within our application code. If we can cache an entire page fragment, we’ll save more time and resources than caching just the database query that was used to render this page fragment
		- Avoiding the web requests reaching our servers is the ultimate goal, but even when it isn’t possible, we should still try to cache as high up the call stack as we can		
	- Reuse Cache Among Users:
		- Always try to reuse the same cached object for as many requests/users as we can:
			- Reduce the number of possible cache key (see example below)
			- Increase our cache pool
			- Extend the TTL of our objects
		- Caching objects that are never requested again is simply a waste of time and resources
		- Use case:
			- A Web API which input is GPS location
			- For example, return all restaurant near a GPS location: 151.209146
			- The challenge is the GPS location will be different for 2 locations far by just a few steps
			- This is making the URL different and rendering our cache completely useless
			- A better approach would be to round the GPS location to 3 decimal places: 151.210
			- Each person within the same street block could reuse the same search limit
			- Instead of having billions of possible locations with the city limits, we reduce the number of possible locations and increase our chances of serving responses from cache
			- If the URL doesn’t contain user-specific data and isn’t personalized, there is no reason why we shouldn’t reuse the entire HTTP response by adding public HTTP caching headers
			- For Sydney city for example, this would reduce the number of possible user locations to less than 1 million. Having just 1 million possible responses would let us cache then efficiently in a reverse proxy layer or even a dynamic content CDN. Because restaurant details are unlikely to change rapidly, we should be able to cache service responses for hours without causing any business impact, increasing our cache hit ratio even further
		- If it isn't possible to cache entire pages, maybe it is possible to cache page fragments or use some other trick to reduce the number of possible cache key
	- Where to Start Caching:
		- To prioritize what needs to be cached 1st, use a simple metric of aggregated time spent generating a particular type of response
		- Aggregated time spent = time spent per request * number of request
	- Cache Invalidation Is Difficult:
		- It is difficult because cached objects are usually a result of computation that takes multiple data source as it input
		- Whenever any of these days sources changes, we should invalidate all of the cached objects that have used it as input
		- Also, each piece of content may have multiple representations, in which case all of them would have to be removed from cache 
	- E.g. an eCommerce website 1: We could cache all of the search queries that we send to the data store: query results for paginated product lists, keyword searches, category pages, and product pages
		- If we wanted to keep all the data in our cache consistent, anytime a product’s details change, we would have to invalidate all the cached objects that contain that product
		- But how will we find all the search results that might have contained a product without running all of these queries?
		- How will we construct the cache keys for all the category listings and find the right page offset on all paginated lists to invalidate just the right objects?
		- That is exactly the problem. There is no easy way to do that
	- E.g. an eCommerce website 2: 
		- The best alternative is to set a short TTL on our cached objects so that data won’t be stale too long 
		- It isn’t always efficient
	- E.g. an eCommerce website 3 (Hybrid solution): 
		- In cases where our business doesn’t allow data inconsistency, we may also consider caching partial results and going to the data source for the missing “critical” i formation
		- If our business required us to always display the exact price and stock availability, 
		- We could still Cache most of the product information and complex query results
		- The only extra work that we would need to do is fetch the exact stock and price for each item from the main data store before the rendering results
		- This solution isn’t perfect, it reduces the # of complex queries that data store needs to process and trades them for a set of much simpler “WHERE product_id IN (…)”
	- For more details on this subject, 2 white papers to read:
		- W6: explains a clever algorithm for query subspace invalidation, where we create “groups” of items to be invalidated
		- W62: describes how Facebook invalidates cache entries by adding cache keys to their MySQL replication logs. This allows them to replicate cache invalidation commands across data centers and ensures cache invalidation after a data store update
	- Recommendations:
		- Even if cache invalidation algorithms are interesting to learn, it isn’t recommended implementing them unless absolutely necessary
		- Avoid cache invalidation altogether for as long as possible and using TTL-based expiration instead
		- Short TTL or a hybrid solution (see above) is enough to satisfy the business needs

</details>

<details>
<summary>7. Asynchronous Processing</summary>

- In Synchronous processing is: 
	- A caller (function/thread/process/app) sends a request to get something done and it waits for a response before continuing its own work 
	- A called usually depends on the result of the operation and can’t continue without it
- Asynchronous processing:
	- It's about issuing requests that don’t block a caller's execution 
	- A called never waits idle for responses from services it depends upon 
	- Requests are sent and processing continues without ever being blocked 
	- It is about Fire-and-forget model
- Customers don’t like to wait:
	- It is dangerous to block user interactions, as users become impatient very quickly
	- Whenever a web app « freezes » for a second or two, users tend to reload the page, click on the back button, or simply abandon the application
	- Users of a corporate web app that provides business-critical processes are more forgiving because they have to get their job done
	- Users clicking around the Web on their way to work have no tolerance for waiting, and we are likely to lose them if our application forces them to wait
- E.g., AJAX:
	- Asynchronous processing doesn’t always have to be purely fire-and-forget 
	- It can allow for the results of the asynchronous call to be consumed by the caller using callbacks
	- AJAX is a good example of how it can be made simple for us
		- If an email message was triggered from JavaScript running in the browser,
		- We could handle its results by providing a callback function declared in place
	- A Callback: 
		- It is a construct of asynchronous processing where the caller doesn’t block while waiting for the result of the operation, but provides a mechanism to be notified once the operation is finished
		- It is a function, an object, or an endpoint that gets invoked whenever the asynchronous call is completed
		- It is common in user interface environments, as it allows tasks to execute in the background, parallel to user interactions
- Queue:
- QueueConsumer:
- Message Consumer:
	- It could be multithreaded
- They’re decoupled
- We can have all the executions above in separate servers as different processes
- Nonblocking I/O:
	- It refers to input/output operations that do not block the client code’s execution
	- When using nonblocking I/O libraries, our code doesn’t wait while we read data from disk or write to a network socket
	- Anytime we make a nonblocking I/O call, we provide a callback function, which becomes responsible for handling the output of the operation
- Message Queues:
	- Even if our application or programming language language runtime doesn’t support asynchronous processing, we can use message queues to achieve asynchronous processing
	- It is a component that buffers and distributes asynchronous requests
	- In the message queue context, messages are assumed to be one-way, fire-and-forget requests
	- We can think of a message as a piece of XML or Json with all of the data that is needed to perform the requested operation
	- They’re created by message producers
	- They’re delivered to message consumers who perform the asynchronous action on behalf of the producer
	- Message producers and consumers in scalable systems usually:
		- They run as separate processes or separate execution threads
		- They’re often hosted on different servers and can be implemented in different technologies to allow further flexibility
		- They can independently of each other
		- They’re only coupled by the message format and message queue location
	- Independently from producers, the message queue arranges messages in a sequence to be delivered to consumers
	- The queue benefits:
		- Nonblocking communication between producer and consumer. Producers don’t have to wait for the consumers to become available
		- Producers and Consumers can be scaled separately
			- We can add more producers at any time without overloading the system
			- We can also increase the number of consumers independently from producers and can be hosted in separate machine
- Message Producers:
	- They’re called also message publisher
	- Message publishing refers to the action of sending a message by producers
	- It is up to the developer to decide where producers should execute and when they should publish their messages
	- Application can have multiple producers, publishing the same type of message in different parts of the codebase
	- The message format is the contract between producers and consumers: it is important to define it well and validate it strictly
	- Using XML or Json format allows for producers and consumers to be implemented in different languages and work independently of one another 

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


## Big Data:
Principles and best practices of scalable real-time data systems
by Nathan Marz and James Warren, 2015

<details>
<summary>1. A new paradigm for Big Data</summary>

- Scaling with a traditional database:
- NoSQL is not a panacea 
- First principles:
	- Information type:
		- Derived information: from other pieces of information
		- Data: rawest information which isn't derived from any other information
	- Function: anything we could ever imagine doing with data can expressed as a function that takes in all the data we have as input 
- Desired properties of a Big Data System: 
	- Robustness and fault tolerance: 
		- Systems need to behave correctly despite machines going down randomly, 
		- Systems need to behave correctly despite the complex semantics of consistency in distributed databases, etc. 
		- Part of making a Big data system robust is avoiding these complexities so that we can easily reason about the system
		- Humain-fault tolerant (an oft-overlooked property): 
			- In production it’s inevitable that someone will make a mistake
			- With immutability and recomputation into the core of data system, the system will be innately resilient to human error by providing a clear and simple mechanism for recovery 
	- Low latency reads and updates:
		- Read latency requirement: very low: between a few milliseconds to a few hundred milliseconds
		- Update latency requirements very between applications: 
			- Some applications require updates to propagate immediately 
			- Other applications: a latency of a few hours is fine
			- We need to be able to achieve low latency reads and updates without compromising the robustness of the system
	- scalability:
		- It’s the ability to maintain performance in the face of increasing data or load by adding resources to the system
		- The Lambda Architecture is horizontally scalable across all layers of the system stack: scaling is accomplished by adding more machines
	- Generalization: 
		- The Lambda Architecture is based on functions of all data
		- The Lambda Architecture generalizes to all applications, whether financial management systems, social media analytics, scientific apps. Social networking, etc.
	- Extensibility: 
		- Extensible systems allow functionalities to be added with a minimal development cost... 
		- E.g., Part of making a system extensible is making it easy to do large-scale migrations
	- Ad hoc queries:
	- Minimal maintenance:
		- Maintenance is a tax on developers
		- It's the work required to keep a system running smoothly
		- It includes anticipating when to add machines to scale, keeping processes up and running, and debugging anything that goes wrong in production
		- Choose components that have as little implementation complexity as possible: 
		- Rely on components that have simple machanisms underlying them: simple algorithms and simple components
		- The more complex a system, the more likely something will go wrong
		- The Lambda Architecture pushes complexity out of the core components and into pieces of the system whose outputs are disardable after a few hours
	- Debuggability
		- To be able to trace
		- The Lambda Architecture handles it through the functional nature of the batch layer and by preferring to use recomputation algorithms when possible
- The problems with fully incremental architectures:
	- Characteristics 
		- It uses of read/write dbs
		- It maintains db state incrementally
		- It's a lot more fundamental than just relational vs. non-relational
		- E.g., Counting pageviews would be to process a new pageview by adding one to the counter for its URL
		- It's a Familiar complexity: People got used to it; they don't realize it's possible to avoid its problems with a different architecture
	- Operational compexity: online compaction
		- Parts of the index become unused => they take space => it needs to be reclaimed to prevent the disk for filling up
		- Compaction is too expensive: it requires high CPU and disks; It lowers the performance during the compaction period
		- Cascading failure: if too many machines compact simultaneously, the load they were supporting will have to be handled by other machines in the cluster
	- Extreme complexity of achieving eventual consistency:
		- A Highly Available (HA) system allows for queries and updates even in the presence of machine or partial network failure
		- A consistent system returns results that take into account all previous writes
		- HA competes with consistency
		- CAP theorem shows that is's impossible to achive HA and consistency in the same system in the presence of network partitions
		- HA system sometimes returns stale results during a network partitions
		- Eventual consistency requires an amazing amount of complexity
	- Lack of human-fault tolerance:
		- It's a synchronous system: it makes updates directy to the database => it leads to data corruption
		- It's solved by adding an event log layer but it doesn't resolve underlying complexities
- Lambda Architecture
- Recent trends in technology

</details>

<details>
<summary>2. Batch layer: Data model for Big Data</summary>
</details>

<details>
<summary>3. Batch layer: Data model for Big Data: Illustration</summary>
</details>

<details>
<summary>4. Batch layer: Data storage on the batch layer</summary>
</details>

<details>
<summary>5. Batch layer: Data storage on the batch layer: Illustration</summary>
</details>

<details>
<summary>6. Batch layer</summary>
</details>

<details>
<summary>7. Batch layer: Illustration</summary>
</details>

<details>
<summary>8. Batch layer: An example batch layer: Architecture and algorithms</summary>
</details>

<details>
<summary>9. Batch layer: An example batch layer: Implementation</summary>
</details>

<details>
<summary>10. Serving layer</summary>
</details>

<details>
<summary>11. Serving layer: Illustration</summary>
</details>

<details>
<summary>12. Speed layer: Realtime views</summary>
</details>

<details>
<summary>13. Speed layer: Realtime views: Illustration</summary>
</details>

<details>
<summary>14. Speed layer: Queuing and stream processing</summary>
</details>

<details>
<summary>15. Speed layer: Queuing and stream processing: Illustration</summary>
</details>

<details>
<summary>16. Speed layer: Micro-batch stream processing</summary>
</details>

<details>
<summary>17. Speed layer: Micro-batch stream processing: Illustration</summary>
</details>

<details>
<summary>18. Speed layer: Lambda Architecture in depth</summary>
</details>

---

## Designing data-Intensive Applications:
 by Martin Kleppmann, 2017

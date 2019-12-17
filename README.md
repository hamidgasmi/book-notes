# Books Notes
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
- Signed and Unsigned Numbers: 
    - The two’s complement numbering system: 
        - It uses the HO bit as a sign bit 
        - With n digits, we can represent -2^[n -1] to +2^[n-1] - 1 
        - E.g., with a 16-bit number 0x8000 (1000_0000_0000_0000b): it's the smalled 16-bit negative number
    - Negation Algorithm: 
        - Invert all the bits in the number 
        - Add +1 and Ignore any overflow 
        - E.g. 1, 0x0005 (+5) => (Inversion) 0xFFFA =>(+1) 0xFFFB (-5) 
        - E.g. 2, 0xFFFB (-5) => 0x0004 => 0x0005 (+5) 
        - E.g. 3, 0x8000 (smallest negative number) => 0x7FFF => 0x8000 (-32,768) => smallest negative number in n-bit doesn't have a positive representation (see n-bit representation limit above) 
- Some useful Properties of Binary Numbers: 
    - If LO bit = 1 in a binary (integer) => odd 
    - If LO bit = 0 in a binary (integer) => even 
    - If the LO n bit of a binary number all contain 0 => the number is evenly divisible by 2^n 
    - If a binary value contains a 1 in bit position n and 0s everywhere else => it’s equal to 2^n 
    - If a binary value contains all 1s from Bit 0 to bit n - 1 and 0 elsewhere => it’s equal to 2^n - 1 

</details>

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
 
## 3. Designing data-Intensive Applications:
 by Martin Kleppmann, 2017

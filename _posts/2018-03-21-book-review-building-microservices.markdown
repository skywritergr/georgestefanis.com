---
layout: post
title: "Book review: Building microservices"
date: 2018-03-21
categories: blog
comments: true
excerpt: "I’ve been working around Microservices for years, but only recently I did start wondering about how everything ties together. My experience at TransferWise helped me to start looking deeper in this world."
---
I’ve been working around Microservices for years, but only recently I did start wondering about how everything ties together. My experience at TransferWise helped me to start looking deeper in this world.

{% include image.html url="https://images.gr-assets.com/books/1403186979l/22512931.jpg" title="Building micro services cover" %}

More specifically, as we move from a monolith to micro services and huge scaling I wanted to know how all the different tools and processes came to be. This book is exactly what I was looking for to get answers about all that.

The book talks about a variety of things, ranging from CI, CD, monitoring, security to scaling and breaking the monolith. It’s a great introduction to micro services ecosystem and a great first point of getting deeper in the rabbit hole. 

I really enjoyed it and totally recommend it. [Building Microservices at goodreads](https://www.goodreads.com/book/show/22512931-building-microservices?ac=1&from_search=true)
 
## Notes
The entire book was very good, but some chapters were more informative, for me, than others. As you can see from the notes below I really got a lot out of Chapter 11 that talks about scaling services and Chapter 8 that talks about monitoring. Chapter 9 about Security was good too.

The notes below are separated in the chapters they belong. It doesn’t mean they are the only interesting part of the chapter or the book, it just what drew my attention more. Things I thought I need to remember for the future.

### Chapter 2, The Evolutionary Architect
* Defining clear attributes that each service should have is one way of being clear as to where that balance sits.
* One of the key ways to identify what should be constant from service to service is to define what a well-behaved, good service looks like. What is a “good citizen” service in your system? What capabilities does it need to have to ensure that your system is manageable and that one bad service doesn’t bring down the whole system?
* Principles are rules you have made in order to align what you are doing to some larger goal, and will sometimes change
* Our practices are how we ensure our principles are being carried out. They are a set of detailed, practical guidance for performing tasks. They will often be technology-specific, and should be low level enough that any developer can understand them.
* architects have a duty to ensure that the system is habitable for developers too.
* Our city—the system—needs to be a good, happy place for everyone who uses it. One thing that people often forget is that our system doesn’t just accommodate users; it also accommodates developers and operations people who also have to work there

### Chapter 3, How to Model Services
* These modular boundaries then become excellent candidates for microservices. In general, microservices should cleanly align to bounded contexts
* When you’re starting out on a new codebase, this is probably a good place to begin. So once you have found your bounded contexts in your domain, make sure they are modeled within your codebase as modules, with shared and hidden models.
* By thinking clearly about what models should be shared, and not sharing our internal representations, we avoid one of the potential pitfalls that can result in tight coupling

### Chapter 4, Integration

* The example of a client trying to be as flexible as possible in consuming a service demonstrates Postel’s Law (otherwise known as the robustness principle), which states: “Be conservative in what you do, be liberal in what you accept from others.”
* This pattern—of implementing a reader able to ignore changes we don’t care about—is what Martin Fowler calls a Tolerant Reader.
* My general rule of thumb: don’t violate DRY within a microservice, but be relaxed about violating DRY across all services

### Chapter 5, Splitting the Monolith

* If the transaction manager goes down, the pending transactions never complete.
* This approach relies on all parties halting until the central coordinating process tells them to proceed. This means we are vulnerable to outages.
* The most common algorithm for handling distributed transactions—especially short-lived transactions, as in the case of handling our customer order—is to use a two-phase commit.
* In many ways, this is another form of what is called eventual consistency. Rather than using a transactional boundary to ensure that the system is in a consistent state when the transaction completes, instead we accept that the system will get itself into a consistent state at some point in the future.
* To see these database-level constraints, which may be a stumbling block, we need to use another tool to visualize the data. A great place to start is to use a tool like the freely available SchemaSpy, which can generate graphical representations of the relationships between tables.

### Chapter 6, Deployment

* Automate everything, and if the technology you have doesn’t allow this, get some new technology!
* Next, if possible, move to a single-service per host/container.
* you need one CI build per microservice
* First, focus on maintaining the ability to release one service independently from another, and make sure that whatever technology you select supports this.
* The tool I’ve used the most for this is Fabric, a Python library designed to map command-line calls to functions, along with good support for handling tasks like SSH into remote machines. Pair it with an AWS client library like Boto, and you have everything you need to fully automate very large AWS environments.

### Chapter 7, Testing
* A test suite with flaky tests can become a victim of what Diane Vaughan calls the normalization of deviance—the idea that over time we can become so accustomed to things being wrong that we start to accept them as being normal and not a problem

### Chapter 8, Monitoring
* Track inbound response time at a bare minimum. Once you’ve done that, follow with error rates and then start working on application-level metrics.
* As always with standardization, tools can help. As I’ve said before, the key is making it easy to do the right thing—so why not provide preconfigured virtual machine images with logstash and collectd ready to go, along with application libraries that let you talk to Graphite really easily?
* One approach that can be useful here is to use correlation IDs. When the first call is made, you generate a GUID for the call. This is then passed along to all subsequent calls,
* This fake event we created is an example of synthetic transaction. We used this synthetic transaction to ensure the system was behaving semantically, which is why this technique is often called semantic monitoring.
* I would strongly suggest having your services expose basic metrics themselves. At a bare minimum, for a web service you should probably expose metrics like response times and error rates
* Graphite is one such system that makes this very easy. It exposes a very simple API and allows you to send metrics in real time. It then allows you to query those metrics to produce charts and other displays to see what is happening
* Kibana is an ElasticSearch-backed system for viewing logs,
* Instead, we’re looking to use specialized subsystems to grab our logs and make them available centrally. One example of this is logstash, which can parse multiple logfile formats and can send them to downstream systems for further investigation.
* With just a few hosts, though, we can use tools like ssh-multiplexers, which allow us to run the same commands on multiple hosts. A big monitor and a grep “Error” app.log later, and we can find our culprit.
* We may even get advanced and use logrotate to move old logs out of the way and avoid them taking up all our disk space.
* If we want to run our own monitoring software, we could use something like Nagios to do so, or else use a hosted service like New Relic.

### Chapter 9, Security
* Start with only running services as OS users that have as few permissions as possible,
* There is a type of vulnerability called the confused deputy problem,
* I’d go as far as to say just look at how Amazon does this for S3 and copy its approach
* Second, this is a pattern, not a standard, and thus there are divergent ways of implementing it. As a result, there is a dearth of good, open, and usable implementations of this approach.
* There are three downsides to this approach. First, both the client and server need a shared secret that needs to be communicated somehow. How do they share it?
* With HMAC the body request along with a private key is hashed, and the resulting hash is sent along with the request. The server then uses its own copy of the private key and the request body to re-create the hash. If it matches, it allows the request.
* An alternative approach, as used extensively by Amazon’s S3 APIs for AWS and in parts of the OAuth specification, is to use a hash-based messaging code (HMAC) to sign the request.
* Another downside is that traffic sent via SSL cannot be cached by reverse proxies like Varnish or Squid.
* Authorization is the mechanism by which we map from a principal to the action we are allowing her to do.
* Generally, when we’re talking abstractly about who or what is being authenticated, we refer to that party as the principal.
* authentication is the process by which we confirm that a party is who she says she is.

### Chapter 10, Conway’s Law and System Design
* Melvin Conway’s paper How Do Committees Invent, published in Datamation magazine in April 1968, observed that: 
* Any organization that designs a system (defined more broadly here than just information systems) will inevitably produce a design whose structure is a copy of the organization’s communication structure.

### Chapter 11, Microservices at Scale
* Swagger lets you describe your API in order to generate a very nice web UI that allows you to view the documentation and interact with the API via a web browser.
* systems that are happy to cede consistency to keep partition tolerance and availability are said to be eventually consistent;
* Partition tolerance is the system’s ability to handle the fact that communication between its parts is sometimes impossible.
* Availability means that every request receives a response
* Consistency is the system characteristic by which I will get the same answer if I go to multiple nodes
* You may well have heard about the CAP theorem
* At its heart it tells us that in a distributed system, we have three things we can trade off against each other: consistency, availability, and partition tolerance. Specifically, the theorem tells us that we get to keep two in a failure mode.
* If you are lucky enough to have fully automatable provisioning of virtual hosts, and can fully automate the deployment of your microservice instances, then you have the building blocks to allow you to automatically scale your microservices.
* Caching can be used to implement resiliency in case of failure. With client-side caching, if the downstream service is unavailable, the client could decide to simply use cached but potentially stale data. We could also use something like a reverse proxy to serve up stale data.
* CDNs like AWS’s CloudFront or Akamai can ensure that requests are routed to caches near the calling client
* Reverse proxies like Squid or Varnish can sit transparently on the network between client and server, storing and expiring cached content as required
* When issuing the subsequent GET request, we can pass in a If-None-Match: o5t6fkd2sa. This tells the server that we want the resource at the specified URI, unless it already matches this ETag value
* let’s imagine we fetch a customer record, and its ETag comes back as o5t6fkd2sa.
* An ETag is used to determine if the value of a resource has changed. If I update a customer record, the URI to the resource is the same, but the value is different, so I would expect the ETag to change
* We also have the option of setting an Expires header,
* First, with HTTP, we can use cache-control directives in our responses to clients. These tell clients if they should cache the resource at all, and if so how long they should cache it for in seconds.
* In a situation where you have multiple types of clients, a server-side cache could be the fastest way to improve performance.
* With server-side caching, everything is opaque to the clients; they don’t need to worry about anything.
* Having a proxy between the client and server does introduce additional network hops, although in my experience it is very rare that this causes problems
* With proxy caching, everything is opaque to both the client and server. This is often a very simple way to add caching to an existing system
* Client-side caching can help reduce network calls drastically, and can be one of the fastest ways of reducing load on a downstream service
* Caching is a commonly used performance optimization whereby the previous result of some operation is stored, so that subsequent requests can use this stored value rather than spending time and resources recalculating the value.
* The Command-Query Responsibility Segregation (CQRS) pattern refers to an alternate model for storing and querying information. With normal databases, we use one system for performing modifications to data and querying the data. With CQRS, part of the system deals with commands, which capture requests to modify state, while another part of the system deals with queries.
* The replication from the primary database to the replicas happens at some point after the write. This means that with this technique reads may sometimes see stale data until the replication has completed. Eventually the reads will see the consistent data. Such a setup is called eventually consistent,
* A service could direct all writes to the single primary node, but distribute reads to one or more read replicas
* In a relational database management system (RDBMS) like MySQL or Postgres, data can be copied from a primary node to one or more replicas.
* Another model is to make use of read replicas.
* scaling for reads is much easier than scaling for writes. Caching of data can play a large part here,
* A more common model would be using a standby. All data written to the primary database gets copied to the standby replica database. If the primary goes down, my data is safe, but without a mechanism to either bring it back up or promote the replica to the primary, we don’t have an available database, even though our data is safe.
* Straight off, it is important to separate the concept of availability of the service from the durability of the data itself. You need to understand that these are two different things,
* The need to change our systems to deal with scale isn’t a sign of failure. It is a sign of success.
* A VLAN is a virtual local area network, that is isolated in such a way that requests from outside it can come only via a router, and in this case our router is also our SSL-terminating load balancer. The only communication to the microservice from outside the VLAN comes over HTTPS, but internally everything is HTTP.
* Some load balancers provide useful features. A common one is SSL termination, where inbound HTTPS connections to the load balancer are transformed to HTTP connections once they hit the instance itself.
* One way to scale for resilience is to ensure that you don’t put all your eggs in one basket. A simplistic example of this is making sure that you don’t have multiple services on one host, where an outage would impact multiple services
* having a single microservice per host is certainly preferable to a multiservice-per-host model.
* Getting a bigger box with faster CPU and better I/O can often improve latency and throughput, allowing you to process more work in less time […] this form of scaling, often called vertical scaling
* Some of the HTTP verbs, such as GET and PUT, are defined in the HTTP specification to be idempotent,
* If operations are idempotent, we can repeat the call multiple times without adverse impact.
* In idempotent operations, the outcome doesn’t change after the first application, even if the operation is subsequently applied multiple times.
* The Chaos Monkey is just one part of Netflix’s Simian Army of failure bots. The Chaos Gorilla is used to take out an entire availability center (the AWS equivalent of a data center), whereas the Latency Monkey simulates slow network connectivity between machines.
* With a single, monolithic application, we don’t have many decisions to make. System health is binary. But with a microservice architecture, we need to consider a much more nuanced situation
* When it comes to considering if and how to scale out your system to better handle load or failure, start by trying to understand the following requirements:
	* "Response time/latency: How long should various operations take?"
	* "Availability: Can you expect a service to be down?"
	* "Durability of data: How much data loss is acceptable? How long should data be kept for?"
* This is actually an example of a strangler application, where a new system intercepts calls made to legacy applications and gradually replaces them altogether.
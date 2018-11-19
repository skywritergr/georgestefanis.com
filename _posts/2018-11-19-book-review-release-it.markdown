---
layout: post
title: "Book review: Release it!"
date: 2018-11-19
categories: blog
comments: true
excerpt: "After reading Building Microservices I felt really inspired and then i wanted to learn more about microservices and devops. Specifically about useful patterns that appy in building modern software"
---
After reading [Building Microservices](https://georgestefanis.com/blog/2018/03/21/book-review-building-microservices.html) I felt really inspired and then i wanted to learn more about microservices and devops. Specifically about useful patterns that appy in building modern software

{% include image.html url="https://imagery.pragprog.com/products/93/mnee.jpg" title="Release it! cover" %}

I've learned so many things. Useful patterns like the circuit breaker or the blocked threads antipattern. More than that it helped me build a deeper understanding on troubleshooting errors in production. This is an amazing book that I really recommend as a follow up read after Building Microservices. It keeps on building from where you left of.

Here's some of my notes in no particular order.

## Notes
* Chaos engineering provides that balancing force. It springs from the view that says we need to optimize our systems for availability and tolerance to disruption in a hostile, turbulent world rather than aiming for throughput in an idealized environment.
* Chaos engineering draws from many other fields related to safety, reliability, and control, such as cybernetics, complex adaptive systems, and the study of high-reliability organizations.
* According to the principles of chaos engineering,[93] chaos engineering is “the discipline of experimenting on a distributed system in order to build confidence in the system’s capability to withstand turbulent conditions in production.”
* Release is the beginning of the software’s true life; everything before that release is gestation.
* We can use URL dualism to support many databases by using URLs as both the item identifier and a resolvable resource.
* Versioning can be a real challenge with events, especially once you have years’ worth of them. Stay away from closed formats like serialized objects. Look toward open formats like JSON or self-describing messages. Avoid frameworks that require code generation based on a schema. Likewise avoid anything that requires you to write a class per message type or use annotation-based mapping
* Event notification: A fire-and-forget, one-way announcement. No response is expected or used.
* Event-carried state transfer: An event that replicates entities or parts of entities so other systems can do their work
* Event sourcing: When all changes are recorded as events that describe the change
* Command-query responsibility segregation (CQRS): Reading and writing with different structures. Not the same as events, but events are often found on the “command” side.
* identified three main ways events are used, plus a fourth term that is often conflated with events:
* Relational databases are good at answering, “What is the value of attribute A on entity E right now?” But they’re somewhat less good at keeping track of the history of attribute A on entity E. They’re pretty awkward with graphs or hierarchies, and they’re downright terrible at images, sound, or video.
* Information architecture is how we structure data.
* Inversion works by taking functionality that’s distributed in several modules and raising it up higher in the system. It takes a good solution to a general problem, extracts it, and makes it into a first-class concern.
* Splitting breaks a design into modules, or a module into submodules
* Another subtle issue about microservices that gets lost in the excitement is that they’re great when you are scaling up your organization. But what happens when you need to downsize? Services can get orphaned easily. Even if they get adopted into a good home, it’s easy to get overloaded when you have twice as many services as developers.
* Keep the people busy all the time and your overall pace slows to a crawl
* One important thing for the platform team is to remember they are implementing mechanisms that allow others to do the real provisioning.
* Sometimes when you ask questions but don’t get answers, it means nobody knows the answers. At other times, though, it means nobody wants to be seen answering the questions.
* The following changes are always safe:
	* Require a subset of the previously required parameters
	* Accept a superset of the previously accepted parameters
	* Return a superset of the previously returned values
	* Enforce a subset of the previously required constraints on the parameters
* changes that don’t do those things must be safe.
* We can always accept more than we accepted before, but we cannot accept less or require more. We can always return more than we returned before, but we cannot return less.
* Postel’s robustness principle says, “Be conservative in what you do, be liberal in what you accept from others.”
* If you want others to respect your autonomy, then you must respect theirs.
* To be successful, your software will be deployed early and often. That means the act of deployment is an essential part of the system’s life. Therefore, it’s worth designing the software to be deployed easily. Zero downtime is the objective
* Once the batch migration is done, you can even push a new deployment that removes the conditional check for the old version.
* What about the documents that don’t get touched for a long time? That’s where the batch part comes in. After this has run in production for a while, you’ll find that the most active documents are updated. Now you can run a batch migration on the remainder.
* The third major approach is the one I like best. I call it “trickle, then batch.” In this strategy, we don’t apply one massive migration to all documents. Rather, we add some conditional code in the new version that migrates documents as they are touched
* A few pointers about configuration services:
* Make sure your instances can start without the configuration service.
* Make sure your instances don’t stop working when configuration is unreachable.
* Make sure that a partitioned configuration node doesn’t have the ability to shut down the world.
* Replicate across geographic regions.
* These services are scalable but not elastic. That means you can add and remove nodes, but response time will degrade as the nodes rebalance their data.
* Configuration services like ZooKeeper and etcd are distributed databases that applications can use to coordinate their configuration
* Here are some categories of things I’ve consistently found useful.
* Splunk dominates the log indexing space today.[41] The troika of Elasticsearch, Logstash, and Kibana is another popular implementation.
* With a pull-mode tool, the collector runs on a central machine and reaches out to all known hosts to remote-copy the logs
* Push mode is quite helpful with containers, since they don’t have any long-lived identity and often have no local storage.
* log collectors can either work in push or pull mode
* the best way to tell if users are receiving a good experience is to measure it directly. This is known as real-user monitoring (or RUM, if you like).
* At scale, “partially broken” is the normal state of operation.
* If you want to apply a heuristic, take your maximum wait time divided by mean processing time and add one. Multiply that by the number of request handling threads you have and bump it up by 50 percent. That’s a reasonable starting point for your listen queue length.
* Once you start contemplating a layer of load balancing in front of your reverse proxy servers, it’s time to look at other options.
* Well-behaved proxies will add the “X-Forwarded-For” header to incoming HTTP requests, so services can use a custom log format to record that.
* A normal proxy multiplexes many outgoing calls into a single source IP address. A reverse proxy server does the opposite: it demultiplexes calls coming into a single IP address and fans them out to multiple addresses.
* Software load balancing is the low-cost approach. It uses an application to listen for requests and dole them out across the pool of instances. This application is basically a reverse proxy server,
* To a calling application, the load balancer should be transparent.
* When using DNS, it’s important to have a logical service name to call, rather than a physical hostname. Even if that logical name is just an alias to the underlying host, it’s still preferable.
* On the other hand, a small business with just a few developers should probably stick with direct DNS entries. Changes aren’t going to be as rapid and the developers can keep services up-to-date.
* A large team or department with hundreds of small services would do well to use Consul or another dynamic discovery service. The cost of running and operating Consul is easily amortized over the number of teams that benefit.
* A health check is just a page or API call that reveals the application’s internal view of its own health
* The instance itself won’t be able to tell much about overall system health, but it should emit metrics that can be collected, analyzed, and visualized centrally. This may be as simple as periodically spitting a line of stats into a log file.
* the record of state transitions will be important during postmortem investigations.
* Interesting state transitions should be logged,
* Messages should include an identifier that can be used to trace the steps of a transaction. This might be a user’s ID, a session ID, a transaction ID, or even an arbitrary number assigned when the request comes in
* Above all else, log files are human-readable. That means they constitute a human-computer interface and should be examined in terms of human factors.
* I recommend adding a step to your build process that automatically removes any configs that enable debug or trace log levels.
* Log errors in business logic or user input as warnings (if at all).
* Just because a user entered a bad credit card number and the validation component threw an exception doesn’t mean anything has to be done about it.
* Logging should be aimed at production operations rather than development or testing. One consequence is that anything logged at level “ERROR” or “SEVERE” should be something that requires action on the part of operations.
* a logs directory under the application’s install directory is the wrong way to go
* If you want to avoid tight coupling to a particular monitoring tool or framework, then log files are the way to go.
* Logging is certainly a white-box technology
* By contrast, white-box technology runs inside the process.
* A black-box technology sits outside the process, examining it through externally observable things.
* In designing for transparency, keep a close eye on coupling. It’s relatively easy for the monitoring framework to intrude on the internals of the system. The monitoring and reporting systems should be like an exoskeleton built around your system, not woven into it.
* Transparency refers to the qualities that allow operators, developers, and business sponsors to gain understanding of the system’s historical trends, present conditions, instantaneous state, and future projections.
* Most small teams are better off using injected config.
* these services require a high degree of operational maturity and carry some noticeable overhead.
* ZooKeeper is scalable but not elastic, and adding and removing nodes is disruptive
* Because this builds a hard dependency on the config service, any downtime is immediately a “Severity 1” problem.
* ZooKeeper and etcd are both popular choices for a configuration service.
* We don’t want our instance binaries to change per environment, but we do want their properties to change. That means the code should look outside the deployment directory to find per-environment configurations.
* This is often described as “immutable infrastructure.”
* Instead, when a change is needed, create a new image starting from the base again,
* The DevOps and cloud community say that it’s more reliable to always start from a known base image, apply a fixed set of changes, and then never attempt to patch or update that machine.
* Only make production builds on a CI server, and have it put the binary into a safe repository that nobody else can write into.
* Developers should not do production builds from their own machines.
* you should plan on moving to a private repository as soon as possible.
* Downloading dependencies from the Internet is convenient but not safe. It’s far too easy for one of those dependencies to silently be replaced, either though a man-in-the-middle attack or by compromising the upstream repository.
* Developers must be able to build the system, run tests, and run at least a portion of the system locally
* Developers should work on code within a version control system. There’s simply no excuse not to use version control today
* The general rule is that VMs have to “volunteer” to do work, rather than having a controller dole the work out. That means a new VM should be able to start up and join whatever pool of workers handles load
* Containerized applications, even more than ordinary ones, need to send their telemetry out to a data collector.
* Finally, it’s notoriously hard to debug an application running inside a container.
* Aim for a total startup time of one second.
* Containers are meant to start and stop rapidly. Avoid long startup or initialization sequences.
* The second thing to externalize is networking. Container images should not contain hostnames or port numbers.
* In either case, look into password vaulting.
* A 12-factor app handles this naturally.
* First, the whole container image moves from environment to environment, so the image can’t hold things like production database credentials.
* When you design an application for containers, keep a few things in mind.
* A close second for “hardest problem in container-world” is making sure enough container instances of the right types are on the right machines.
* The most challenging part of running containers in the data center is definitely the network.
* The bottom line is: don’t trust the OS clock. If external, human time is important, use an external source like a local NTP server.
* A clock on a virtual machine is not necessarily monotonic or sequential
* Design for production hardware for most applications just means building to scale horizontally.
* Many utilities and programs assume that the machine’s self-assigned FQDN is a legitimate DNS name that resolves back to itself. This is largely true for development machines and largely untrue for production services.
* a machine uses its hostname to identify the whole machine, while a DNS name identifies an IP address.
* a machine may have its FQDN set to “spock.example.com” but have a DNS mapping as “mail.example.com” and “www.example.com.”
* Together, the concatenation of the hostname and search domain is called the fully qualified domain name (FQDN.)
* Consider a response curve.
* Actions may be safe within a defined range. Outside that range they should encounter increasing “resistance” by slowing down the rate by which they can occur.
* The whole point of a governor is to slow things down enough for humans to get involved. Naturally that means connecting to monitoring both to alert humans that there’s a situation and to give them enough visibility to understand what’s happening.
* A governor is stateful and time-aware. It knows what actions have been taken over a period of time. It should also be asymmetric.
* We can create governors to slow the rate of actions.
* A governor limits the speed of an engine. Even if the source of power could drive it faster, the governor prevents it from running at unsafe RPMs.
* We should use humans for what automation is bad at: perceiving the whole situation at a higher level.
* Automation has no judgment. When it goes wrong, it tends to go wrong really quickly. By the time a human perceives the problem, it’s a question of recovery rather than intervention.
* You only have a few options when a queue is full. All of them are unpleasant: drop data, refuse work, or block. Consumers must be careful not to block forever.
* as a queue’s length reaches toward infinity, response time also heads toward infinity
* The test harness can produce slow responses, no responses, or garbage responses. Then you can see how your application reacts.
* The test harness can be designed like an application server; it can have pluggable behavior for the tests that are related to the real application. A single framework for the test harness can be subclassed to implement any application-level protocol, or any perversion of the application-level protocol, necessary.
* A test harness that injects faults will unearth many hidden dependencies. Injecting latency in requests will uncover many more.
* Actor systems use a hierarchical tree of supervisors to manage the restarts. Whenever an actor terminates, the runtime notifies the supervisor. The supervisor can then decide to restart the child actor, restart all of its children, or crash itself
* When we crash an actor or a process, how does a new one get started?
* If the system can determine in advance that it will fail at an operation, it’s always better to fail fast.
* If slow responses are worse than no response, the worst must surely be a slow failure response.
* Ship the log files to a centralized logging server, such as Logstash, where they can be indexed, searched, and monitored.
* Make sure that all log files will get rotated out and eventually purged, though, or you’ll eventually spend time fixing the tool that’s supposed to help you fix the system.
* one of the excellent logging frameworks available, the logrotate utility is ubiquitous on UNIX.
* The logical extreme on the “no fiddling” scale is immutable infrastructure—it can’t be fiddled with!
* At smaller scales, process binding is an example of partitioning via bulkheads. Binding a process to a core or group of cores ensures that the operating system schedules that process’s threads only on the designated core or cores. Because it reduces the cache bashing that happens when processes migrate from one core to another,
* Open source circuit breaker libraries are available for every language and framework, so it’s probably better to start with one of those.
* It’s a simple counter that you can increment every time you observe a fault. In the background, a thread or timer decrements the counter periodically (down to zero, of course.) If the count exceeds a threshold, then you know that faults are arriving quickly.
* I like the Leaky Bucket pattern
* The Timeouts pattern is useful when you need to protect your system from someone else’s failure.
* My experience has been that problems on the network, or with other servers, tend to last for a while. Thus, fast retries are very likely to fail again.
* Language runtimes that use callbacks or reactive programming styles also let you specify timeouts more easily.
* An approach to dealing with pervasive timeouts is to organize long-running operations into a set of primitives that you can reuse in many places.
* Well-placed timeouts provide fault isolation—a problem in some other service or device does not have to become your problem.
* In any API or protocol, the caller should always indicate how much of a response it’s prepared to accept.
* If your system tracks its own responsiveness, then it can tell when it’s getting slow. Consider sending an immediate error response when the average response time exceeds the system’s allowed time
* Memory leaks often manifest via Slow Responses as the virtual machine works harder and harder to reclaim enough space to process a transaction. This will appear as a high CPU utilization, but it is all due to garbage collection, not work on the transactions themselves
* Infrastructure management tools can make very large impacts very quickly. Build limiters and safeguards into them so they won’t destroy your whole system at once.
* Systems that consume resources should be stateful enough to detect if they’re trying to spin up infinity instances.
* When the gap between expected state and observed state is large, signal for confirmation.
* Apply hysteresis. (See ​Governor​.) Start machines quickly, but shut them down slowly.
* If observations report that more than 80 percent of the system is unavailable, it’s more likely to be a problem with the observer than the system.
* We can implement similar safeguards in our control plane software:
* Use random clock slew to diffuse the demand.
* A pulse can develop during load tests, if the virtual user scripts have fixed-time waits in them. Instead, every pause in a script should have a small random delta applied.
* A dogpile can occur in several different situations:
	* When booting up several servers, such as after a code upgrade and restart
	* When a cron job triggers at midnight (or on the hour for any hour, really)
	* When the configuration management system pushes out a change
* When a bunch of servers impose this transient load all at once, it’s called a dogpile.
* It might be impractical to evenly match capacity in each system for a lot of reasons. 
* Point-to-point communication scales badly, since the number of connections increases as the square of the number of participants. 
* shares its sessions with another designated application server. There are numerous strategies for session failover, but they all involve getting the user’s session off the original server. Most of the time, that implies some level of shared resources.
* As for the human-facilitated attacks, the keys are training, education, and communication.
* You can avoid machine-induced self-denial by building a “shared-nothing” architecture. (“Shared-nothing” is what you have when each server can run without knowing anything about any other server.
* A self-denial attack describes any situation in which the system—or the extended system that includes humans—conspires against itself.
* Avoid infinite waits in function calls; use a version that takes a timeout parameter. Always use timeouts, even though it means you need more error-handling code.
* Learn and apply safe primitives. It might seem easy to roll your own producer/consumer queue: it isn’t.
* Recall that the Blocked Threads antipattern is the proximate cause of most failures.
* In object theory, the Liskov substitution principle (see Family Values: A Behavioral Notion of Subtyping [LW93]) states that any property that is true about objects of a type T should also be true for objects of any subtype of T
* When the time comes to alter their state, do it by constructing and issuing a “command object.” This style is called “Command Query Responsibility Separation,”
* One elegant way to avoid synchronization on domain objects is to make your domain objects immutable.
* Managed runtime languages such as C#, Java, and Ruby almost never really crash.
* The most common failure mode for applications built in these languages is navel-gazing—a happily running interpreter with every single thread sitting around waiting for Godot.
* Use a session only for caching so you can purge the session’s contents if memory gets tight. 
* The second approach is legal. Write some terms of use for your site that say users can view content only for personal or noncommercial purposes. Then, when the screen scrapers start hitting your site, sic the lawyers on them.
* When a single IP address claims to be running Internet Explorer on Windows, Opera on Mac, and Firefox on Linux in the same five-minute window, something is up
* The first is technical. Once you identify a screen scraper, block it from your network. If you’re using a content distribution network such as Akamai, it can provide this service for you. 
* I’ve seen only two approaches work. 
* Some sites also choose to redirect robots and spiders, based on the user-agent header
* Keeping out legitimate robots is fairly easy through the use of the robots.txt file.[8] The robot has to ask for the file and choose to respect your wishe
* so if you are not using URL rewriting to track sessions, each new page request will create a new session.
* Want to bring down nearly any dynamic web application? Pick a deep link from the site and start requesting it without sending cookies
* It’s there as part of TCP’s defense against bogons.
* After your application code closes a socket, the TCP stack moves it through a couple of terminal states. One of them is the TIME_WAIT state.
* You can turn the TIME_WAIT interval down to get those ports back into use ASAP.
* A bogon is a wandering packet that got routed inefficiently and arrives late, possibly out of sequence, and after the connection is closed.
* You may not spend much time thinking about the number of sockets on your server, but that’s another limit you can run into when traffic gets heavy.
* “Capacity” is the maximum throughput your system can sustain under a given workload while maintaining acceptable performance.
* The most effective patterns to combat cascading failures are Circuit Breaker and Timeouts.
* Most of the time, a chain reaction happens when your application has a memory leak.
* Recognize that one server down jeopardizes the rest.
* A chain reaction happens because the death of one server makes the others pick up the slack. The increased load makes them more likely to fail
* Chain reactions are sometimes caused by blocked threads. This happens when all the request-handling threads in an application get blocked and that application stops responding.
* The alternative, vertical scaling, means building bigger and bigger servers—adding core, memory, and storage to hosts.
* The dominant architectural style today is the horizontally scaled farm of commodity hardware. Horizontal scaling means we add capacity by adding more servers.
* Every integration point will eventually fail in some way, and you need to be prepared for that failure.
* The most effective stability patterns to combat integration point failures are Circuit Breaker and Decoupling Middleware.
* Network failures can hit you in two ways: fast or slow
* The read call will just block until the server gets around to responding. Often, the default is to block forever. 
* The listen queue is the worst place to be. While the socket is in that partially formed state, whichever thread called open is blocked inside the OS kernel until the remote application finally gets around to accepting the connection or until the connection attempt times out. 
* One wrinkle to watch out for, though, is that it can take a long time to discover that you can’t connect.
* The simplest failure mode occurs when the remote system refuses connections. The calling system must deal with connection failures
* Faults will happen; they can never be completely prevented. And we must keep faults from becoming errors.
* One way to prepare for every possible failure is to look at every external call, every I/O, every use of resources, and every expected outcome and ask, “What are all the ways this can go wrong?”
* Tight coupling accelerates cracks. 
* Triggering a fault opens the crack. Faults become errors, and errors provoke failures.
* Failure: An unresponsive system.
* Error: Visibly incorrect behavior.
* Fault: A condition that creates an incorrect internal state in your software.
* No matter what, your system will have a variety of failure modes. Denying the inevitability of failures robs you of your power to control and contain them
* The major dangers to your system’s longevity are memory leaks and data growth.
* In a mechanical system, a material changes shape when stress is applied. This change in shape is called the strain. Stress produces strain. The same thing happens with computer systems.
* The terms impulse and stress come from mechanical engineering. An impulse is a rapid shock to the system. An impulse to the system is when something whacks it with a hammer. In contrast, stress to the system is a force applied to the system over an extended period.
* Enterprise software must be cynical. Cynical software expects bad things to happen and is never surprised when they do.
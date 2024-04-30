End to End Service Mesh: Secure Boot (Need Cool Name)

A fully mathematically verifiable secure boot kernel that can't be corrupted during run time.

This means that we can statically determine if the kernel is ready to be able to bootstrap the inital loaders.

We can create a cache of correct function traces that is allowed by the kernel. 

And then a microkernel watches every singular call made by the main kernel that is supposed to spawn importan services.

If a function traceback is not in this allowed set, the main kernel is deemed untrustworthy and thus replaced.

And to ensure security of the microkernel demon, we can simply extend it to at least 2 or more replicas. 

The loaders in the main kernel are for important things we need before a "service" runs. 

These initial loaders shouldn't be assumed to be trusted by default (default ring security structure).

Instead, we should employ Linux daemon like "services" that are very lightweight microkernels to check the security of these loaders.

These microkernels are able to directly interact with the main kernel containing the loaders and check memory.

These microkernels can use cryptographic methods to verify memory correctness and use ECC techniques such as parity bit checks to ensure that every singular bit in both the stack and heap is correct. 

The cryptographic methods can also use other techniques to obfcuscate virtual memory mapping for further security.

All of this results in us employing zero trust/ no trust at the root level from which every process spawns while also ensuring that memory is fully clean/correct. I believe this is one method of achieving perfect kernel startup security guarantee when employing zero trust / no trust default rule. 

Something similar to this: https://www.usenix.org/legacy/publications/library/proceedings/sec03/tech/full_papers/home/staff/alex/export/twycross/bhatkar/bhatkar_html/dao002.html

Finally, we can scale these daemon like microkernels depending on quorom vs majority rules. It would be interesting to bench mark this collection of kernels and microkernels and to see if 2, 3 or 5 microkernels are needed.

Why? We are trying to create a complete end to end service mesh archiecture from the ground up.

We knew that gRPC and monitoring were vital pieces required in each "node".

So we could have a secure gRPC channel as a loader, a secure Open Telemetry (OTel) exporter loader and a third optional secure service args loaders.

None of these should be trusted by default including the provided bare gRPC channel, so we decided to try this experiment.

We were planning on forking this: https://sel4.systems and benchmarking. We are striving to make the fastest and most lighweight bootloader.

We were planning on writing this in Rust and even considered going down to the assembly code and reorganizing instructions for performance.

Another idea was to have a very lightweight GDB type program that could inspect every single trace in a binary. 

I think this is doable and would barely impact performance. 


Credits: Simhon Chourasia (s2choura). We were the only ones that discussed this. I brought the idea of a demon L4 microkernel to him.

I'm currently trying to create a very fast and secure Layer 0 and Layer 1 for an end to end service mesh. 

The Layer 1 is simply a stub service that is ready to execute a main function and has a gRPC channel ready for transport.

It also has a built in Open Telemetry (OTel) periodic exporter ready to publish metrics to an exposed gRPC endpoint.

I wanted to build this because I had built an intercepter for gRPC in one of my coops for distributed tracing.

I also recently did an internship at Apple where I instrumented and brought up an entire end to end observation platform.

This platform was simply OTel at the service level to instrument metrics and then an exporter that published securely using mTLS to an endpoint.

These metrics were sent fast, highly efficient, took very little storage due to the nature of protocol buffers.

The average delay time I noticed when I implemented this was 2-5 seconds (more data needed) from when my service was hit over mTLS to when data was ingested to a timeseries database, queried and then visualized. The latter part of this is Apple's own IP.

I wanted to complete this path and make the entire thing end to end and open source, and started recruiting my friends to do it over the summer. 

Thank you,

Umar Yousafzai (uyousafz@uwaterloo.ca, umar.yousafzai@uwaterloo.ca, uyousafz@icloud.com)





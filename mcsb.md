---
layout: page
---

I am the archtect and primary author of [MCSB, the Multi-Client Shared Buffer](https://github.com/GregoryEAllen/mcsb), a high-throughput shared-memory publish-subscribe middleware suitable for implementing soft real-time systems on POSIX.
MCSB grew out of our organization's need to efficiently handle high-throughput sensor data:
- Upwards of gigabytes per second, and no way to throttle
- Moving or copying the data in memory is very expensive
- Memory bandwidth is a limited resource
- Preserve memory alignment for high-performance SIMD DSP kernels
- Use zero-copy interfaces where possible
- Adhere to soft real-time system requirements
- Misbehaving clients should not back up the whole system

Thread programming is a common approach for concurrent execution. Programs using threads can be notoriously difficult to write and debug, because the thread model is [wildly nondeterministic](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2006/EECS-2006-1.pdf) and can be burdensome to the programmer.
Many models and languages have been proposed to address this, but they generally remain esoteric.

My dissertation topic, [Computational Process Networks (CPN)](https://users.ece.utexas.edu/~bevans/students/phd/greg_allen/) (and [CPN software](https://github.com/GregoryEAllen/cpn)), provides a scalable model for determinate execution of concurrent systems and high-throughput, zero-copy interfaces for implementing signal processing systems. However its restrictive dataflow model can be a poor fit for some other types of interaction patterns, e.g. RPC.

We already had decades of experience with the publish/subscribe middleware model. We like the convenience, modularity, and protection that such a middleware provides, but existing middleware solutions at the time couldn't come close to meeting the required data rates.

MCSB is a pub/sub middleware designed with lessons learned from CPN. It is less academic and more practical than CPN, with a less restrictive and more flexible model. It is less formal than CPN, but still focused on some formal guarantees such as liveness and memory boundedness. MCSB allows the convenience of using a middleware while allowing the high performance of a shared memory multi-threaded design. It allows the building of determinate systems from composeable components.

A *manager* process allocates and manages a series of large shared memory buffers, as well as a local (Unix) socket for control. Client processes connect to the manager and map the shared memory buffers. Producer clients are told where in the buffers to put messages for sending, and consumer clients are told where in the buffer to read messages they've received. The manager coordinates these transactions by reference, and recycles buffer memory when it becomes available.

Because all message traffic occurs through shared memory, no copying is needed and throughput is typically limited only by the memory bandwidth. MCSB allows the convenience and protection of a middleware design but with the performance only afforded by a shared-memory design.

MCSB is written in C++ and has first-class Python bindings. Implementation of MCSB began in 2009 and was first delivered with a project in 2010. I defended in 2011. By 2013 it was in heavy internal use, and v2.0.0 was publicly released in 2014. As of September 2025, the current internal version is v2.7.1. (See [here](sw/) about our release process.)

MCSB is a foundational software infrastructure in many of the systems that we develop and deliver, and an ecosystem of software tools has grown around it.
This includes an MCSB-bridge program that transparently connects the pub/sub middleware across a network of computers, with the obvious throughput penalty of copying the messages across a TCP network. This would be a good candidate for RDMA, but that has never been deeply explored.

This also includes a recorder that streams high-throughput data to disk in a log structure, often as fast as the disk will allow. The recorder additionally saves a streaming index file that can used to quickly create a database of all recorded messages. This allows fast search and random access for analysis and playback. We have recorded petabytes of data in these formats, and increasing over time.

These recordings feed a sizeable portion of our activity, such as system perfomance analysis, design verification, algorithm development, research, and post-mission analysis and decision making. They also feed our AI/ML training pipeline.

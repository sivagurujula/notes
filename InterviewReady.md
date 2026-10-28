This is actually the highest ROI thing you can do.

Don't ask AI:

Explain ConcurrentHashMap


Ask AI:

Train me to answer interview questions on ConcurrentHashMap from Junior to Staff level.


The difference is massive.

MASTER PROMPT TEMPLATE

Use this for every topic:

Act as a Staff Engineer interviewer from Amazon, Microsoft, Uber, Netflix and Goldman Sachs.

Topic: <TOPIC>

Teach me this topic in the following order:

1. First principles explanation.
2. Real-world analogy.
3. Internal implementation.
4. JVM/OS level behavior.
5. Common interview questions.
6. Senior-level questions.
7. Staff-level questions.
8. Follow-up questions interviewers usually ask.
9. Common mistakes candidates make.
10. Production use cases.
11. Open source examples (Spring/Kafka/Netty/Tomcat).
12. Debugging scenarios.
13. Performance considerations.
14. Design trade-offs.
15. 2-minute interview answer.
16. Visual mental model.
17. Create 20 interview questions with model answers.

Challenge me until I can answer confidently.

1. HashMap Mastery Prompt
Act as a Java Staff Engineer interviewer.

Teach me HashMap from first principles.

Cover:

- hash()
- bucket calculation
- collisions
- linked list
- treeification
- resize
- load factor
- why powers of 2 are used
- hashCode vs equals
- memory overhead

Show OpenJDK source flow for:

put()
get()
resize()

Then perform a mock interview with increasing difficulty.

Keep asking follow-up questions until I can answer like a Staff Engineer.

2. ConcurrentHashMap Mastery Prompt
Teach me ConcurrentHashMap from interview perspective.

Cover:

- Why HashMap fails
- Hashtable problems
- Segment locking (JDK7)
- Bucket locking (JDK8)
- CAS
- synchronized bins
- weakly consistent iterators
- computeIfAbsent
- LongAdder
- memory visibility

Show actual examples from:

- Tomcat
- Kafka
- Spring
- Caffeine

Then generate:

20 Senior-level questions
20 Staff-level questions

Challenge every answer with follow-up questions.

3. Java Memory Model Prompt
Teach me Java Memory Model from first principles.

Explain:

- CPU Cache
- Main Memory
- Register
- Cache line
- Store buffer

Then explain:

- visibility
- atomicity
- ordering
- happens-before
- memory barriers

Show how volatile works internally.

Show assembly-level intuition.

Generate 30 interview questions and challenge my understanding.

4. Concurrency Prompt

You already spend a lot of time here.

Teach me Java concurrency from Staff Engineer perspective.

Cover:

- Thread lifecycle
- synchronized
- Lock
- ReadWriteLock
- StampedLock
- CAS
- AtomicInteger
- AtomicReference
- ABA problem
- AQS
- Semaphore
- CountDownLatch
- CyclicBarrier
- Phaser

Show implementation internals and production use cases.

Create a mind map and cheat sheet.

Conduct a mock interview.

5. ThreadPoolExecutor Prompt
Teach me ThreadPoolExecutor deeply.

Explain:

- corePoolSize
- maxPoolSize
- queue
- rejection policy

Walk through execute() source code.

Show request lifecycle.

Show thread creation decisions.

Create production tuning examples.

Challenge me with Staff-level scenarios.

6. CompletableFuture Prompt
Teach me CompletableFuture from beginner to Staff level.

Cover:

- Future
- CompletableFuture
- ForkJoinPool

Explain:

- thenApply
- thenCompose
- thenCombine
- allOf
- anyOf

Show production examples:

- API aggregation
- parallel DB calls
- timeout handling
- retries

Create interview drills.

7. JVM Prompt
Teach me JVM internals.

Cover:

- Heap
- Stack
- Metaspace
- ClassLoader
- JIT
- Interpreter

Trace:

new Employee()

from source code to memory allocation.

Show JVM diagrams.

Create Staff-level interview questions.

8. Garbage Collection Prompt
Teach me Garbage Collection.

Cover:

- Heap layout
- Eden
- Survivor
- Old Gen

Explain:

- Minor GC
- Major GC
- Full GC

Then:

- CMS
- G1
- ZGC
- Shenandoah

Create production troubleshooting scenarios.

9. SQL & Indexing Prompt
Act as a Staff Database Engineer.

Teach me SQL interview topics.

Cover:

- B+ Trees
- Clustered Index
- Secondary Index
- Composite Index

Explain:

SELECT
JOIN
ORDER BY
GROUP BY

using indexes.

Generate performance troubleshooting questions.

Show query optimization techniques.

10. Transactions Prompt
Teach me database transactions deeply.

Cover:

- ACID
- Locks
- MVCC

Explain:

- Read Uncommitted
- Read Committed
- Repeatable Read
- Serializable

Show real banking examples.

Generate interview questions.

11. Spring Core Prompt
Teach me Spring Core internals.

Cover:

- BeanFactory
- ApplicationContext
- BeanDefinition
- Bean Lifecycle
- Dependency Injection

Trace application startup.

Explain:

@Autowired

from source code perspective.

Generate Senior and Staff interview questions.

12. Spring AOP Prompt
Teach me Spring AOP internally.

Cover:

- Dynamic Proxy
- CGLIB
- Interceptor
- Advice

Trace:

@Transactional

execution flow from REST call to DB commit.

Generate mock interview questions.

13. Kafka Prompt
Teach me Kafka from first principles.

Cover:

- Broker
- Topic
- Partition
- Offset
- Consumer Group

Explain:

ordering
replication
leader election

Show production architecture.

Challenge me with Staff-level design questions.

14. Logging & Tracing Prompt

Use this after today's discussion.

Teach me logging internals.

Explain:

Logger
Appender
Layout
Async Logging
MDC
ThreadLocal

Show:

log.info("Hello")

to disk write path.

Then explain:

TraceId
SpanId
OpenTelemetry
Zipkin
Jaeger

Create production troubleshooting scenarios.

15. System Design Prompt
Act as a Staff Engineer interviewer.

Teach me System Design from first principles.

Cover:

- Scalability
- Availability
- Reliability
- Performance

Explain:

CAP
Replication
Sharding
Caching
Load Balancing

Generate:

URL Shortener
Payment System
Chat System
Notification System

interview questions.

Challenge every design decision.

THE ULTIMATE INTERVIEW DRILL PROMPT

This is the one prompt I would use every day.

Act as a Staff Engineer interviewer.

Choose one topic at random from:

- HashMap
- ConcurrentHashMap
- JMM
- Concurrency
- CompletableFuture
- JVM
- GC
- SQL
- Transactions
- Spring
- Kafka
- Logging
- System Design

Conduct a real interview.

Rules:

1. Ask one question at a time.
2. Wait for my answer.
3. Score my answer out of 10.
4. Point out missing concepts.
5. Ask deeper follow-up questions.
6. Keep drilling until Staff-level depth is reached.
7. At the end provide:
   - strengths
   - weaknesses
   - revision topics
   - ideal interview answer

My recommendation for your 7-day sprint

Spend daily:

30%
Concurrency + JMM

20%
JVM + GC

20%
Spring Core + AOP

15%
SQL + Transactions

10%
Kafka

5%
Logging + Tracing


And for every topic, use this cycle:

Learn
  ↓
Explain aloud
  ↓
Mock Interview
  ↓
Gap Analysis
  ↓
Cheat Sheet
  ↓
Repeat


That's exactly how I'd prepare a Senior Java developer for a Staff-level interview in one focused week.

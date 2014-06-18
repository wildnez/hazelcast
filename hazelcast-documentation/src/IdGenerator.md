

## IdGenerator

Hazelcast IdGenerator is used to generate cluster-wide unique identifiers. Generated identifiers are long type primitive values between 0 and `Long.MAX_VALUE`. 

ID generation occurs almost at the speed of `AtomicLong.incrementAndGet()`. A group of 1 million identifiers is allocated for each cluster member. In the background, this allocation takes place with an IAtomicLong incremented by 1 million. Once cluster member claims to generate IDs (allocation is done), IdGenerator is able to increment a local counter. If a cluster member uses all IDs in the group, it will have another 1 million IDs. By this way, only one time of network traffic is needed, meaning 999.999 identifiers are generated in memory. And this is fast.

Let's write a sample identifier generator.

```java
public class IdGeneratorExample {
     }
```

And let's run the above code two times. Output will be similar to the below.
```

```

You can see that the generated IDs are unique and counting upwards. If you see duplicated identifiers, it means your instances could not form a cluster. 


<font color='red'>***Note:***</font> *Generated IDs are unique during the life cycle of the cluster. If the entire cluster is restarted, IDs start from 0 again or you can initialize to a value using the `init()` method of IdGenerator.*

<font color="red">***Note:***</font> *IdGenerator has 1 synchronous backup and no asynchronous backups. Its backup count is not configurable.*

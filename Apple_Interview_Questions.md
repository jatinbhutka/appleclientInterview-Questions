# Apple Client Interview Questions:

## Scala Questions:

#### 1. Difference between var, val, lazy val and def?

Both Var and Val keyword are used to declare variables in Scala. 

There is a subtle difference between them. Var is variable use to declare variable. Its mutable reference to a value. Since its mutable Variable, its value may change through the program lifetime. 

On the other hand, Val is used to declare values. Val keyword represent a value. Its an immutable reference, meaning that its value never changes. Once assigned it will always keep the same value.

Variable types in Scala cannot change.

The def is a function declaration. It gets executed on function call. It’s exactly similar to the def in python.



			
			
#### 2) Write a small scala function to retrieve value of a token: 

       def getValue(tokenString:String, valueString:String, key:String):String
       Input is 2 strings token : 
       tokenString : "key1, key2, key3, key4"
       valueString : "val1, val2, val3, val4”
       key : “key2"
   
```scala
object retriveValOfToken 
{ 
	def main(args: Array[String]) 
	{ 
		 var tokenString: String = "key1, key2, key3, key4"
		 var valueString: String = "val1, val2, val3, val4"
		 var key: String = "key2"
		 println("Value of a given token: " + getValue(tokenString,valueString, key)); 
	} 

	// declaration and definition of function 
	def getValue(tokenString:String, valueString:String, key:String):String =
	{ 
	   var n:Int = 0  
	   var tokenString1: Array[String] = tokenString.split(", ")
	   var valueString1: Array[String] = valueString.split(", ")
	   //println(tokenString)
	   //println(valueString)

	   var zippedTokenValue: Seq[(String, String)] = tokenString1 zip valueString1
	   for ((token, value)<- zippedTokenValue )
		{
		  if (token == key)
		  {	  
		  return value
		  }
		}
	   // returning the value of sum 
	   return key
	} 
} 

```


#### 3) What is the difference between persist() and cache()?

Spark RDD persistence is an optimization technique in which saves the result of RDD evaluation. Using this we save the intermediate result so that we can use it further if required. It reduces the computation overhead.
		
We can make persisted RDD through cache() and persist() methods. 
		
When we use the cache() method we can store all the RDD in-memory. We can persist the RDD in memory and use it efficiently across parallel operations.
		
The difference between cache() and persist() is that using cache() the default storage level is MEMORY_ONLY while using persist() we can use various storage levels 
		
Using persist() we can use various storage levels to Store Persisted RDDs in Apache Spark. Let’s discuss each RDD storage level one by one-

a. MEMORY_ONLY
		In this storage level, RDD is stored as deserialized Java object in the JVM. If the size of RDD is greater than memory, It will not cache some partition and recompute them next time whenever needed. In this level the space used for storage is very high, the CPU computation time is low, the data is stored in-memory. It does not make use of the disk.

b. MEMORY_AND_DISK
		In this level, RDD is stored as deserialized Java object in the JVM. When the size of RDD is greater than the size of memory, it stores the excess partition on the disk, and retrieve from disk whenever required. In this level the space used for storage is high, the CPU computation time is medium, it makes use of both in-memory and on disk storage.

c. MEMORY_ONLY_SER
		This level of Spark store the RDD as serialized Java object (one-byte array per partition). It is more space efficient as compared to deserialized objects, especially when it uses fast serializer. But it increases the overhead on CPU. In this level the storage space is low, the CPU computation time is high and the data is stored in-memory. It does not make use of the disk.

d. MEMORY_AND_DISK_SER
		It is similar to MEMORY_ONLY_SER, but it drops the partition that does not fits into memory to disk, rather than recomputing each time it is needed. In this storage level, The space used for storage is low, the CPU computation time is high, it makes use of both in-memory and on disk storage.

e. DISK_ONLY
		In this storage level, RDD is stored only on disk. The space used for storage is low, the CPU computation time is high and it makes use of on disk storage.
			
Hence, Caching or persistence are the optimization techniques for interactive and iterative Spark computations. It helps to save intermediate results so we can reuse them in subsequent stages. These intermediate results as RDDs are thus kept in memory (default) or more solid storages like disk and/or replicated.


#### 4) Explain the difference between Spark SQL and Hive

#### 5) Explain Partitions and SparkContext?

#### 6) Write a Scala function which takes a list and a target number and returns combination of numbers whose sum to the target number

#### 7) There are 2 lists; one with birth year, other one with death year. Write Scala program to find out which year people lived the max.

#### 8) How do you remove elements with a key present in the other RDD?


## General/Java Questions

#### 1) Difference between List and Set data structures?

#### 2) Why is String immutable (or final) in Java?

#### 3) What does “final” keyword achieve for a class, method or variable?

#### 4) When would you have a private constructor in a class?

#### 5) What does a “synchronized” method or code block achieve?

#### 6) Why does a “wait()” and “notify()” need to be within a “synchronized” block? How does these calls help in inter thread communication?

#### 7) Write a function to remove duplicates from an unsorted linked list?


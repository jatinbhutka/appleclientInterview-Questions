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

a. MEMORY_ONLY:
In this storage level, RDD is stored as deserialized Java object in the JVM. If the size of RDD is greater than memory, It will not cache some partition and recompute them next time whenever needed. In this level the space used for storage is very high, the CPU computation time is low, the data is stored in-memory. It does not make use of the disk.

b. MEMORY_AND_DISK:
In this level, RDD is stored as deserialized Java object in the JVM. When the size of RDD is greater than the size of memory, it stores the excess partition on the disk, and retrieve from disk whenever required. In this level the space used for storage is high, the CPU computation time is medium, it makes use of both in-memory and on disk storage.

c. MEMORY_ONLY_SER:
This level of Spark store the RDD as serialized Java object (one-byte array per partition). It is more space efficient as compared to deserialized objects, especially when it uses fast serializer. But it increases the overhead on CPU. In this level the storage space is low, the CPU computation time is high and the data is stored in-memory. It does not make use of the disk.

d. MEMORY_AND_DISK_SER:
It is similar to MEMORY_ONLY_SER, but it drops the partition that does not fits into memory to disk, rather than recomputing each time it is needed. In this storage level, The space used for storage is low, the CPU computation time is high, it makes use of both in-memory and on disk storage.

e. DISK_ONLY:
In this storage level, RDD is stored only on disk. The space used for storage is low, the CPU computation time is high and it makes use of on disk storage.
			
Hence, Caching or persistence are the optimization techniques for interactive and iterative Spark computations. It helps to save intermediate results so we can reuse them in subsequent stages. These intermediate results as RDDs are thus kept in memory (default) or more solid storages like disk and/or replicated.


#### 4) Explain the difference between Spark SQL and Hive

	
Apache Hive and Spark SQL perform the same action, retrieving data, each does the task in a different way.
		 
Apache Hive:

Apache Hive is built on top of Hadoop. Moreover, It is an open source data warehouse system. Also, helps for analyzing and querying large datasets stored in Hadoop files. At First, we have to write complex Map-Reduce jobs. But, using Hive, we just need to submit merely SQL queries. Users who are comfortable with SQL, Hive is mainly targeted towards them.
			
Spark SQL:

In Spark, we use Spark SQL for structured data processing. Moreover, We get more information of the structure of data by using SQL.  Also, gives information on computations performed. One can achieve extra optimization in Apache Spark, with this extra information. Although, Interaction with Spark SQL is possible in several ways. Such as DataFrame and the Dataset API.	
		

#### 5) Explain Partitions and SparkContext?

Partition in a spark is a logical chunk of a large data set.

Very often data we are processing can be separated into logical partitions (ie. payments from the same country, ads displayed for given cookie, etc). In Spark, they are distributed among nodes when shuffling occurs.
	
Spark’s partitioning feature is available on all RDDs of key/value pairs.
	
For one, quite important reason — performance. By having all relevant data in one place (node) we reduce the overhead of shuffling (need for serialization and network traffic).
	
Also understanding how Spark deals with partitions allow us to control the application parallelism (which leads to better cluster utilization — fewer costs).
	
	
	"""
		"""
		
		from pyspark import SparkContext
		# The default data used for calculations
		nums = range(0, 10)
		print(nums)
		
		"""
		
		
		"""
		Output:
			[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]	
		"""
	
	"""
	
	
	
	"""
		"""
			with SparkContext("local") as sc:
				rdd = sc.parallelize(nums)			
				print("Number of partitions: {}".format(rdd.getNumPartitions()))
				print("Partitioner: {}".format(rdd.partitioner))
				print("Partitions structure: {}".format(rdd.glom().collect()))
			
		"""
	
		"""
			Output:
				Number of partitions: 1
				Partitioner: None
				Partitions structure: [[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]]
		
		"""
	"""

	Here, Data is distributed across one local core. Now let’s try to allow our driver to use two local cores.

	"""
		"""
		with SparkContext("local[2]") as sc:
			rdd = sc.parallelize(nums)
			
			print("Default parallelism: {}".format(sc.defaultParallelism))
			print("Number of partitions: {}".format(rdd.getNumPartitions()))
			print("Partitioner: {}".format(rdd.partitioner))
			print("Partitions structure: {}".format(rdd.glom().collect()))
		
		"""
		
		"""
		Output
		Default parallelism: 2
		Number of partitions: 2
		Partitioner: None
		Partitions structure: [[0, 1, 2, 3, 4], [5, 6, 7, 8, 9]]
		"""
	"""

	The data is distributed across two partitions and each will be executed in a separate thread.


#### 6) Write a Scala function which takes a list and a target number and returns combination of numbers whose sum to the target number
	
```scala
		// Scala
		// Time Complexity: O(n)
		object getThePairs 
		{ 
			def main(args: Array[String]):Unit=
			{         
			  val myList= Array(1, 10, 4, -1,6,6,12,0)
			  var n: Int = 16
			  println("Pairs founds are:")
			  printPairs(myList,n); 
			} 

			def printPairs(arr:Array[Int], n:Int)
			{ 
			  var ret = Array()
			  var s = Set[Int]()
			  var diff: Int = 0
			  for (i <- (0 to arr.length - 1))
			  {
				diff = n - arr(i)
				  if (s.contains(diff))
				  {
				   println(diff, arr(i))
				  }
				else
				{
				  s += arr(i)
				}
			  }
			} 
		} 

```


```python
		# Python - Method 1: 
		# Time complexity: O(n^2)

		def getPairs(arr, req_sum):
			for i in range(len(arr)): 
				for j in range(i + 1, len(arr)): 
					if arr[i] + arr[j] == req_sum: 
						print(arr[i], '\t', arr[j])

		arr = [1, 5, 7, -1] 
		n = len(arr) 
		req_sum = 6
		getPairs(arr, req_sum)

```

```python
		# Python - Method 2: 
		# Time complexity: O(n)			
		def getPairs1(arr, s):
			ret = []
			h = ()
			for i in range(len(arr)):
				diff = s - arr[i]
				if diff in h:
					r = [diff, arr[i]]
					ret.append(r)
				else:
					h = h + (arr[i],)
			print(ret)

		arr = [1, 10, 4, -1,6,6,12,0] 
		n = len(arr) 
		req_sum = 10
		getPairs1(arr, req_sum)

```


	


#### 7) There are 2 lists; one with birth year, other one with death year. Write Scala program to find out which year people lived the max.




#### 8) How do you remove elements with a key present in the other RDD?

	Using subtractByKey(rdd_key):

	Two pair of RDDs: (rdd = {(1, 2), (3, 4), (3, 6)} other = {(3, 9)})
	rdd.subtractByKey(other) ==============>   {(1, 2)}


## General/Java Questions

#### 1) Difference between List and Set data structures?

##### List:
		
List is the collection of items (Data types can be same or different) ordered in a linear sequence.

Lists are implemented either as linked lists (singly, doubly, circular, …) or as dynamic array.

It allows positional access. You can access any elements by its position.

List allows duplicates


##### Sets:

Sets, is an unorder collection of items, with no repeated values. By unorder means there is no index like lists.

You can use Sets, When all what you need is a bunch of items into it, where you don’t care about the sequence. There is no specific sequence as with a linked list, or a stack, or a queue. There is no key-value pairs as with a hash table.

Unlike an array, or values in an associative array, or a linked list, sets do not allow duplicates. You cannot add the same object, the same value twice to the same set.

Sets are designed for very fast lookup, to very quickly be able to see if we already have a value contained in a collection.
You can also iterate through all the elements in a set, you just may not have any guaranteed order.


#### 2) Why is String immutable (or final) in Java?
The string is Immutable in Java because String objects are cached in String pool. Since cached String literals are shared between multiple clients there is always a risk, where one client's action would affect all another client. For example, if one client changes the value of String "Test" to "TEST", all other clients will also see that value as explained in the first example. Since caching of String objects was important from performance reason this risk was avoided by making String class Immutable. At the same time, String was made final so that no one can compromise invariant of String class e.g. Immutability, Caching, hashcode calculation etc by extending and overriding behaviors.

The string is made final to not allow others to extend it and destroy its immutability.

Security: Parameters are typically represented as String in network connections, database connection URLs, usernames/passwords, etc. If it was mutable, these parameters could be changed easily.

Synchronization and Concurrency: making String immutable automatically makes them thread safe thereby solving the synchronization issues.

Caching: when compiler optimizes our String objects, it seems that if two objects have the same value (a =" test", and b =" test") and thus we need only one string object (for both a and b, these two will point to the same object).

Class loading: String is used as arguments for class loading. If mutable, it could result in the wrong class being loaded (because mutable objects change their state).


#### 3) What does “final” keyword achieve for a class, method or variable?

Final Keyword in Java is used to finalize the value of a variable, class or method for the entire program. 

Final keyword is used in different context,

Final Variable -------> To create constant variable

We must initialize a final variable, otherwise compiler will throw compile-time error.A final variable can only be initialized once, either via an initializer or an assignment statement. There are three ways to initialize a final variable :

You can initialize a final variable when it is declared.This approach is the most common. A final variable is called blank final variable,if it is not initialized while declaration. Below are the two ways to initialize a blank final variable.

A blank final variable can be initialized inside instance-initializer block or inside constructor. If you have more than one constructor in your class then it must be initialized in all of them, otherwise compile time error will be thrown.

A blank final static variable can be initialized inside static block.

Final Methods  -------> To prevent method overriding

When a method is declared with final keyword, it is called a final method. A final method cannot be overridden. The Object class does this—a number of its methods are final.We must declare methods with final keyword for which we required to follow the same implementation throughout all the derived classes.

Final Classes  -------> To prevent Inheritance

When a class is declared with final keyword, it is called a final class. A final class cannot be extended(inherited). There are two uses of a final class :

One is definitely to prevent inheritance, as final classes cannot be extended. For example, all Wrapper Classes like Integer,Float etc. are final classes. We can not extend them.
	final class A
	{
		 // methods and fields
	}
	// The following class is illegal.
	class B extends A 
	{ 
		// COMPILE-ERROR! Can't subclass A
	}
The other use of final with classes is to create an immutable class like the predefined String class.You can not make a class immutable without making it final.


#### 4) When would you have a private constructor in a class?

Like any method we can provide access specifier to the constructor. If it’s made private, then it can only be accessed inside the class.

There are various scenarios where we can use private constructors. The major ones are

1. Singleton class design pattern:
	In this, We can restricts the instantiation of class and ensures that only one instance of the class exists.

2. To Prevent Subclassing:
	If we create private constructor, No class can extend your class, because it can't call the super() constructor. This is some kind of alternative for final class.

3. Builder Design Pattern:
	Private constructor can also used in builder design pattern and thus creating Immutable classes as well.


#### 5) What does a “synchronized” method or code block achieve?
Java is multi-threaded language where multiple threads runs parallel to complete their execution. We need to synchronize the shared resources to ensure that at a time only one thread is able to access the shared resource.

If an Object is shared by multiple threads then there is need of synchronization in order to avoid the Object’s state to be getting corrupted.

Java programming language provide two synchronization idioms:

1.Methods synchronization:
	Synchronized methods enables a simple strategy for preventing the thread interference and memory consistency errors. If a Object is visible to more than one threads, all reads or writes to that Object’s fields are done through the synchronized method.

2.Block synchronization:
	If we only need to execute some subsequent lines of code not all lines (instructions) of code within a method, then we should synchronize only block of the code within which required instructions are exists.


#### 6) Why does a “wait()” and “notify()” need to be within a “synchronized” block? How does these calls help in inter thread communication?

To tackle the multithreading problem, methods like Wait and Notify in Java are used. The Object class uses these three final methods that allow threads to communicate about the locked status of a resource.

Wait()
	This method causes the thread to wait until another thread invokes notify() and notifyAll() methods for this object. This Wait() method tells the calling thread to let go of a lock and go to sleep until some other thread enters the same monitor and calls to notify(). This method releases the lock before waiting and reacquires the lock before returning from the wait() method.

Wait() method is tightly integrated with the synchronization lock. This is done by using a feature not available directly from the synchronization mechanism.


Notify()
	This method is used to notify the threads that it needs to function. It wakes up one thread that called the wait() method on the same object.

Note that calling notify() eventually does not give up a lock. It tells a waiting thread that it can wake up. However, the lock is not actually given up until the notifier’s synchronized block has completed. Now say, if you call notify() on a resource but the notifier still needs to perform actions for 10 seconds within its synchronized block, the thread that had been waiting will have to wait at least for another additional 10 seconds for the notifier to release the lock on the object, even though notify() had been called.

#### 7) Write a function to remove duplicates from an unsorted linked list?


```python
## Python: 
		
class Node():
#Single node:

def __init__(self, data):
	self.data = data
	self.nextNode = None

def __str__(self):
	return str(self.data)

class LinkedList():
#Create singly linked list:
def __init__(self, linkedList):
	self.head = None
	self.add(linkedList)

def add(self, linkedList):
	for data in reversed(linkedList):
		node = Node(data)
		node.nextNode = self.head
		self.head = node

def printList(self):
		node = self.head
		if node is not None:
			print (node,)
			node = node.nextNode

		while node:
			print (node)
			node = node.nextNode
		print ("\n")

def removeDuplicates(linkedList):
previousNode = linkedList.head
currentNode = previousNode.nextNode

keys = set([previousNode.data])

while currentNode:
	data = currentNode.data

	if data in keys:
		previousNode.nextNode = currentNode.nextNode
		currentNode = currentNode.nextNode
	else:
		keys.add(data)
		previousNode = currentNode
		currentNode = currentNode.nextNode

print ("After removing the duplicates:")
linkedList.printList()

list1 = [1, 2, 3, 4, 5, 3, 5, 4]
list2 = ['a', 'b', 'c', 'd', 'c', 'e', 'f', 'b']

l = LinkedList(list1)
l.printList()
removeDuplicates(l)

l = LinkedList(list2)
l.printList()
removeDuplicates(l)
```

## Question 1: Please write a Python script that:
 Reads the JSON located at http://mysafeinfo.com/api/data?list=englishmonarchs&format=json
 Outputs a JSON object consisting of lists of unique 'nm', grouped by 'cty' and 'hse'
 

		Example output:
		{
			 "cty1": {
			   "hse1": [
			     "name1", 
			     "name2"
			   ],
			   "hse2": [
			     "name1", 
			     "name2" 
			   ]      
			 },
			 "cty2": {
			   "hse3": [
			     "name1", 
			     "name2"
			   ],
			   "hse3": [
			     "name1", 
			     "name2" 
			   ] } }

```python

import json
import urllib.request
url = "https://mysafeinfo.com/api/data?list=englishmonarchs&format=json"
data = urllib.request.urlopen(url).read().decode()
data = json.loads(data)

print("Json Data read from")
print ("https://mysafeinfo.com/api/data?list=englishmonarchs&format=json")
print ()
print(data)
#print(type(data))

"""
[
    {'ID': 1, 'Name': 'Edward the Elder', 'Country': 'United Kingdom', 'House': 'House of Wessex', 'Reign': '899-925'}, 
    {'ID': 2, 'Name': 'Athelstan', 'Country': 'United Kingdom', 'House': 'House of Wessex', 'Reign': '925-940'}, 
    {'ID': 3, 'Name': 'Edmund', 'Country': 'United Kingdom', 'House': 'House of Wessex', 'Reign': '940-946'}, 
    {'ID': 4, 'Name': 'Edred', 'Country': 'United Kingdom', 'House': 'House of Wessex', 'Reign': '946-955'}, 
    {'ID': 5, 'Name': 'Edwy', 'Country': 'United Kingdom', 'House': 'House of Wessex', 'Reign': '955-959'}
]
"""

op = {}
country = []
house = []
for item in data:
    #print (item,"\n")
    for key in item:
        if key == 'Country':
            if item[key] not in country:
                country.append(item[key])
                
        if key == 'House':
            if item[key] not in house:
                house.append(item[key])                
#print(country)
#print(house)    

for con in country:
    for hos in house:
        nam = []
        for item in data:
            if con in item["Country"] and hos in item["House"]:
                nam.append(item["Name"])
        op = [{con:{hos: nam}}]

print()
print("Output Json:")        
print(op)

```


#### Question 2: Please write a Python program that:
	Reads the JSON located at https://data.cityofnewyork.us/api/views/25th-nujf/rows.json
	Maps the 'name' from each field in "columns, available at JSON_ROOT['meta']['view']['columns'], to each list inside JSON_ROOT['data']. (e.g. the name of the first field listed in "columns" is the name of the first item in each list in "data")
	Outputs a JSON file containing only data for the following fields: ["Child's First Name", "Gender", "Ethnicity", "Year of Birth", "Rank", "Count"]
	Filters the aforementioned data to only the years 2012-2014 (inclusive), then groups it- first by "Child's First Name" and then "Ethnicity"- and provides the sum of "Count" for each combination.
	The resulting data should be written both to JSON and to CSV.


##### Question 3: Write Python program to implemenet quick sort for below list:
 	random_list_of_numbers = [22,5,1,18,99]
 
 
 ```python
 def merge_sort(A):
    l = len(A)
    if l<2:
        return A
    else:
        mid = l//2
        
        left = A[:mid]
        right = A[mid:]
        
        merge_sort(left)
        merge_sort(right)
        
        merge(left, right, A)
    return A
    
def merge(left, right, A ):
    nl = len(left)
    nr= len(right)
    i = 0
    j = 0
    k = 0
    
    while(i<nl and j<nr):
        if left[i]<=right[j]:
            A[k]=left[i]
            i+=1
        else:
            A[k]=right[j]
            j+=1
        k+=1
    while i < nl:
        A[k]=left[i]
        i+=1
        k+=1
    while j<nr:
        A[k]=right[j]
        j+=1
        k+=1
    return A

def main():
    A = [22,5,1,18,99] 
    print("Array to be sorted are:\n", A, "\n")
    
    A = merge_sort(A)
    print ("Merge Sorted array:\n", A) 
main()
 ```
 
 
 
 ```python
def partition(arr,low,high): 
    i = ( low-1 )         
    pivot = arr[high]
    for j in range(low , high): 
  
        if   arr[j] < pivot: 
          
            i = i+1 
            arr[i],arr[j] = arr[j],arr[i] 
  
    arr[i+1],arr[high] = arr[high],arr[i+1] 
    return ( i+1 ) 


# Function to do Quick sort 
def quickSort(arr,low,high): 
    if low < high: 

        pi = partition(arr,low,high) 

        quickSort(arr, low, pi-1) 
        quickSort(arr, pi+1, high) 
  
arr = [22,5,1,18,99] 
print("Array to be sorted are:\n", arr, "\n")
n = len(arr) 
quickSort(arr,0,n-1) 
print("Quick Sorted array:\n",arr, "\n") 
 ```

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


#### 3) What is the difference between persist() and cache()

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


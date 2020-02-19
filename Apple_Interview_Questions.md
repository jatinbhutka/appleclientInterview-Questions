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

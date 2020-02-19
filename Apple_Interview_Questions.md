<center>Apple Client Interview Questions:</center>


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


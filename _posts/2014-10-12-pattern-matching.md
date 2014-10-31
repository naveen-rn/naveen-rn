---
layout: post
title: Scala - Pattern Matching.
categories: programming languages
tags: 
  - programming languages
  - scala
  - functional programming
comments: false
mathjax: null
featured: true
published: true
---

Pattern Matching in Scala !

The secret of match feature in Scala is the concept of partial functions. In relation to a function, we can define partial function as a mapping from a subset of input values to an output. Thus partial functions can be valid only for certain range of values and undefined for other values in that domain.

For example, consider the function on which given an integer, populates inverse of that integer. As we know, the input "Zero" to this function must be invalid. So, we can write the partial function inverse as below:

    val inverse: PartialFunction[Int, Double] = {
     case x if x != 0 => (1/x)
    }

    println(inverse.apply(10))
    println(inverse(-5))
    println(inverse(0))

As we can see, the partial function "inverse" here is actually an object. To execute this partial function, we will have to call "apply" method on the object either explicitly or implicitly as shown in the example above. When we try to print inverse of 10 and -5, the output is as expected. But, when we invoke partial function inverse on zero, the code throws a match error since the result for this invalid input is undefined. We can even query whether a given input is valid for a partial function using isDefinedAt(input_parameter) method on it.

Now consider the use of match below:

    def check(data : Any) = {
      data match {
        case 5 => println("got 5")
        case 10 => println("got 10")
      }
    }

"Match" keyword in Scala gives us an ability to specify a group of cases, like the partial function that works on any kind of object. Just like the partial function inverse was undefined for zero, the example above recognize that only 5 and 10 are acceptable values and result for any other input is undefined. We can implement above example with our own partial function too and make it more reusable and add input validity checking to it.

From above discussion, we might infer that since match is so similar to a partial function, it must be implemented internally using partial functions. But inferring so would be incorrect. Match looks like a partial function, but it is really implemented as a combination of if-else statements where the predicate is generated based on pattern. If we see the byte code of the check function, it looks as shown below:

           0: aload_1       
           1: astore_2      
           2: iconst_5      
           3: invokestatic  #16 
           6: aload_2       
           7: invokestatic  #20   
          10: ifeq          28
          13: getstatic     #26   
          16: ldc           #28   
          18: invokevirtual #31    
          21: getstatic     #37    
          24: astore_3      
          25: goto          52
          28: bipush        10
          30: invokestatic  #16    
          33: aload_2       
          34: invokestatic  #20     
          37: ifeq          53
          40: getstatic     #26     
          43: ldc           #39 
          45: invokevirtual #31     
          48: getstatic     #37     
          51: astore_3      
          52: return        
          53: new           #41      
          56: dup           
          57: aload_2       
          58: invokespecial #44       
          61: athrow        

From line 10 and 37, we can see that the value 5 and 10 is checked respectively by using "ifeq"  and if none of them matches, a match error is thrown. If instead of integer literal, we use complex objects like lists or guards, the predicates are generated accordingly and the unbounded variables are bounded. Sometimes the 'instance of' check is applied before binding the variables.

Another interesting feature is that, from Scala version 2.8 the @switch annotation has been introduced. This is similar to the pattern matching, with a goal to ensure that the pattern matching will be compiled into tableswitch or lookupswitch instead of a series of if-else conditions as shown above. 

Thus, we can conclude that pattern matching in Scala is achieved using if-else blocks even though it looks similar to a partial function.

P.S; This article was written along with Amita(amitakulkarni8@gmail.com).
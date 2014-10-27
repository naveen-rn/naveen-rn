---
layout: post
title: Statically typed languages
description: "Statically typed languages"
headline: "Variables in Statically typed languages"
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

>&quot;A statically typed language verifies the type of variables and objects at compile time. In order for this
to work, when programming in a statically typed language, we specify the type for each variable or object in code.&quot;

A process of analyzing a program to ensure that the types of expressions are consistent throughout the program is called as Type Checking. A programming language is said to be statically typed, if the type of the variable or an object is known during the compile time. The general examples of statically typed languages are C, C++, C#, Java, Fortran, Haskell, Perl and Scala. 

We can develop our discussion based on the following Fortran code,

```
program simple

    integer     :: a(4)
    
    a = 98.99
    
    print *, a

end program simple
```


The program now will print only 98 instead of 98.99. So, this example shows that usually in statically typed language the type of the variable or object should be known during compile time and it can't be modified during runtime. It is usually believed that in order to achieve this, we need to specify the type for each variable or object in code as we have mentioned the variable "a" to be of type integer in the above code.

Consider a sample Haskell code;

```
a = [1, 1, 1, 1]
main = do
    print list
```

And a Ruby code;

```
a = Arrays.new(1, 1, 1, 1)
print a
```

Though it might look the same in both Haskell and Ruby, they are statically and dynamically typed, respectively. Haskell uses the traditional Hindley-Milner (HM) polymorphic type system. The most important property of HM type system is its ability to deduce the most general type of a given program without the need for any type annotations or other hints supplied by the programmer. OCaml is yet another static typed programming language of this sort.

This type checking is also one of the important features of Haskell, which sets it apart from other programming languages. A type signature of the Haskell program will look something like this;

```
functionName :: arg1Type -> arg2Type -> arg3Type -> ....... -> argNType
```

Hence, the above example shows how a language can be statically typed without explicitly specifying the type of the object. Usually the compiler determines and assigns the type to object/variable. These languages also perform the job of typecasting the variable/object to a different compatible type for a valid assignment. This allows us to have some flexibility with static type languages. For example, the code below will compile in Java:

```
float num = 5.5;
num = 3;
```

But it is not always possible even for statically typed languages to verify the type at compile time and display errors if there is a wrong assignment. Sometimes, compiler cannot infer the right type of an object or variable at compile time and an executable can be generated with incorrect type assignments.

```
public class Test {
public static void main(String args[]) {
    List <Integer> numbers = new ArrayList <Integer> ();
    numbers.add(1);
    addToList(numbers);     //String is added to the list
    int total = numbers.get(0) + numbers.get(1);
}

private static void addToList(List myList) {
    myList.add("Hello");
}   
}
```

The above code compiles perfectly. But, as we can see the string "Hello" is added to list of "only" integers, which is a wrong type assignment. As expected, the code throws an exception at runtime while trying to add the two list elements. 

Statically type languages thus help us avoid a lot of mistakes in the code by type checking information at compile time. But, it will be incorrect to assume that a compiled code of a language always has correct typing assignments just because it is statically typed language. We should always test for typing, even in such languages to ensure that the code performs the expected operations.

From, the above discussion we can conclude that type checking in a statically typed language checks the type of the variables and objects at compile time. But, this does not necessarily identify all the errors during compilation. And for the static type checking to work, there is no standard rule that a programmer should specify the each variable or object type in the code.

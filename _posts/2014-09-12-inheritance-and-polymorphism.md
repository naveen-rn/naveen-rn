---
layout: post
title: Inheritance & polymorphism.
description: "Inheritance is essential to support polymorphism."
headline: "Discussion on whether Inheritance is essential to support polymorphism"
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

"Inheritance is essential to support polymorphism."

In Object Oriented Programming, Polymorphism is defined as the ability of an object to be able to take multiple forms. Inheritance is one of the ways of reusing code, by obtaining all the code of the base class, without the duplication of code. In that way you can extend your object only where it is needed and leave the rest of implementation untouched. Polymorphism through inheritance comes very natural because you are guaranteed that the method exist. So the only thing the compiler is left to check, is if in the tree of classes at some point, there exists the object that is expected by the method. But this is just a way to apply the concept of polymorphism, not what it is actually means. 

Polymorphism can also be implemented in some languages by simply applying the method on a received object. The compiler doesn't check if the object truly has such a method because it doesn't know the type which is known only at the runtime. So at runtime it checks whether there exist such a method and simply calls it with the implementation that each object has provided. In that way the burden of correctness verification lies heavily on the side of the caller. 

Static type checking in programming languages involves the consistency check before the program runs. Object Oriented Languages like C++, Java, C# support a strong static type checking, while languages like Python, Ruby are those with only a generic type for variable declaration. This type checking forms the base in determining the relationship between inheritance and polymorphism.  

In static type checked languages, polymorphism is inherently dependent on inheritance or we can even say in order to have polymorphism we need to have some kind of inheritance. Let us consider the following code snippet to understand this relationship.

    class Carbon
    {
        public virtual boolean ProductType() = 0;
    }

    class Diamond : Carbon 
    {
        public boolean ProductType()
        {
            //implement carbon ratio and 
            //other Product Properties
        } 
    }

    class Graphite : Carbon 
    {
        public boolean ProductType()
        {
            //implement carbon ratio and 
            //other Product Properties
        } 
    }

    Carbon Allotrope[] = { new Diamond(), new Graphite() };

    for( int buffer = 0; buffer < 2; buffer++ )
        Allotrope[buffer].ProductType();


In this example, the Allotrope array of type Carbon can only hold those objects which are derived from Carbon, i.e Diamond and Graphite. Thus polymorphism works like a charm in this case. But, when we add an extra Allotrope say Buckyball as shown below,

    class Buckyball
    {
        public boolean ProductType()
        {
            //implement carbon ratio and other Product Properties   
        }
    }

    Carbon Allotrope[] = { new Diamond(), new Buckyball() };

    for( int buffer = 0; buffer < 2; buffer++ )
        Allotrope[buffer].ProductType();

The compiler would generate a compile time error when BuckyBall is added. Because BuckyBall is not derived from Carbon. This is because of the static type check. This means that in all strongly typed checked languages, polymorphism is possible to be implemented through inheritance. 
In such languages (Java or C#) exist workarounds to bypass these "constraints". One of these is use of RTTI(Run Time Type Information) libraries. By identifying an object type at runtime, and recasting it to an object of another hierarchy, we can break the Inheritance. Of course that will require several if statements, so that the correct method depending from the type can be applied.
That approach breaks the encapsulation, and makes the code dependent on the "guts" of objects which were not intended to be used by application programmers, and can change without notice. Of course in cases that we want to try a new approach in a problem, such a quick hack might be actually very welcome, to verify that the goal can be implemented in such a way, but then refactoring must not be neglected. 

In brief, polymorphism is basically a way to communicate and inheritance is a way to reuse code, and they are independent. But languages like Java and C++ force the user to inherit from interfaces or classes just in order to provide polymorphism.

Now let us think on the design aspects. This tight link between inheritance and polymorphism creates a huge negative impact on the design. Hence Interface was introduced in these statically type checked languages. But there are languages which provides pure polymorphism without the usage of Inheritance. Python, Ruby comes under those categories. Does this mean , we can completely neglect Inheritance? If inheritance is neglected, then we have to implement a workaround in analyzing the missing methods, when type checking is deferred to run time.

This is where the implementation of Delegation to avoid the usage of inheritance takes place. Delegation is a way of reusing  and extending  the behavior of a class. It works by writing a new class that incorporates the functionality of the original class by using an instance of the original class and calling its methods. Delegation can be considered as a most generalized version of Inheritance. 

An example of the design ramifications that the tight coupling of Inheritance with Polymorphism can be seen in the following example. You need to modify some class A to fix a problem or add a feature; it is decided to leave A alone and introduce a new class A'. Depending on whether or not A' must be substitutable for A, non polymorphic inheritance might be a good technique. That allows for easy introduction of classes that implement more than one classes. It allows for fast development. The fact the need for Interfaces is non existence in polymorphism without inheritance, changes the necessary number of classes for the representation drastically, and exponentially with the size of the initial design. That alone is a great change in design practice and agility. 

One other aspect of polymorphism, which hasn't yet been discussed is the object polymorphism which can be seen at templates. In such cases we actually create a relationship in width and not in depth as inheritance. That kind of relationship ends up in objects that may (or not depending on the language implementation) have hierarchical relationships. This type of polymorphism is obviously totally independent from Inheritance.

What we infer from the above analysis is that object oriented languages are capable of inclusive use of inheritance, where everything that is relative being modeled with inheritance in practice should be accepted as a huge mistake. Hence, Inheritance should be made exclusive and should be confined in usage to those relations that occur naturally by domain and not by deign.

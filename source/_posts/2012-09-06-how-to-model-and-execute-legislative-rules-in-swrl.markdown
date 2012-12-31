---
comments: false
date: 2012-09-06 21:39:39
layout: post
slug: how-to-model-and-execute-legislative-rules-in-swrl
title: How to model and execute legislative rules in SWRL
wordpress_id: 157
categories:
- howto
tags:
- owl
- pellet
- swrl
---

=Prequisites=

Download and install:
* Pellet reasoner: http://clarkparsia.com/pellet/


=Source Rules=

In plain English the source rules are:

A person satisfies Section A if either:
* they satisfy both Sections B and C, OR
* they satisfy EITHER Section D or Section E.

Further, a person satisfies Section E if they satisfy BOTH:
* Section F, AND
* Section G.

=Prefixes=

Define a default prefix for this file: 'ls' for 'legislative SWRL'.  The prefix
is a full URI, followed by a '#'.  
```
Prefix: : <urn:ls#>
```

=Ontology Name=

Ontologies have to have a name in the form of an absolute URI:

```
Ontology: 
```

=Basic Classes=

This is our simple method for modelling legislation:
* Each section of the legislation is an instance of the class 'Section'.
* The legislation usually applies to something, such as a transaction, a company, or an amount.  In this case, we assume it applies to a person.  So each person that the legislation applies to is an instance of the class 'Person'.

Further, the same 'thing' cannot be both a person and a section.  We need to express this explicity in OWL by saying the classes are 'disjoint'.


```
Class: Person

    DisjointWith: 
        Section
    
    
Class: Section

    DisjointWith: 
        Person
 

```

=Properties=

A person can satisfy particular sections in the legislation.  For example, a particular person might satisfy Section Y by fulfilling whatever criteria are in Section Y.  If Section Y said 'the person is under 18' and the particular person was in fact under 18, then we say that the person satisfies section Y.

We express this in OWL with an 'object type property' called 'satisfies'.  This is a relationship between classes.  The 'domain' of the property is the class Person.  The 'range' of the property is the class Section. 

You can say this aloud as 'a person satisfies a section'.  Notice that we are referring in general to **a** person, **not** a particular person at this point.  A particular person would be 'Bob' or 'Jill'.   The property is **defined** at a more abstract level as a relation between classes, not individuals.  When we create individual instances, they will have this property, but we do not define the property for them - we defined it at the class level.It is important not to get confused between classes and individuals, and between an object type property and instances of the property connecting individuals.
```
ObjectProperty: satisfies

    Domain: 
        Person
    
    Range:
	Section
```         

We can also add some additional characteristics to this object property to communicate more information about it.  In general, the more information we add, the more can be inferred from the ontology.  In this case, we want to express that the property is:
* asymettric, and
* irreflexive.

'Asymetric' means that a person can satisfy a section, but a section cannot satisfy a person.

'Irreflexive' means that a person cannot satisfy themselves (in this context, anyway).

```
    Characteristics: 
        Asymmetric,
        Irreflexive
```


=Individuals=

==Sections===
As discussed above, each particular section of the legislation we will model as an instance of the class 'Section'.  Since there are section 'A' through 'G' in our source rules, we create one individual for each:

```
 
Individual: SectionA
	Types: Section
	
Individual: SectionB
	Types: Section

Individual: SectionC
	Types: Section

Individual: SectionD
	Types: Section

Individual: SectionE
	Types: Section

Individual: SectionF
	Types: Section

Individual: SectionG
	Types: Section
```


=Rules=

The rules contain the logic that glues together the sections so tthey apply to a person.  Since we have defined the person class and individuals for the praticular sections, we can now write the rules to capture the logic.

Recall the first part of the source rules were that a person satisfies Section A if either:
* they satisfy both Sections B and C, OR
* they satisfy EITHER Section D or Section E.

Recall that in SWRL, rules consist of a head and a body, and all the clauses in the body have to be true for the head to be true.  You cannot have a disjunction in the body of a rule - you need to create separate rules for disjunctions.

So this rule above really breaks down to **three** rules, showing that a person may satisfy section A **three** ways:
Rule 1:  A person satisfies Section A if they satisfy sections B AND C.
Rule 2: A person satisfies Section A if they satisfy Section D.
Rule 3: A person satisfies Section A if they satisfy section E.

The rules will apply to any person, so we need a variable for person.  The variable has to have a full URI for a name, so we'll call it 'urn:anyPerson' just to make it clear that this variable represents any person.

In SWRL, Rule 1 is :

```
Rule:
Person(?), satisfies(?,SectionB), satisfies(?,SectionC) -> satisfies(?,SectionA)
```

This consists of three clauses in the body, separated by a comma, followed by the head.

The first clause 'Person' binds all instances of the class Person to the variable 'urn:anyPerson'.  The predicate will be true if there is an instance of the class Person in our ontology.  (There isn't yet as we haven't defined one yet, but we will shortly.)  This is so we can refer to this set of persons in the rest of the rule.

The second clause looks for persons with the object type property 'satisfies' connecting to the individual 'SectionB'. We have already defined the individual 'SectionB'.  So this clause should identify a set of people that satisfy section B.  Similarly, the third clause identifies people that satisfy SectionC.

If all three of those clauses are true for a given person, we know that person should satisfy Section A.  The clause in the head of the rule expresses this.

So the overall effect of that rule is that for every person that satisfies section B and Section C, that person is inferred to satisfy Section A.  The rule will applies to multiple people if there are multiple people defined in the ontology.

Rules 2 and 3 follow the same pattern.

The last rule we need to write says that a person satisfies section E if they satisfy both Section F and Section G.  This time Section E is in the head of the rule rather than the body:
```
Rule:
Person(?), satisfies(?,SectionF), satisfies(?,SectionG) -> satisfies(?,SectionD)
```

Note that the same clause 'satisfies(?,SectionD)' appears in the head of this rule, but the body of Rule 3 discussed above.  This means the rules are **chained** together.  The inference of one rule can feed into another rule, so they are all evaluated together.

==Testing the rules==

We can test the rules by creating some instances of the class Person, then running our rules.

For this simple example, we'll just create one person, called 'Person1'.

```
Individual: Person1
	Types: Person
```


For the purpose of this test, we will say the person satisfies Section D and Section E:

```
	Facts: satisfies SectionB
	Facts: satisfies SectionC
```

The expected result is that Person01 also satisfies Section A.

==Running the rules==

We'll demonstrate running the rules using the Pellet reasoner from the command line.  You can also  use Pellet from within Protege 3.x and 4.x.

First, save the ontology you have built up as 'legislativeSwrl.owl'.

For convenience, create an environment variable that contains the full path of the this file, called 'LS' for 'Legislative SWRL'.  We'll use this in the Pellet commands.

Linux:
```
LS=
```

Change to the directory where you unzipped Pellet (cd ).

The following command asks Pellet to explain whether Person1 satisfies Section A, and for the reasons why:
 
Linux:
```
./pellet.sh explain --property-value urn:ls#Person1,urn:ls#satisfies,urn:ls#SectionA $LS
```

Some things to note:
* we use the '-property-value' switch because 'satisfies' is an object type property.
* we specify the property value we want to explain in the form ,,.  This is: Person1,satisfies,SectionA.  We need to use the full URIs in the for the Pellet command line however.  The full URI's begin with <urn:ls#> because this was the default prefix we defined in our ontology (see above).

The output of this command is:

```
Axiom: Person1 satisfies SectionA

Explanation(s): 
1)   Rule(Emission(?urn:anyPerson), satisfies(?urn:anyPerson, SectionB), satisfies(?urn:anyPerson, SectionC) -> satisfies(?urn:anyPersone, SectionA))
     Person1 satisfies SectionB
     Person1 type Person
     Person1 satisfies SectionC

```

The first line of the result tells us that Person1 does indeed satisy SectionA.  This accords with our expected result.

The explanation tells us **why** Person1 satisfies Section A in terms of our ontology.  In plain English, it tells us that Person1 satisfies Section A because they satisfy Section B and C, Person 1 is an individual of the 'Person' class and because of the rule we defined.  

Note that Pellet has identifed only the **relevant** information from our ontology.  It has not listed any of the other rules, or any of the irrelevant sections.

===What if there are multiple ways to satisfy a section?===

In the test above, there is only one way that Person1 can satisfy Section A given the facts we provided: because they satisfy both sections B and C.  In other cases though, there may be multiple routes to the same conclusion.  To test this, change the facts for Person1 from:


```
	Facts: satisfies SectionB
	Facts: satisfies SectionC
```

... to ...


```
	Facts: satisfies SectionD
`	Facts: satisfies SectionE
```

Recall from the source rules that a person satisfies Section A if they satisfy **either** Section D **or** Section E.  In the new facts, Person1 satisfies **both** - so there are two ways they can satisfy Section A.

Change the Pellet explain command to show up to 10 explanations:

Linux:
```
./pellet.sh explain --max 10 --property-value urn:ls#Person1,urn:ls#satisfies,urn:ls#SectionA $LS
```

The output is:

```
Axiom: Person1 satisfies SectionA

Explanation(s): 
1)   Person1 type Person
     Person1 satisfies SectionD
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionD) -> satisfies(?urn:anyPerson, SectionA))


2)   satisfies domain Person
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionE) -> satisfies(?urn:anyPerson, SectionA))
     Person1 satisfies SectionE


3)   satisfies domain Person
     Person1 satisfies SectionD
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionD) -> satisfies(?urn:anyPerson, SectionA))


4)   Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionE) -> satisfies(?urn:anyPerson, SectionA))
     Person1 type Person
     Person1 satisfies SectionE

```

This shows **four** explanations for why Person1 satisfies SectionA.

Explanation 1 is similar to the one in our first test: Person1 satisfies SectionA because they are a Person, they satisfy Section D, and there is a rule which says any person who satisfies Section D automatically satisfies Section A.

Explanation 3 shows that you can infer Person1 satisies Section A because:
* the domain of the satisfies property is the class 'Person'
* Person1 is in the domain of a satisfies property (in this case the property connected to 'SectionD'), therefore Person1 must be a person.
* The rule discussed above applies.

If Explanation 3 is correct, we should not need to specify explicitly in our ontology that Person1 is a Person.  It should be sufficient to specify that Person1 satisfies SectionE.  To test this, **temporarily remove** the assertion that Person1 is a Person:
```
Individual: Person1

    Types: <-- REMOVE THIS LINE
        Person <-- REMOVE THIS LINE
    
    Facts:  
     satisfies  SectionD,
     satisfies  SectionE
 
```

Now run the Pellet command again.  This time the explanation is:

```
Axiom: Person1 satisfies SectionA

Explanation(s): 
1)   satisfies domain Person
     Person1 satisfies SectionD
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionD) -> satisfies(?urn:anyPerson, SectionA))


2)   satisfies domain Person
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionE) -> satisfies(?urn:anyPerson, SectionA))
     Person1 satisfies SectionE

```

Notice how explanations based on the explicit fact that Person1 is a Person no longer appear. Don't forget to put the lines you removed back in.

Returning to the original explations, we can see Explanation 2 and 4 mirror the original Explanations 1 and 2 except that they refer to Section E.  As expected, this shows us that there are multiple ways the person in our test can satisfy Seciton A: via Section D or via Section E.

==Chaining rules==

Recall that a person satisfies Section A if they satisfy Section E.  Further, a person satisfies Section E if they satisfy both Section F and G.  Therefore, a person who satisfies Sections F and G should automatically satisfy Section A - because the rules chain together.

To test this, change the facts about Person1 to:
```
Individual: Person1

    Types: 
        Person
    
    Facts:  
     satisfies  SectionF,
     satisfies  SectionG
 
``` 

Now run the Pellet command again.  The first explanation is:

```
Axiom: Person1 satisfies SectionA

Explanation(s): 
1)   Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionF), satisfies(?urn:anyPerson, SectionG) -> satisfies(?urn:anyPerson, SectionD))
     Person1 satisfies SectionF
     Person1 type Person
     Rule(Person(?urn:anyPerson), satisfies(?urn:anyPerson, SectionD) -> satisfies(?urn:anyPerson, SectionA))
     Person1 satisfies SectionG


```

This tells us that Person1 satisfies Section A because:
* they satisfy both Sections F and G;
* of the rule which chains together Sections F, G, D;
* of the rule which chains together Section D and Section A.


=The complete ontology=

```
Prefix: : <urn:ls#>


Ontology: 


ObjectProperty: satisfies

    Characteristics: 
        Asymmetric,
        Irreflexive
    
    Domain: 
        Person
    
    Range: 
        Section
    
    
Class: Person

    DisjointWith: 
        Section
    
    
Class: Section

    DisjointWith: 
        Person
    
    
Individual: SectionG

    Types: 
        Section
    
    
Individual: SectionD

    Types: 
        Section
    
    
Individual: SectionC

    Types: 
        Section
    
    
Individual: SectionF

    Types: 
        Section
    
    
Individual: SectionE

    Types: 
        Section
    
    
Individual: SectionB

    Types: 
        Section
    
    
Individual: Person1

    Types: 
        Person
    
    Facts:  
     satisfies  SectionD,
     satisfies  SectionE
    
    
Individual: SectionA

    Types: 
        Section
    
    
Rule: 
    Person(?), satisfies(?, SectionB), satisfies(?, SectionC) -> satisfies(?, SectionA)

Rule: 
    Person(?), satisfies(?, SectionF), satisfies(?, SectionG) -> satisfies(?, SectionD)

Rule: 
    Person(?), satisfies(?, SectionD) -> satisfies(?, SectionA)

Rule: 
    Person(?), satisfies(?, SectionE) -> satisfies(?, SectionA)

```












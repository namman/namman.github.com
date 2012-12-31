---
comments: false
date: 2012-09-04 18:17:46
layout: post
slug: introduction-to-swrl-and-owl
title: Introduction to SWRL and OWL
wordpress_id: 177
categories:
- howto
tags:
- owl
- swrl
---

=Purpose=

The purpose of this tutorial is:
* to show you how to express some basic knowledge and rules using the OWL and SWRL standards;
* make your computer draw conclusions based on that knowledge, so you don't have to.

It is a jump straight in the deep end, but with extensive hand holding and exhaustive explanations.

=Prerequisites=

* No programming experience required
* Must not feel oppressed by computers

==Install Protoge and Pellet==

* Download and install Protege 4.2 following the instructions from the Protege homepage: protege.stanford.edu.
* Once installed, open Protege, select 'Preferences' from the File menu, then select the 'Plugins' tab.
* Click the 'Check for downloads now' button.
* Tick the check box to install the 'Pellet' plugin, and click Install.
* Restart Protege.


==Get a text editor==

You need a plain text editor such as Microsoft Notepad.  Wordprocessing software such as Microsoft Word will not work.


=Knowledge=

The knowledge we want to capture:

Suppose there is a tax break for small business corporations.

A corporation is eligible if:
* it has annual revenue less than $2M, OR
* it has less than five employees.

Our objective is to capture this rule in a way that a computer can apply it to
the particular facts of a given circumstance.


=Ontology=

Create a new file called helloSwrl.owl in your text editor.  You can add the code below progressively.  At the end, you should have the complete ontology - a specification of structured knowledge.

The name of the ontology will be 'hello_swrl'.

We specify this as a 'URI': a unique name that has a special form:
```
	Ontology: 
```
==Define some namespaces==

Namespaces just allow you to give precise names to things in the ontology,
ensuring that different things do not have the same name.  A full name is the
namespace + the local name.  This is similar to how some forms request make you
select 'Mr, Mrs' or whatever as a title - it just reduces the chance of two
different people having the same name. 

Namespace prefixes allow you to use a shorthand way to refer to a namespace
rather than writing out the full namespace every time.
```
	Prefix: : <urn:hello_swrl#>
```
This defines a default namespace for everything that does not otherwise have a
namespace defined.
```
	Prefix: xsd: 
```
Here we are defining the prefix 'xsd' and associating it with the namespace
'http://www.w3.org/2001/XMLSchema#' - a namespace defined by the W3C.
```
    	Prefix: swrlb: 
```
This imports a namespace to do with functions built into SWRL, and gives it the
'swrlb' prefix.

Note that although these namespaces look like a web page address, it does not necessarily mean they point to a web page.

==Define classes==

A class is a group of individuals, like a class in school.  'Individuals' are **particular** things that are members of that class.  Usually both the individuals and the class have names.

For example: 'Year 7 Pottery' is the name of a class of students.  'Bobby Little' is
the name of a boy in that class.  In OWL terms, people would say that Bobby Little is a 'member of' Year 7 Pottery, is an 'individual in' Year 7 Pottery or an 'instance of' Year 7 Pottery.  Bobby Little can of course be members of other classes at the same time.  And the class can exist without Boddy Little or even if there are no students in it.

We'll define a new class called 'Corporation' in the default namespace:
```
	Class: Corporation
```

The corporation has two bits of data associated with that we are interested in:
* Number of employees
* annual revenue

The simplest way to express this is using 'datatype properties'.  Data type
properties express that a particular bit of data may be connected to a
particular individual.

Continuing the school class example above, we may want to express that members
of 'Year 7 Pottery' have a particular grade for the semester.

The properties have **a subject, a predicate and an object**.  These mirror the grammatical subject and object in a sentence.  For example, in the sentence 'the corporation has an annual revenue of $1M', you can identify a subject, predicate and object.  There are actually several ways to identify a subject, predicate and object in this sentence.  You should choose one that makes most sense to humans - the computer does not care so long as you are  consistent.

One way is to say the subject is 'a corporation', the predicate is 'has an annual revenue' and the object is '$1M'.  In OWL, the class that is the subject of a property is called the 'domain' and the class that is the object is called the 'range'.

When we define these datatype properties, we are saying that individuals in this class **can** have these properties.  We are not attaching them to any particular individuals yet.  It is as if we are just setting a placeholder or container for them, which may or may not be filled.  So the datatype properties attach to classes, **not** individuals.  This is a very important distinction.

Hence, we declare a datatype property for annual revenue called 'hasAnnualRevenue':
```
	DataProperty: hasAnnualRevenue
      	  Domain:  Corporation
	  Range: xsd:integer
	  Characteristics: Functional
```
'Domain: Corporation' means that this is a property of the Corporation class.
'Range: xsd:integer' means that this property is an integer.
'Characteristics: Functional' means that each Corporation has only one number for its revenue.
	
We do the same thing again for the number of employees:
```
	DataProperty: hasNumberOfEmployees
    		Characteristics:  Functional
		Domain: Corporation    
		Range: xsd:integer
```
How to we denote whether or not a corporation is eligble? We create a class called 'Eligible'.  Eligible corporations will be members of that class.
```
	Class: Eligible
```
There are two tests in this rule: the annual revenue and the employees test.  We'll just focus on the first limb for the moment.

First we will write the rule in a simplified format so we are sure we understand
it:
```
    Corporation(?corporation) ^ hasAnnualRevenue(?corporation,?revenue) ^ lessThan(?revenue,2000000) -> Eligible(?corporation)
```
The rule has two main parts: the 'body' and the 'head', separated by the '->' characters.  Within the body, there are three 'atoms', separated by the '^' character.

You can think of each atom as a sort of filter applied to all the individuals in the ontology.  The objective is to use the filters to narrow down the the individuals we are interested in.

With a filter, either things pass through or they don't. Another name for a filter is a 'predicate' - an expression that resolves to either true or false.

Each predicate also labels the things that pass through the filter - called
'binding'.  Things that do not pass through the filter are discarded.

The things in this context are individuals in the ontology.  Some pass through
the filter and are bound to a variable.


The first atom:
```
	Corporation(?corporation)
```
This means 'look for individuals in the ontology that are instances of the "Corporation" class.
Bind those individuals to the variable 'corporation'."  (The '?' means it is a variable.)

Since those individuals are bound to ?corporation, we can use them elsewhere in the rule.

The second atom:
```
	hasAnnualRevenue(?corporation,?revenue)
```
This means 'find all the particular individuals which are bound to the ?corporation variable and have the property "hasAnnualRevenue". Then bind the the revenue number for each individual to the variable "revenue".'


The third atom:
```
	lessThan(?revenue,2000000)
```
This means 'filter out revenue numbers less than 2,000,000'.

Recall the atoms in the body all have to be true.  So the combined effect of the atoms above is to select **all individuals which are corporations, have a value for annual revenue, and the value is less than 2,000,000**.  The filters apply cumulatively.

Now we have isolated the individual corporations we are interested in, we want to **make them eligible**.  The head of the rule just takes all individuals bound to the ?corporation variable and makes them members of the class 'Eligible':
```
	Eligible(?corporation)
```
So the effect of the whole rule is **all individuals which are corporations, have a value for annual revenue, and the value is less than 2,000,000 are eligible**.

=Translating to SWRL=

You can see that expressing this in plain English is not really longer than the formal definition which Protege understands. However, in order to encode the rules in SWRL we need to add namespaces and prefixes.  The basic logic and structure is the same.

We need **two** SWRL rules to capture our logic.  This is because the corporation is eligible if it has annual revenue less than $2M, **or** it has less than five employees. 

The first rule:
```
	Rule: 
	Corporation(?), hasAnnualRevenue(?, ?), (?, 2000000) -> Eligible(?)
```
Note:
* We have replaced each variable name with a 'URI' in angle brackets. 
* To do the comparison between the actual revenue and the function, we reference a 'built in' function called 'lessThan' in the 'swrlb' namespace.  This is part of the SWRL specification in the W3C recommendation.


The second rule is the same as the first except that it refers to number of employees instead of revenue:
```
	Rule: 
	Corporation(?), hasNumberOfEmployees(?, ?), (?, 5) -> Eligible(?)
```


=Facts=

So far we have defined a framework for our data, consisting of some classes and properties, and some rules which operate on that data.  Now we can provide some test data.

Our test data consists of three corporations:

Acme Corp: 
* Revenue: $1M dollars.
* Employees: 10

Maas Corp:
* Revenue: $3M dollars
* Employees: 4 
 
Globex Corp:
* Revenue: $5M dollars
* Employees: 15



The expected results are:
* Acme Corp is eligible because it has a revenue of less than $2M dollars.
* Maas Corp is eligible because it has less than 5 employees.
* Globex Corp is **not** eligible because it meets neither of the revenue or employees tests.


The test data:
```
	Individual: AcmeCorp
		Types: Corporation
		Facts: hasAnnualRevenue 1000000
		Facts: hasNumberOfEmployees 5
			
	Individual: MaasCorp
		Types: Corporation
		Facts: hasAnnualRevenue 3000000
		Facts: hasNumberOfEmployees 4

	Individual: GlobexCorp
		Types: Corporation
		Facts: hasAnnualRevenue 5000000
		Facts: hasNumberOfEmployees 15

```


This is the full ontology which should now be saved in your file hello_swrl.owl:

```

Prefix: swrl: 
Prefix: xsd: 
Prefix: swrlb: 
Prefix: : <urn:hello_swrl#>

Ontology: 
 
Class: Corporation
    
Class: Eligible
    
DataProperty: hasNumberOfEmployees

    Characteristics: 
        Functional
    
    Domain: 
        Corporation
    
    Range: 
        xsd:integer
    
    
DataProperty: hasAnnualRevenue

    Characteristics: 
        Functional
    
    Domain: 
        Corporation
    
    Range: 
        xsd:integer
    
   
    
 	Rule: 
	Corporation(?), hasAnnualRevenue(?, ?), (?, 2000000) -> Eligible(?)

	Rule: 
	Corporation(?), hasNumberOfEmployees(?, ?), (?, 5) -> Eligible(?)



	Individual: AcmeCorp
		Types: Corporation
		Facts: hasAnnualRevenue 1000000
		Facts: hasNumberOfEmployees 5
			
	Individual: MaasCorp
		Types: Corporation
		Facts: hasAnnualRevenue 3000000
		Facts: hasNumberOfEmployees 4

	Individual: GlobexCorp
		Types: Corporation
		Facts: hasAnnualRevenue 5000000
		Facts: hasNumberOfEmployees 15

```

=Testing in Protege=

You should now be able to open hello_swrl.owl in Protege.  If you get 'Load Error' dialogue box, there is mostly likely a typo in your ontology.  Click on the 'ManchesterOWLSyntaxOntologyParser' tab.  The information in that dialog box will help you hunt down the error.

From the 'Reasoner' menu, select 'Pellet', then press Ctrl-R to start the reasoner.

You should now be able to click on 'Corporation' in the 'Class hierarchy tab' and see the three companies that are members of that class.

[[image:corporation.png|link=source]]

Then click on the 'Eligible' class and see that only the two companies we expect are members of that class, excluding GlobexCorp.

[[image:eligible.png|link=source]]


Now click on the small '?' next to 'AcmeCorp'.  This will show the reasons why AcmeCorp isEligible.

[[image:explanation.png|link=source]]



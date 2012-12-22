---
comments: false
date: 2012-09-06 22:00:08
layout: post
slug: how-to-query-swrl-rules-with-sparql
title: How to query SWRL rules with SPARQL
wordpress_id: 273
categories:
- howto
tags:
- owl
- sparql
- swrl
---

=Prerequisites=

Download and install Arq which allows you to run SPARQL queries against RDF: http://incubator.apache.org/jena/documentation/query/index.html

Convert your ontology to the Turtle format.  You can do this by using the Save As command in Protege.

=How to run queries=

This Arq command runs the queries and displays output to the console:

{{{
arq --data= --query=

}}}

For example, to run the first query;

* Copy the text of the query into a text file and save it as "query1.rq".
* Save the ontology in Turtle format as "legislativeSwrl.ttl".
* Put both of those files in the same directory and change to that directory.

{{{
arq --data=legislativeSwrl.ttl --query=quer1.rq
}}}


=Find all sections in the head of a rule=
{{{

PREFIX rdf:  
PREFIX swrl: 
PREFIX : <urn:ls#> 
PREFIX list: 
PREFIX owl:  

SELECT DISTINCT  ?headSection 
WHERE {
 	?rule a swrl:Imp . 
	?rule swrl:head ?head .

	?head list:member ?headMember .
	?headMember (swrl:argument1 | swrl:argument2) ?headSection .
	?headSection a owl:NamedIndividual .
	?headSection a :Section .

}
}}}

Output:

{{{

---------------
| headSection |
===============
| :SectionA   |
| :SectionD   |
---------------

}}}

=Find all the sections referenced in the body of a rule=
{{{
PREFIX rdf:  
PREFIX swrl: 
PREFIX : <urn:ls#> 
PREFIX list: 
PREFIX owl:  

SELECT DISTINCT ?bodySection 
WHERE {
 	?rule a swrl:Imp . 
	?rule swrl:body ?body .

	?head list:member ?headMember .
	?headMember (swrl:argument1 | swrl:argument2) ?bodySection .
	?bodySection a owl:NamedIndividual .
	?bodySection a :Section .
}


}}}

Output:

{{{
---------------
| bodySection |
===============
| :SectionB   |
| :SectionC   |
| :SectionD   |
| :SectionA   |
| :SectionE   |
| :SectionF   |
| :SectionG   |
---------------
}}}



The full text of the legislative SWRL example converted to Turtle:

{{{

@prefix : <urn:ls#> .
@prefix dc:  .
@prefix owl:  .
@prefix rdf:  .
@prefix xml:  .
@prefix xsd:  .
@prefix rdfs:  .
@base  .

rdf:type owl:Ontology .


#################################################################
#
#    Object Properties
#
#################################################################


###  urn:ls#satisfies

:satisfies rdf:type owl:AsymmetricProperty ,
                    owl:IrreflexiveProperty ,
                    owl:ObjectProperty ;
           
           rdfs:domain :Person ;
           
           rdfs:range :Section .





#################################################################
#
#    Classes
#
#################################################################


###  urn:ls#Person

:Person rdf:type owl:Class ;
        
        owl:disjointWith :Section .



###  urn:ls#Section

:Section rdf:type owl:Class .





#################################################################
#
#    Individuals
#
#################################################################


###  urn:ls#Person1

:Person1 rdf:type owl:NamedIndividual ,
                  :Person ;
         
         :satisfies :SectionD ,
                    :SectionE .



###  urn:ls#SectionA

:SectionA rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionB

:SectionB rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionC

:SectionC rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionD

:SectionD rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionE

:SectionE rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionF

:SectionF rdf:type owl:NamedIndividual ,
                   :Section .



###  urn:ls#SectionG

:SectionG rdf:type owl:NamedIndividual ,
                   :Section .





#################################################################
#
#    Rules
#
#################################################################


rdf:type  .
[ rdf:type  ;
  rdf:label "rule1" ;
   [ rdf:type  ;
                                          rdf:rest rdf:nil ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :SectionD ;
                                                       :satisfies
                                                    ]
                                        ] ;
   [ rdf:type  ;
                                          rdf:rest [ rdf:type  ;
                                                     rdf:first [ rdf:type  ;
                                                                  ;
                                                                  :SectionF ;
                                                                  :satisfies
                                                               ] ;
                                                     rdf:rest [ rdf:type  ;
                                                                rdf:rest rdf:nil ;
                                                                rdf:first [ rdf:type  ;
                                                                             ;
                                                                             :SectionG ;
                                                                             :satisfies
                                                                          ]
                                                              ]
                                                   ] ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :Person
                                                    ]
                                        ]
] .
[ rdf:type  ;
 rdf:label "rule2" ;
   [ rdf:type  ;
                                          rdf:rest [ rdf:type  ;
                                                     rdf:rest rdf:nil ;
                                                     rdf:first [ rdf:type  ;
                                                                  ;
                                                                  :SectionD ;
                                                                  :satisfies
                                                               ]
                                                   ] ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :Person
                                                    ]
                                        ] ;
   [ rdf:type  ;
                                          rdf:rest rdf:nil ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :SectionA ;
                                                       :satisfies
                                                    ]
                                        ]
] .
[ rdf:type  ;
rdf:label "rule3" ;
   [ rdf:type  ;
                                          rdf:rest rdf:nil ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :SectionA ;
                                                       :satisfies
                                                    ]
                                        ] ;
   [ rdf:type  ;
                                          rdf:rest [ rdf:type  ;
                                                     rdf:rest [ rdf:type  ;
                                                                rdf:rest rdf:nil ;
                                                                rdf:first [ rdf:type  ;
                                                                             ;
                                                                             :SectionC ;
                                                                             :satisfies
                                                                          ]
                                                              ] ;
                                                     rdf:first [ rdf:type  ;
                                                                  ;
                                                                  :SectionB ;
                                                                  :satisfies
                                                               ]
                                                   ] ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :Person
                                                    ]
                                        ]
] .
[ rdf:type  ;
rdf:label "rule4" ;
   [ rdf:type  ;
                                          rdf:rest rdf:nil ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :SectionA ;
                                                       :satisfies
                                                    ]
                                        ] ;
   [ rdf:type  ;
                                          rdf:first [ rdf:type  ;
                                                       ;
                                                       :Person
                                                    ] ;
                                          rdf:rest [ rdf:type  ;
                                                     rdf:rest rdf:nil ;
                                                     rdf:first [ rdf:type  ;
                                                                  ;
                                                                  :SectionE ;
                                                                  :satisfies
                                                               ]
                                                   ]
                                        ]
] .

###  Generated by the OWL API (version 3.2.5.1928) http://owlapi.sourceforge.net

}}}


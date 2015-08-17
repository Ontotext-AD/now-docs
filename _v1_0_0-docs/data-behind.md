---
title: Data Behind
layout: default
prev_section: high-level-architecture
next_section: extraction-pipe
category: Getting Started
permalink: v1_0_0-docs/data-behind/
---

## Dataset
In the current 2.1 release we crafted the publishing dataset using the latest versions of [DBpedia](http://wiki.dbpedia.org/) and [Wikidata](http://wikidata.org) datasets. In addition, there are links to [Geonames](http://www.geonames.org) instances and mappings to [Schema.org](http://schema.org) and [Umbel](http://umbel.org/) classes which increases the accuracy of the type detection for named entities.

#### Dataset sources *(What dataset are used?)*
We utilize the english version of DBpedia-2015-04 and corresponding Wikidata export (20150223). Mappings to Geoname and Umbel are retrieved from the DBpedia export.

#### Internal representation *(How are they merged?)*
Each source we used to produce the dataset relies on its own ontology schema tightly related with the main purpose of the dataset and its application. There isn't a strict match between the classes found in the primary sources and their count also differs. There are many errors especially in the types that come from the external sources and very often there are entities which come with more than one basic class. The majority of problems we faced are when those classe overlap (i.e Location/Organization). To simplify the things we introduced publishing ontology schema which purpose is to describe the most interesting classes speaking in terms of news and publishing. The model aims to provide a bare minimum features required by the extraction pipeline and the rest of the platform services.

There are few major classes that represent the main focus of the entity recognition and several subsidiary classes for better classification of the instances.

##### Major classes for named entities
These classes are used by the pipeline during the NER process.
 * Person
 * Location
 * Organization

##### Additional classes for named entities
Used to describe additional groups of objects and not used in the  
  * Event
  * Work
  * Animal
  * Plant

##### Subclasses
To Used to add more specific class information for particular entity. So far this information is for display purposes only. Currently there are 28 subclasses in the schema:
  * Artist (subclass of Person)
  * Athlete (subclass of Person)
  * Company (subclass of Organization)
  * Building (subclass of Location)
  * ...

##### Mappings to external sources
In order to select a preferred class for each instance in the dataset we created a mapping between the external classes and our model. This mapping is fully customizable and  

Class from publishing ontology  | Classes from external sources
------------- | -------------
Person  | http://dbpedia.org/ontology/Person http://www.wikidata.org/entity/Q5 http://umbel.org/umbel/rc/Person
Person::Athlete | http://dbpedia.org/ontology/Athlete  http://www.wikidata.org/entity/Q2066131  http://umbel.org/umbel/rc/Athlete
Person::Artist | http://dbpedia.org/ontology/Artist http://www.wikidata.org/entity/Q483501 http://umbel.org/umbel/rc/Artist
Person::Politician | http://dbpedia.org/ontology/Politician  http://www.wikidata.org/entity/Q82955  http://umbel.org/umbel/rc/Politician
... | ...

The reason we use this mapping is because we found lots of instances coming from DBpedia without clearly defined type. We try to extend that coverage by adding Wikidata and Umbel types in the stack. The mapping to the external sources is point to point so we take into account the ontology shcema of the external source. For example since we have a mapping from pub:Artist to dbp:Artist and we if we have an instance with dpb:Painter the algorithm will try to choose the most specific type from our side examining the dbp schhttp://ontology.ontotext.com/taxonomy/gender	1253202
http://ontology.ontotext.com/taxonomy/occupation	1174076
http://ontology.ontotext.com/taxonomy/dateOfBirth	1032445
http://ontology.ontotext.com/taxonomy/country	933620
http://ontology.ontotext.com/taxonomy/coordinateLocation	898982
http://ontology.ontotext.com/taxonomy/countryOfCitizenship	846828
ema.

In the cases we still don't have a valid type we try to guess it using categorization algorithms over the description. That allows us to keep in the datasourse some incomplete but important articles from DBpedia.

##### Properties
There are several common properties that all instances share and a number of specific properties which apply to different object types:
######  Common properties
  * **Type**. Represents the type of the instance (one of the types in our ontology model). In order to select this type we take into account the types that we receive from the external sources and the mappings we produced. The selection of the preferred type is automated process and can be easily
  * **Preferred label**. Represents the preferred label of an instance. This is the label displayed in the UI in the topic page for given concept.
  * **Alternative labels**. A collection of common names under which the entity appears in varios sources. For example for *United States Department of Justice* we have alternative labels *US Justice Department*, *US DOJ* and so on.
  * **Short description**. Briefly describes the main characteristics of the entity (e.g. *Italian painter*).
  * **Full Description**. Full description of the entity retrieved from DBpedia abstract.
  * **Image URI**. URI of image depicting the concept (if any).
  * **Image thumbnail URI**. URI of the thumbnail of the image depicting the concept.
  * **Exact matches**. List of URIs from the original sources (DBpedia,Wikidata,Geonames) which can be provided to the end user if requested.

###### Additional properties
There are also a number of additional properties depending of the type of the concept.  For example if the instance type is Person it may contain information of birth day, birth place, gender, etc.

#### Dataset statistics *(How many instances of P/L/O/Other do we have?)*

This is the count of the instances grouped by major types in the dataset:

- Person : 1245237
- Location: 905198
- Organization: 262030

- Thing: 446846
- Event: 86318
- Work: 549938
- Plant: 51568
- Animal: 212349

More detailed statistics showing types and subtypes can be found in the following table:

Type          | Subtype           | Count
--------------|-------------------|------
Person        |                   | 773904
Person	| Athlete |	280288
Person	| Artist |	111038
Person	| Politician | 	39569
Person	| Scientist	| 20416
Person	| Cleric	| 12349
Person	| Monarch	| 3883
Person	| Journalist	| 2840
Person	| Economist	| 950
Organization	| | 	30228
Organization	| Company	| 60301
Organization	| Band	| 39078
Organization	| EducationalInstitution	| 48842
Organization	| SportsTeam	| 28761
Organization	| Broadcaster	| 22015
Organization	| MilitaryUnit	| 13337
Organization	| PoliticalParty	| 9838
Organization	| Non-ProfitOrganization	| 4957
Organization	| SportsLeague	| 3333
Organization	| TradeUnion	| 1340
Location	| 	| 95996
Location	| PopulatedPlace	| 521137
Location	| Building	| 146626
Location	| BodyOfWater	| 51758
Location	| SportFacility	| 7643
Location	| Infrastructure	| 60419
Location	| Mountain	| 21619
Event		| | 86318
Work		| | 488163
Work	| MeanOfTransportation	| 29779
Work	| Software	| 31996
Animal		| | 212349
Plant		| | 51568
Thing		| | 446846


More than 10 million individual properties
The most common properties and counts:

Property              | Count
--------              | -----
gender                | 1253202
occupation            | 1174076
dateOfBirth           | 1032445
country	              | 933620
coordinateLocation	  | 898982
countryOfCitizenship  | 846828
locatedIn             |	686095
dateOfDeath           |	484317
placeOfBirth          |	404604
... | ...


#### How do exact matches work?
During the generation of the dataset we combined LOD instances into clusters and for each cluster an Ontotext URI is assigned. To extend the interoperability between our system and external clients and to provide an option for future upgrades of the dataset from exteranal sources we keep all LOD URIs and they can be provided upon request.

#### How are ontotext instance URIs generated and why?
Each URI identifies a cluster of object found in different dataset that we identified to represent a unique object. We generate these URIs using a modified version of Flake (A decentralized, k-ordered id generation service) which guarantee there are no duplicated identifiers. Flake produces short identifiers which can be represented using 64 bit numbers which also lowers the space required by different indexes in the system.  

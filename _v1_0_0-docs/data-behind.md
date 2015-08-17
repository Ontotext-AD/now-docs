---
title: Data Behind
layout: default
prev_section: high-level-architecture
next_section: extraction-pipe
category: Getting Started
permalink: v1_0_0-docs/data-behind/
---

## Dataset
In the current 2.1 release we crafted our dataset using the latest versions of [DBpedia](http://wiki.dbpedia.org/) and [Wikidata](http://wikidata.org) datasets. There are also mappings to [Geonames](http://www.geonames.org) entities and mappings to [Umbel](http://umbel.org/) classes.

#### Dataset sources *(What dataset are used?)*
We are using the english version of DBpedia-2015-04 and corresponding Wikidata export from the end of march 2015. Mappings to Geoname and Umbel are retrieved from the DBpedia export.

#### Internal representation *(How are they merged?)*
Working with various sources is not a trivial task since each source utilizes its own format and ontology schema. Although DBpedia is the central source around which we built the dataset we were trying to find a solution that will allow us not to be bound to any particular data provider in future. This is the reason we decided to introduce our own ontology schema which we will maintain and improve with next releases.
The model aims to provide a bare minimum of features required by the extraction pipeline and the rest of the platform services.

As a parent class for all classes we use pub:Thing. There are few major classes that represent the main focus of the entity recognition and several subsidiary classes which allow better classification of the instances.

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
Used to add more specific class information for particular entity. So far this information is for display purposes only. Currently there are 28 subclasses in the schema:
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

The reason we use this mapping is because we found lots of instances coming from DBpedia without clearly defined type. We try to extend that coverage by adding Wikidata and Umbel types in the stack. The mapping to the external sources is point to point so we take into account the ontology shcema of the external source. For example since we have a mapping from pub:Artist to dbp:Artist and we if we have an instance with dpb:Painter the algorithm will try to choose the most specific type from our side examining the dbp schema.

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
#### How do exact matches work?
#### How are ontotext instance URIs generated and why?

## Pipeline

#### How does the pipeline use the dataset?
#### What types of annotations does it output?
#### Overview of the components used (with a diagram, preferably)

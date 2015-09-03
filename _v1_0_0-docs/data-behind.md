---
title: Data Behind
layout: default
prev_section: high-level-architecture
next_section: extraction-pipe
category: Getting Started
permalink: v1_0_0-docs/data-behind/
---
In the current 2.1 release, the publishing dataset uses the latest versions of [DBpedia](http://wiki.dbpedia.org/) and [Wikidata](http://wikidata.org). In addition, there are links to [GeoNames](http://www.geonames.org) instances and mappings to [Schema.org](http://schema.org) and [Umbel](http://umbel.org/) classes, which increase the accuracy of the type detection for named entities.

## Dataset sources *(what datasets are used)*

* English version of DBpedia-2015-04 and the corresponding Wikidata export (20150223);
* Mappings to GeoNames and Umbel, retrieved from the DBpedia export.

## Internal representation *(how they are merged)*
NOW uses a custom publishing ontology schema describing the most interesting classes in terms of news and publishing. Its aim is to provide the bare minimum of features required by the extraction pipeline and the rest of the platform services.

### Challenges
As the ontology schemas of the dataset sources differ in purpose and application, their number of classes, naming and definitions of types and properties also differ. Therefore, there is no direct match between them. Many errors occur with the types coming from the external sources and the entities that have more than one basic class. The majority of problems spring from overlapping classes (i.e., when an entity is both a Location and an Organization).

### Classes
There are few major classes that represent the main focus of the entity recognition and several subsidiary classes for better classification of the instances.

#### Major classes for named entities
The following classes are used by the pipeline during entity recognition:

* Person - individuals in the dataset;
* Location - various places such as geographical regions, natural locations, public or commercial places, buildings, etc. All countries are also marked as Locations;
* Organization - profit and non-profit organizations, sports teams, military alliances, government institutions, etc.


#### Additional classes for named entities
Besides the Person/Location/Organisation classes, the dataset has some additional groups of objects:

* Event - temporary or scheduled events such as festivals, competitions, gatherings, concerts, etc.;
* Work - intellectual or artistic creations;
* Animal - multicellular eukaryotic organisms;
* Plant - multicellular eukaryotic organisms of the kingdom Plantae.

#### Subclasses
There are also several other subclasses that provide additional meaning to the named entities. So far, this information has been used only for display purposes (named entity recognition work with the base classes only). Currently, there are 28 subclasses in the schema:

* Artist (subclass of Person);
* Athlete (subclass of Person);
* Company (subclass of Organization);
* Building (subclass of Location);<br>
  (... 24 more).

#### Mappings to external sources
For each instance in the dataset a preferred class is selected by mapping the external classes to our model. This mapping is fully customizable and can be tweaked to satisfy any client requirements.

Class from publishing ontology  | Classes from external sources
------------- | -------------
<code>Person</code>  | <code>http://dbpedia.org/ontology/Person</code> <code>http://www.wikidata.org/entity/Q5</code> <code>http://umbel.org/umbel/rc/Person</code>
<code>Person::Athlete</code> | <code>http://dbpedia.org/ontology/Athlete</code>  <code>http://www.wikidata.org/entity/Q2066131</code> <code>http://umbel.org/umbel/rc/Athlete</code>
<code>Person::Artist</code> | <code>http://dbpedia.org/ontology/Artist</code> <code>http://www.wikidata.org/entity/Q483501</code> <code>http://umbel.org/umbel/rc/Artist</code>
<code>Person::Politician</code> | <code>http://dbpedia.org/ontology/Politician</code> <code>http://www.wikidata.org/entity/Q82955</code>  <code>http://umbel.org/umbel/rc/Politician</code>
... | ...

Such a mapping is necessary because of the many instances coming from DBpedia without a clearly defined type. We have extended this coverage by adding Wikidata and Umbel types in the stack. As the mapping to the external sources is point to point, the algorithm also considers their ontology schemas.
For example, in order to map <code>pub:Artist</code> to <code>dbp:Artist</code> with an instance <code>dpb:Painter</code>, the algorithm examines all currently loaded ontology relations (dbpeda, wikidata, umbel class trees) and suggests the proper class from the publishing ontology.

In cases where there is still no valid type, categorisation algorithms are used over the description to guess it. Thus, some incomplete but important articles from DBpedia are kept in the data source.

### Properties
There are several common properties that all instances share and a number of specific properties that apply to different object types.

####  Common properties
The common properties are applied to all entities in the knowledge base regardless of their class.

* **Type** - the type of the instance. To generate this type, we have taken into account the types of the external sources and our mapping. The selection of the preferred type is an automated process and can be easily adjusted by changing the mapping.
* **Preferred label** - the preferred label of an instance. This is the label displayed for a given concept in the topic page  in the UI.
* **Alternative labels** - a collection of common names under which the entity appears in various sources. For example, for *United States Department of Justice* we have the alternative labels: *US Justice Department*, *US DOJ*, etc.
* **Short description** - a brief description of the main characteristics of the entity (e.g. *an Italian painter*).
* **Full Description** - a full description of the entity retrieved from the DBpedia abstract.
* **Image URI** - the URI of image depicting the concept (if any).
* **Image thumbnail URI** - the URI of the thumbnail of the image depicting the concept.
* **Exact matches** - a list of the URIs from the original sources (DBpedia,Wikidata,Geonames) that can be provided to the end user, if requested.

#### Additional properties
There are also a number of additional properties depending of the type of the concept. For example, if the instance type is Person, it may contain information about date of birth, birth place, gender, etc.

* http://ontology.ontotext.com/taxonomy/gender	1253202
* http://ontology.ontotext.com/taxonomy/occupation	1174076
* http://ontology.ontotext.com/taxonomy/dateOfBirth	1032445
* http://ontology.ontotext.com/taxonomy/country	933620
* http://ontology.ontotext.com/taxonomy/coordinateLocation	898982
* http://ontology.ontotext.com/taxonomy/countryOfCitizenship	846828

There are more than 10 million individual properties coming from more than fifty types that we have collected. The following is a list of the most common properties and counts:

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

Currently, these properties can be found in the KB Explorer component.

## Dataset statistics *(how many instances of P/L/O/Other we have)*

This is the count of the instances grouped by major types in the dataset:

* Person : 1245237
* Location: 905198
* Organization: 262030

* Thing (unspecified entity): 446846
* Event: 86318
* Work: 549938
* Plant: 51568
* Animal: 212349

The following table provides more detailed statistics, including types and subtypes:

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

## How exact matches work
During the generation of the dataset, we combined different LOD instances into clusters and an Ontotext URI was assigned for each cluster. To extend the interoperability between our system and external clients as well as to provide an option for future upgrades of the dataset from external sources, we have kept all LOD URIs and they can be provided upon request.

## How Ontotext instance URIs are generated and why
Each Ontotext URI identifies a cluster of external datasets URIs representing the same unique object. These URIs were generated by using a modified version of Flake (a decentralized, k-ordered ID generation service), which guarantees that there would be no duplicated identifiers. Flake produces short identifiers that can be represented internally using 64 bit numbers, which also lowers the space requirements of the various components in the system.

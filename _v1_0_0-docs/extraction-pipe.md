---
title: Extraction Pipeline
layout: default
prev_section: data-behind
next_section: brief-ux
category: Getting Started
permalink: v1_0_0-docs/extraction-pipe/
---
## Overview

The extraction pipeline used in [NOW](http://now.ontotext.com) shows the text analytics that takes place behind the scene of the [Ontotext Dynamic Semantic Publishing platform](http://ontotext.com/semantic-solutions/dynamic-semantic-publishing-platform/). It enriches the content aggregated from various news sources based on data from [DBpedia](wiki.dbpedia.org/), [WikiData](http://wikidata.org/), [GeoNames](http://www.geonames.org/) and others, and a wide variety of linguistic and algorithmic resources -- such as semantic gazetteers, rules triggered by particular linguistic patterns, various statistical models for classification and sequence tagging trained against human-annotated corpora, etc.. The extraction pipe recognises mentions of entities such as Person, Organisation, Location, keyphrases, and relationships between them, as well as their relevance and confidence to the text.

After the initial preprocessing phase (content cleanup, tokenization, sentence-splitting, morphological analysis), the pipeline performs annotation via lexicons and rules in order to extract generic concepts (numbers, measures and metrics), keyphrases (noun phrases relevant to the main topic of a document), named entity discovery and linking (matching the contents of the knowledge base against the document content and resolving any ambiguity that may occur), novel entity recognition (the discovery and handling of named entities previously unavailable in the knowledge base), and, finally, extracting relationships that may exist between the discovered named entities. Furthermore, the pipeline assesses the degree of importance of the concepts in the context of the article where they were discovered, as well as the sentiment of their immediate context.

A high-level description of the phases (sub-pipelines) involved in the concept extraction pipeline

## Preprocessing phase
During this phase, a very basic pre-processing takes place:

- content clean-up rules (normalization of quotation marks, apostrophes, etc., provision of sentence splits at paragraph boundaries, etc.)
- tokenization (ANNIE English Tokenizer PR)
- sentence splitting (ANNIE Sentence Splitter PR)
- stemming (Snowball Stemmer PR)
- POS-tagging (OpenNLP English POS Tagger PR)
- chunking (OpenNLP English Chunker PR)
- lemmatization (Gate Morpholocial Analyser PR)

Most of the processing resources used during this phase are part of the GATE distribution. Several additional rules that improve the output and facilitate the subsequent tasks are also provided (e.g. rules that insert additional splits on newline characters and document elements available through the “Original markups” annotation set; rules that modify noun phrase chunks in order to improve the extraction of keyphrase candidates; rules that generate canonical forms for such noun phrases).

## Keyphrase extraction phase

This phase contains logic that generates keyphrase candidates, assigns relevance scores to the candidates, and classifies them into positive or negative instances via a heuristic ranking scheme that uses .... WHAT?

## Gazetteer-based enrichment phase

At this stage, the document content is enriched by means of a semantic gazetteer. This component annotates the character sequences that resemble mentions of concepts available in the knowledge base. The gazetteer lookups are not part of the extraction results per se, but they are used as a means of spotting "candidates" that facilitate the statistical models that produce the final set of entities.

All sub-pipelines are responsible for the execution of a single gazetteer (ANNIE Gazetteer, LD Gazetteer), and the consequent transfer of features from the gazetteer-generated annotations to other annotation types involved in the named entity recognition and disambiguation phases.

The “LD Gazetteer” component's cache is populated with instances from the following sources: [DBpedia](wiki.dbpedia.org/) and [WikiData](http://wikidata.org/). In addition, there are links to [GeoNames](http://www.geonames.org/) instances and mappings to [Schema.org](http://schema.org) and [Umbel](http://www.umbel.org/) classes, which increase the accuracy of the type detection for named entities.

## Named entity recognition and disambiguation phase

### Named entity disambiguation

Using the named entity candidates discovered by the LD Gazetteer, and given the specific article context, this phase makes use of a specialized classifier to assign a "positive" or "negative" label to each candidate. As a result, the ambiguity associated with the complete set of gazetteer lookups is eliminated – at most one named entity remains per document offset, and the redundant ("negative") named entity candidates are filtered.

The disambiguation mechanism relies on some additional metadata derived from Wikipedia:

- a short textual description of each candidate (based on DBpedia and Freebase abstracts);
- a set of URIs representing the entities that appear in the full DBpedia article for each candidate.

Various similarity scores are computed by a specialized processing resource that accesses the metadata (stored in indices prepared especially for this task) and evaluates the correspondence between the candidate and the context (the article content and the content stored in the aforementioned indices). The final classification is conducted by a separate processing resource, based on these pre-computed scores and some additional features derived via rules from the local context.

Currently, the component supports disambiguation of named entities belonging to either of the following classes:

#### Major classes for named entities
The following classes are used by the pipeline during entity recognition:

* Person - individuals in the dataset;
* Location - various places such as geographical regions, natural locations, public or commercial places, buildings, etc. All countries are also marked as Location;
* Organization - profit and non-profit organizations, sports teams, military alliances, government institutions;

#### Additional classes for named entities
Besides the Person/Location/Organisation classes, the dataset has some additional groups of objects:

* Event - temporary or scheduled events such as festivals, competitions, gatherings, concerts, etc.;
* Work - intellectual or artistic creation;
* Animal - multicellular eukaryotic organisms;
* Plant - multicellular eukaryotic organisms of the kingdom Plantae;

#### Subclasses
There are also several other subclasses that provide additional meaning to the named entities. So far, this information has been used only for display purposes (named entity recognition work with the base classes only). Currently, there are 28 subclasses in the schema:

* Artist (subclass of Person)
* Athlete (subclass of Person)
* Company (subclass of Organization)
* Building (subclass of Location)
  (... 24 more)

### Discovery of novel named entities

Named entities not available in the “LD Gazetteer” component's cache are not recognized, and therefore not handled by the above-described disambiguation mechanism. The recognition of novel entities belonging to the “Person”, “Location” and “Organization” classes is handled by the PLO Tagger processing resource, which compensates for the lack of perfect coverage by the classifier-based tagging approach.

The results extracted during phases 4.1 and 4.2 are combined in a way that eliminates the overlapping among annotations produced by the disambiguation classifier and the PLO tagger components. The implemented logic guarantees that the disambiguated entities having a meaningful URI are preferred to the anonymous entities discovered by the PLO tagger whenever possible.

## Generic entity extraction phase

This phase implements a rule-based enrichment with entities of generic type. Currently, these include:

- dates (normalization logic is provided as well)
- numbers
- money
- percentages
- measurements

## Result consolidation phase

This phase contains rules that take into account all entity types discovered during the preceding phases in order to refine the extraction results. At its end, instance URIs are generated and assigned to entities that have no such identifiers.

This phase involves the execution of the “Orthomatcher” processing resource, which deals with the discovery of orthographical variations of the labels and aliases of people, location and organization entities. Subsequently, the trusted URIs of disambiguated entities are propagated to novel aliases annotated by the PLO tagger, based on linkage done by the “Orthomatcher” component. At the end of the phase, URIs are generated for the entities that have not been assigned a valid URI during the above-described phases.

## Relation extraction phase

This phase conducts rule-based extraction of various relationships between the atomic entities discovered at the preceding stages. Currently, the following types of relations are supported:

* RelationAcquisition
* RelationOrganizationAbbreviation
* RelationOrganizationAffiliatedWithOrganization / RelationSubOrganization
* RelationOrganizationHasCompetitor
* RelationOrganizationHasCustomer
* RelationOrganizationLocation
* RelationOrganizationQuotation
* RelationPersonHasRoleInLocation
* RelationPersonHasRoleInOrganization
* RelationPersonHasRoleWithinOrganizationInLocation
* RelationPersonQuotation
* RelationPersonRole

## Clean-up phase

During this phase, a final clean-up takes place, through which redundant intermediate annotations are removed, the document readability is improved, and the annotation sets are reorganized in order to assume the structure expected by the components that process the documents after the completion of the concept extraction pipeline.

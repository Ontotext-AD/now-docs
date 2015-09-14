---
title: Extraction Pipeline
layout: default
prev_section: data-behind
next_section: brief-ux
category: Getting Started
permalink: v1_0_0-docs/extraction-pipe/
---
## Overview






The extraction pipeline used in [NOW](http://now.ontotext.com) shows the text analytics that takes place behind the scene of the [Ontotext Dynamic Semantic Publishing platform](http://ontotext.com/semantic-solutions/dynamic-semantic-publishing-platform/). It enriches the content aggregated from various news sources based on data from [DBpedia](wiki.dbpedia.org/), [WikiData](http://wikidata.org/), [GeoNames](http://www.geonames.org/) and others. The pipeline utilises  a wide variety of linguistic and algorithmic resources such as semantic gazetteers, rules triggered by particular linguistic patterns, various statistical models for classification and sequence tagging trained against human-annotated corpora, etc. These resources are chained together in a sequence (hence the name pipeline) that provides content enrichment of gradually increasing complexity, where each phase builds upon the results produced by the one that precedes it. The extraction pipeline recognises mentions of entities such as Person,  Organization, and Location, and links them, if possible, to the structured knowledge behind. It also tags the relevant nounphrases, called keyphrases, thus allowing a fast grasp into the topic of the document. Furthermore, it detects  relationships between the extracted entities, as well as their relevance and confidence to the text.


**Sketch of the pipeline:**


- After the initial preprocessing phase (content cleanup, tokenization, sentence-splitting, morphological analysis), the pipeline performs annotation via lexicons and rules in order to extract some generic concepts like numbers, measures and metrics.

- In a further step the **keyphrases** are extracted. These are noun phrases that are particularly relevant to the document and as such tend to describe its topic in a concise form.

- Similarly, the **named entities (NE)** mentioned in the document also provide valuable information on its subject. They are extracted during the NE discovery and linking phase of the pipeline, where mentions of concepts from the knowledge base are recognised in the document by using a semantic gazetteer and a machine-learning word sense disambiguation algorithm.

- Since not all NE in the document are present in the knowledge base, we also perform **novel named entity recognition**.

- In a final step, the pipeline extracts **relationships** between the discovered named entities.

- For all extracted keyphrases and NE, the pipeline assesses the degree of importance (**relevance score**) for the article where they were discovered, as well as the sentiment of their immediate context.

<img src="{{ site.baseurl }}/img/Tagasauris_pipeline.png" alt="Pipeline" style="width:400px;height:800px; margin: 0 auto">

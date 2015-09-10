---
title: Content Enrichment
layout: default
prev_section:
next_section:
category: Features
permalink: v1_0_0-docs/content-enrichment/
---
On top of presenting the latest news by category, NOW offers a broad and in-depth perspective on each story. The coloured lines in the text show concepts, keyphrases and relationships forming the article's unique semantic fingerprint.

<img src="{{ site.baseurl }}/img/OverviewArticle.png" alt="NOW Content Enrichment" style="width:900px;height:500px; margin: 0 auto">

The following entities are tagged:

**Trusted Named Entities** - Entities such as Persons, Locations, Organizations, etc. that are linked to the knowledge behind.

<img src="{{ site.baseurl }}/img/trustedNEv.png" alt="NOW Trusted Named Entities" style="width:400px;height:200px; margin: 0 auto">


Additional background information  from the knowledge base  as well as timelines and related stories can be retrieved upon clicking on them.

<img src="{{ site.baseurl }}/img/trustedNE1.png" alt="NOW Content Enrichment" style="width:900px;height:500px; margin: 0 auto">

**Generated Named Entities** - We also capture mentions of Named Entities that  are not present in the knowledge base. They are tagged as Generated Named Entities.


<img src="{{ site.baseurl }}/img/generatedNEv.png" alt="NOW Generated Named Entities" style="width:400px;height:200px; margin: 0 auto">

**Keyphrases** -  (noun-)phrases that are particularly relevant to the topic of the document. A short glance at the tagged keyphrases should reveal what this particular piece of news is about. Similarly to the named entities, the keyphrases can be trusted and generated, depending upon whether they can be linked to an object in the knowledge base.

<img src="{{ site.baseurl }}/img/keyphraseV.png" alt="NOW Keyphrases" style="width:400px;height:200px; margin: 0 auto">  

**Relations** between the involved named entities are tagged as well.  

<img src="{{ site.baseurl }}/img/relNEv.png" alt="NOW Relations" style="width:400px;height:120px; margin: 0 auto">

All tags also contain information on the **relevance** and the **confidence** of the particular tagged entity. The relevance score is a measure on how relevant is the particular entity to the main topic of the article. Per definitions, keyphrases are the phrases with the highest relevance score. The process of tagging the above mentioned types of entities involves a wide variety of linguistic and algorithmic resources and the confidence score is a measure of how confident are the algorithms in adding the particular tag.  

All in all, the tagged entities, together with the additional information from the knowledge base, allow the reader to rapidly grasp the main topic of the article and in the same time to obtain background information on the involved people, places, organisations, quotations and the relationships between them as well as articles with a similar semantic fingerprint.

<img src="{{ site.baseurl }}/img/SemanticFingerprint1.png" alt="NOW Semantic Fingerprint" style="width:300px;height:500px; margin: 0 auto">

As a result, NOW introduces a profound reading experience, which can be used for different kinds of analysis, forecasting, etc.

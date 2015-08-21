---
title: Content Enrichment
layout: default
prev_section:
next_section:
category: Features
permalink: v1_0_0-docs/content-enrichment/
---

The idea is to explain what types of information is extracted, relevance & confidence scores, what's the motivation behind, who can take an advantage from it and why.

On top of presenting the latest news by category, NOW offers a broad and in-depth perspective on each story. The coloured lines in the text show concepts, keyphrases and relationships forming the article's unique semantic fingerprint.

<img src="{{ site.baseurl }}/img/OverviewArticle.png" alt="NOW Content Enrichment" style="width:650px;height:300px; margin: 0 auto">

The following entities are tagged:

**Trusted Named Entities** - These are mentions in the text of Persons, Locations and Organizations from the Knowledge Base. 

<img src="{{ site.baseurl }}/img/trustedNEv.png" alt="NOW Trusted Named Entities" style="width:300px;height:200px; margin: 0 auto">


Additional background information  from the Knowledge Base  as well as timelines and related stories can be retrieved upon clicking on the entity. 

<img src="{{ site.baseurl }}/img/trustedNE1.png" alt="NOW Content Enrichment" style="width:650px;height:300px; margin: 0 auto">

**Generated Named Entities** - We also capture mentions of Named Entities that  are not present in the knowledge base. They are tagged as Generated Named Entities.


<img src="{{ site.baseurl }}/img/generatedNEv.png" alt="NOW Generated Named Entities" style="width:300px;height:200px; margin: 0 auto">

**keyphrases** - Keyphrases are (noun-)phrases which are particularly relevant to the topic of the document. A short grasp on the tagged  keyphrases should reveal what is the particular piece of news about. Similarly as the named entities, the keyphrases can be trusted and generated, depending upon if they can be linked to an object in the knowledge base.

<img src="{{ site.baseurl }}/img/keyphraseV.png" alt="NOW Keyphrases" style="width:300px;height:200px; margin: 0 auto">  

**relations** - relationships between the involved named entities are tagged as well.  

<img src="{{ site.baseurl }}/img/relNEv.png" alt="NOW Relations" style="width:300px;height:200px; margin: 0 auto"> 
 
All tags also contain information on the **relevance**  and the **confidence** of the particular tagged entity. The relevance score is a measure on how relevant is the particular entity to the main topic of the article. Per definitions keyphrases are the phrases with the highest relevance score. 
The process of tagging the above mentioned types of entities involves a wide variety of linguistic and algorithmic resources and the confidence score is a measure of how confident are the algorithms in putting the particular tag.  


Put it all together,  the tagged entities, together with the additional information from the Knowledge Base, allows the reader to rapidly grasp the main topic of the article and in the same time obtain background information on the involved people, places, organisations, quotations and the relationships between them. 

Readers can also see at a glance what the article is about, what other people, places and organisations are mentioned in it as well as articles with a similar semantic fingerprint.

<img src="{{ site.baseurl }}/img/SemanticFingerprint1.png" alt="NOW Semantic Fingerprint" style="width:350px;height:600px; margin: 0 auto">

As a result, NOW introduces a profound reading experience, which can be used for different kinds of analysis, forecasting, etc.

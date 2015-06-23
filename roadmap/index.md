---
title: Roadmap
layout: default
---
## Foreword

In an effort to be transparent with our roadmap, we are publishing in advance the important changes that are in progress. As we are a small team and not all dependencies are in our control, release dates may change in some circumstances but we will do our best to communicate them as soon as possible. This roadmap intends to show future changes that may affect existing applications and also includes the new features we are currently working on.

## Upcoming changes

### June and July 2015

#### New dataset

We have not been particularly happy with our current blend of [DBPedia 3.9](http://wiki.dbpedia.org/services-resources/datasets/data-set-39) and [Freebase](https://www.freebase.com/), so we are preparing a mesh of [WikiData](https://www.wikidata.org/wiki/Wikidata:Main_Page) (which is really cool) and [DBPedia 2014](http://wiki.dbpedia.org/Downloads). Our main issues are with data correctness and completeness and the tests we have done so far with this new dataset mesh look very promising. Although rather difficult, it is an essential job for us to do as all our concept extraction, search and recommendation capabilities ultimately depend on the dataset.

#### New concept extraction pipeline

We are dramatically improving our extraction capabilities and the majority of the silly errors that can currently be seen will disappear. This is the other major feature along with topic pages and the new dataset. The main challenge here is actually the size of the different resources in the pipeline such as dictionaries, metadata indexes, and more. They have grown rather big and started breaking our software development practices as well as pushing the limits of the tools we use for deployment and distribution. So, we need to re-invent these along the way, too.

#### UI design improvements

The current UI design will be changed to a flat one in order to improve its look and feel, and open more space for showing some additional capabilities, powered by our services.

#### Topic pages

We know that publishers would love to be able to see generated pages about particular concepts, or topics. Right now, we are working on automatically aggregating pages for People, Locations and Organisations. The information is compiled from the data extracted from the articles and our knowledge base.

In other words, on a page about Yanis Varoufakis, we will be able to show his occupation, nationality, date and place of birth as well as what he said or wrote in the news, what other concepts he is usually mentioned with (i.e. Angela Merkel, ECB), etc.

#### Channel view

For each channel, we want to have visuals of the trending concepts in the news at the moment as well as for the past week and month. We believe it is a useful way to see what's being hot in business, sport, science and so on.

#### Document view

We believe it is important to show the main concepts of an article (most relevant concepts) and what the other mentions are (less relevant ones). We will also provide a trend estimation chart based on the presence of the most relevant concepts in the news in the last few days, weeks, or months.

Another useful feature will be color-coded annotations with on/off control.  

<img src="{{ site.baseurl }}/img/Annotations_ON_OFF.png" alt="Annotations ON/OFF" style="width:400px;height:150px; margin: 0 auto">

To get a better idea, try out our [Tagging Service](http://tag.ontotext.com).


#### Autosuggest ranking

Currently, the typeahead suggestions in the search bar are not ranked. This should be easy to fix, as we have a handy ranking plug-in for GraphDB.

#### Ability to sort search results

A new feature for sorting search results by date and relevance will be implemented to give end users more control over the expected results.

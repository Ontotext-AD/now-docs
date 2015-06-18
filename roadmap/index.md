---
title: Roadmap
layout: default
---
## Foreword

In an effort to be transparent with our roadmap, we publish in advance the important changes we are working on. We will try to stick to our release deadlines, but usually it is much easier to commit to month or quarter estimates for some of the more difficult ones. Since we are a small team and not all dependencies are in our control, release dates can change and we will give our best to communicate updates as soon as possible. This roadmap intends to show future changes that may affect existing applications and also includes new features we are working on.

## Upcoming changes

### June and July 2015


#### UI design improvements

We feel a flat design would look and feel better, and would also grant us more space where we can show additional information, powered by our services.

#### Document view

We believe it's more important to show what the article is about (most relevant concepts) and what are the other mentions (less relevant). We also want to provide
a chart showing how the most relevant concepts have been trending in the news in the last few days, week and month.

Another useful feature we want to include is the annotation on/off control which also provides a color legend. To get an idea, see the following image or try
our [Tagging Service](http://tag.ontotext.com) which already has it.

<img src="{{ site.baseurl }}/img/Annotations_ON_OFF.png" alt="Annotations ON/OFF" style="width:600px;height:270px">


#### Topic pages

The ability to generate pages about particular concepts, or topics is something publishers would love to have and we know that. We are working on automatically generated
pages for People, Locations and Organisations, which are going to aggregate both information present in our knowledge base and information we have extracted from articles.
For example, on a page about Yanis Varoufakis, we will be able to show not only basic properties such as occupation, nationality, date and place of birth, but also
his quotes we have extracted from the news, what other concepts he is usually mentioned (i.e. Angela Merkel, ECB). This is the most exciting single feature we
are preparing, and it's also the most complex.

#### Channel view

For each channel we want to have visuals of the trending concepts in the news now, in the past week and in the past month. We believe it is a useful way to see
what's being hot in business, sport, science and so on.


#### Autosuggest ranking

We don't actually rank results when providing type ahead suggestions in the search bar. This is something we should be able to easily fix, as we have a handy ranking plug-in for
GraphDB.

#### Ability to sort search results

By date and relevance. At the moment we don't really give choice, but do what we've decided to do. Providing more control to end users is something we are after.

#### New dataset

We're not particularly happy with our current blend of [DBPedia 3.9](http://wiki.dbpedia.org/services-resources/datasets/data-set-39) and [Freebase](https://www.freebase.com/), so we're preparing a mesh of [WikiData](https://www.wikidata.org/wiki/Wikidata:Main_Page) (which is really cool)
and [DBPedia 2014](http://wiki.dbpedia.org/Downloads). Our main issues are with data correctness and completeness and the tests we've done with this new dataset
mesh look very promising. Still a tough job to do, but an essential one to pull off, because all our concept extraction, search and recommendation capabilities ultimately
depend on the dataset.

#### New concept extraction pipeline

As concept extraction relies on the dataset in use, we've managed to dramatically improve our extraction capabilities. The majority of those stupid errors which you can see now
 will go away (to be replaced by others in order to restore the balance in the universe). This is the other major feature along with topic pages and the dataset. The main challenge there
 is actually the size of the different resources in the pipeline, such as dictionaries, metadata indexes and more. They've grown big and are breaking our software development practices,
 they are pushing the limits of the tools we use for deployment and distribution, so we need to re-invent these along the way too.



---
title: Roadmap
layout: default
---
## Foreword

In an effort to be transparent with our roadmap, we are publishing in advance the important changes that are in progress. We will try to stick to our release deadlines but usually, for some of the more difficult ones, it is much easier to commit to monthly or quarterly estimates. Since we are a small team and not all dependencies are in our control, release dates can change and we will do our best to communicate this as soon as possible. This roadmap intends to show future changes that may affect existing applications and also includes new features we are currently working on.

## Upcoming changes

### June and July 2015


#### UI design improvements

We think a flat design would look and feel better, and would also give more space where we can show additional information, powered by our services.

#### Document view

We believe it is more important to show what the article is about (most relevant concepts) and what the other mentions are (less relevant ones). We also want to provide a chart showing what trends the most relevant concepts have been exhibiting in the news in the last few days, weeks, or months.

Another useful feature we want to include is annotation on/off control with corresponding colour-coding. To get an idea, see the following image or try
our [Tagging Service](http://tag.ontotext.com).

<img src="{{ site.baseurl }}/img/Annotations_ON_OFF.png" alt="Annotations ON/OFF" style="width:600px;height:270px">


#### Topic pages

The ability to generate pages about particular concepts, or topics, is something publishers would love to have and we know that. Right now, we are working on automatically generated
pages for People, Locations and Organisations, which are going to aggregate information available in our knowledge base as well as information we have extracted from articles.

For example, on a page about Yanis Varoufakis, we will be able to show not only basic properties such as occupation, nationality, date and place of birth but also quotes by him that we have extracted from the news, what other concepts he is usually mentioned together with (i.e. Angela Merkel, ECB), etc. This is the single? most exciting feature we are preparing as well as the most complex one.

#### Channel view

For each channel, we want to have visuals of the trending concepts in the news, now as well as the past week and month. We believe it is a useful way to see
what's being hot in business, sport, science and so on.


#### Autosuggest ranking

When we provide type ahead suggestions in the search bar, we don't actually rank results. This is something we should be able to easily fix, as we have a handy ranking plug-in for GraphDB.

#### Ability to sort search results

By date and relevance. At the moment, we don't really give a choice, but do what we've decided to do. Providing more control to end users is something we are after.

#### New dataset

We have not been particularly happy with our current blend of [DBPedia 3.9](http://wiki.dbpedia.org/services-resources/datasets/data-set-39) and [Freebase](https://www.freebase.com/), so we are preparing a mesh of [WikiData](https://www.wikidata.org/wiki/Wikidata:Main_Page) (which is really cool)
and [DBPedia 2014](http://wiki.dbpedia.org/Downloads). Our main issues are with data correctness and completeness and the tests we have done so far with this new dataset
mesh look very promising. Although rather difficult, it is an essential job for us to do as all our concept extraction, search and recommendation capabilities ultimately
depend on the dataset.

#### New concept extraction pipeline

We have also managed to dramatically improve our extraction capabilities and the majority of the silly errors that you can currently see
will go away (no doubt, to be replaced by others in order to restore the balance in the universe). This is the other major feature along with topic pages and the new dataset. The main challenge there is actually the size of the different resources in the pipeline such as dictionaries, metadata indexes and more. They have grown rather big and started breaking our software development practices as well as pushing the limits of the tools we use for deployment and distribution. So, we need to re-invent these along the way, too.

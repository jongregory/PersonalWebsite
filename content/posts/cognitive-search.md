---
title: "Cognitive Search"
date: 2018-09-09T13:54:45Z
draft: true
tags: ["ai","azure","cognitive search","cognitive services"]
---

**Overview**

Azure Cognitive Search is a feature of Azure Search (In preview at the time of writing) which allows search indexes to be built for traditionally non-searchable content.

Using the azure cognitive services to provide Natural Language Processing and Image Processing search can be enabled for  entity recognition, language detection, key phrase extraction, text manipulation, and sentiment detection,  facial detection, image interpretation, image recognition (famous people and landmarks) or attributes like colors or image orientation.


The majority of websites can use Azure search so are also compatible with Azure Cognitive Search, this means that websites  could offer search across all the media a company owns, could search for 'positive' comments or videos containing a named presenter.

Because the search index can integrate into cognitive services search can be far more open, so where search on websites has been traditionally keyword based it can now be question based if Azure Cognitive search is combined with LUIS. For Example "I would like to find products that are blue"

**Concepts**

Cognitive Search works as a pipeline using the azure search indexers, the key difference is skills are attached to perform cognitive services on the data, the output is a JSON based Azure Search Index that can be used like any azure search index. The documentation has links to key features.

*1 - Document Cracking*

Document Cracking is the start of the pipeline where unstructured text, image files etc are read and loaded by and indexer - the supported formats are here.

*2 - Cognitive Skills and Enrichment*

Cognitive Skills is the section of the pipeline where the magic happens and sets Cognitive Search beyond normal azure search, this is achieved by using built in cognitive skills or defining custom skills. The output from the custom skills enriches the search indexes. 

*3 - Search Index & Query Based Access*

Querying the search index the output from the pipeline can now work like any other azure search index and the cognitive insights are built into the website.

**Resources**

[https://docs.microsoft.com/en-us/azure/search/cognitive-search-tutorial-blob](https://docs.microsoft.com/en-us/azure/search/cognitive-search-tutorial-blob)

[https://github.com/Azure/LearnAI-Cognitive-Search](https://github.com/Azure/LearnAI-Cognitive-Search)

[https://docs.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset](https://docs.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset)
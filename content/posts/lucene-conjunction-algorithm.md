---
title: How Lucene performs searches over word conjunctions
date: 2022-05-08
tags: [algorithms, lucene]
---

[Apache Lucene][2] is an open source search software used by many tech giants, including Twitter and LinkedIn to power their sites' search features. It offers the ability to search for multiple words across multiple documents, otherwise known as a conjunction. How is Lucene able to quickly<!--QC1--> perform these conjunctions?

This is where the leapfrog algorithm comes in<!--QC2-->. The leapfrog algorithm is used to find word conjunctions across several documents. Before we dive into how this algorithm works, we should explain a few things first:

* **Lucene's inverted index** - Lucene makes use of an inverted index, which is a map of all the words and a list of the document IDs they reside in (we'll call this list a **posting list**). We will refer to a posting list for a given word, `x`, as `p_x` from now on.

* **The `next` function** - the `next` function acts on a list of document IDs, `next(p_x)`, and returns the value of the next index in that list. If the current index is undefined, then `next(p_x)` will return the first element in that list.

* **The `advance` function** - the `advance` function is a general function that acts on any list and, given a value that matches the type within the list, will either return the first value that is greater than or equal to the provided value. In the context of a list of document IDs, given a list `p_foo = [1, 12, 17, 25]`, if `advance(p_foo, 12)` is executed, then `12` will be returned since `12` exists in the list - this will be referred to as a **match**; but if `advance(p_foo, 13)` is executed, then `17` will be returned, since the first value found greater than `13`.

> ⚠️ **NOTE**: These functions are not necessarily representative of how they exist in code, but should give a rough idea of how they are implemented and are modified to make the explanation of this algorithm simpler.

Given this information, we can now explain how the leapfrog algorithm works<!--QC3-->:

1. For each word in the conjunction, retrieve its posting list
2. Sort all posting lists in ascending order of length
3. Store the next element of the first posting list: `curr_doc_id = next(p_1)`
4. For each posting list after `p_1`, run `advance(p_x, doc_id)`
5. Advance to the next posting list if a match is found - append the doc ID to a `hits` list if `advance(p_x, doc_id)` returns a match for all posting lists. Repeat from step 3.
6. If a match is not found, set `curr_doc_id` to `advance(p_1, last_doc_id)`, where `last_doc_id` is the doc ID returned by the last execution of `advance`.
7. Return the list of `hits` once all elements in `p_1` have been exhausted.

To learn more about Lucene's data structures and algorithms, you can watch the [full talk given by Adrien Grand][1].

<!-- References -->
[1]: <https://2017.berlinbuzzwords.de/15/session/algorithms-and-data-structures-power-lucene-and-elasticsearch.html> (Algorithms and data-structures that power Lucene and Elasticsearch)
[2]: <https://lucene.apache.org/> (Apache Lucene)

<!-- Questions and comments - refer to IDs with QC prefix

1. Are there any benchmarks or examples for how quickly Lucene is able to find conjunctions across documents?
2. Is the leapfrog algorithm invented by the Lucene team, or is it a common algorithm? See if we can find any other references of it.
3. Improve with illustration - see if we can make use of [Hugo diagrams](https://gohugo.io/content-management/diagrams/)
-->
WordNet in JSON Format
======================

The [WordNet](http://wordnet.princeton.edu) dataset is provided in a format that requires dedicated parsing routines. [JSON](https://en.wikipedia.org/wiki/JSON#Example) is a universal data format, that is supported across various programming languages.

**Using JSON, anyone can import and use WordNet dataset with ease.**

Version
-------

This dataset was built from version 3.1 of the [WordNet data files](https://wordnet.princeton.edu/download/current-version).

Citation
--------

This dataset is based on: Princeton University "About WordNet." WordNet.
Princeton University. 2010. http://wordnet.princeton.edu

Please cite them if you use this dataset.

Download
--------

See [releases](https://github.com/fluhus/wordnet-to-json/releases).

File Structure
--------------

#### WordNet (root object)

An entire WordNet database.

Fields:

* **synset** (map to [Synset](#synset)) from synset ID to synset object.
* **lemma** (map to string array) from pos.lemma to synset IDs that contain it.
* **lemmaRanked** (map to string array) like Lemma but synsets are ordered from the
  most frequently used to the least. Only a subset of the synsets are ranked, so
  LemmaRanked has less synsets.
* **exception** (map to string array) from exceptional word to its forms.
* **example** (map to string) from example ID to sentence template.

#### Synset

A set of synonymous words.

Fields:

* **offset** (int) synset offset in the raw data file, also used as an identifier.
* **pos** (string) part of speech:
  * a: adjective
  * n: noun
  * r: adverb
  * s: satellite
  * v: verb
* **word** (string array) words in this synset.
* **pointer** ([Pointer](#pointer) array) pointers to other synsets.
* **frame** ([Frame](#frame) array) sentence frames for verbs.
* **gloss** (string) lexical definition.
* **example** ([Example](#example) array) usage examples for words in this synset. Verbs only.

#### Pointer

Denotes a semantic relation between one synset/word to another.

Fields:

* **symbol** (string) relation between the 2 words. Target is \<symbol\> to source. See their meanings
  [here](https://godoc.org/github.com/fluhus/gostuff/nlp/wordnet#pkg-constants).
* **synset** (string) target synset ID.
* **source** (int) index of word in source synset, -1 for entire synset.
* **target** (int) index of word in target synset, -1 for entire synset.

#### Frame

Links a synset word to a generic phrase that illustrates how to use it. Applies to verbs only.

Fields:

* **wordNumber** (int) index of word in the containing synset, -1 for entire synset.
* **frameNumber** (int) frame number on the WordNet site.

#### Example

Links a synset word to an example sentence. Applies to verbs only.

Fields:

* **wordNumber** (int) index of word in the containing synset, -1 for entire synset.
* **templateNumber** (int) tumber of template in the [WordNet](#wordnet).Example field.

Go API
------

If you are working with Go, I encourage you to skip this JSON file and work
directly with the [Go API](https://godoc.org/github.com/fluhus/gostuff/nlp/wordnet).
This JSON dump is simply a marshaled
[WordNet](https://godoc.org/github.com/fluhus/gostuff/nlp/wordnet#WordNet)
struct.

Having Trouble?
---------------

If you have any issues, questions, or comments - feel free to share them on the
[issues](https://github.com/fluhus/wordnet-to-json/issues) section.

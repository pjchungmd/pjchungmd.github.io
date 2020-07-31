---
layout: post
title: Extracting Symptom Data from Text
subtitle: How can we ensure that models are reproducible?
#cover-img: /assets/img/path.jpg
#thumbnail-img: /assets/img/thumb.png
#share-img: /assets/img/path.jpg
tags: [Feinstein, NLP]
---

Extracting symptom data from text presents multiple challenges. The first is 
identifying which conceptual entities, which may span multiple words, should be 
labeled as a symptom, as opposed to physical exam findings, or other objective
findings. However, prior to this, other considerations include dealing with
very messy free text data that can contain (1) misspelled words, 
(2) abbreviations (which may or may not be standard), (3) non-standard language
to describe symptoms.

As part of the pipeline, the text must undergo a series of transformations,
most of which result in changes to the original text such that the it cannot be
re-constructed from the new text. Also the transformation operators themselves
can be subject to changes as their dependencies change over time.

This leads to the problem of **reproducibility**. Perhaps a reason why being 
able to reproduce results has lagged behind other aspects of machine learning 
is that just being able to get things to work well for yourself is difficult
enough, let alone getting it to work for *someone else*.

To tackle this problem in the context of the project to extract symptoms data,
let's consider how we might deal with transformed data and the transformation
operations (which can include human programmed functions or models trained from
data). Because we are using machine learning techniques, there are three items
to consider: (1) data, (2) code, and (3) artifacts. While there are mature
tools availble to version control code (e.g. Git), the process by which data
and artifacts can and should be versioned is less straightforward.

Let's consider what happens when we version control code using a tool like Git.
Once a change has been staged, it is then commited. The commit process involves
the programmer providing a useful comment stating what the commit was for. In
the background, Git keeps track of the diffs between each version of the code
and the comments provide some background information (although of varying 
quality) as to what the change is about. Furthermore each version of the code
is immutable.

Currently the methods for version controlling data is haphazard. The most
commonly employed technique seems to be incorporating metadata into the
filename of the data. While a system that utilizes filename metadata might be
useable, the main issue is that the data is mutable - files can be accidentally
overwritten. From a data storage point of view, this can also be very
inefficient since different files may have much in common, leading to redundant
storage. 

An issue that code versioning systems do not have to deal with is the problem
of attributing the source of creation. The vast majority of code is written by
humans, and therefore the source information is often found in the commit
comment. Otherwise, if the data is forked, a clear trail exists as to where the
code originated from. However data can come from many sources. It can be raw in
the sense of being pulled from some outside system. It can be processed from an
original source, and have undergone many subsequent transformations, such as
having been processed by either code, or code with a model. 

The fact that data now is often processed by models brings us back to the
original difficulty. Models are artifacts that are the by products of both code
and data. Without the reproducibility problem in data solved, data that is 
transformed by models propagates this problem to the models as well (since they
are partial offspring of data as well).


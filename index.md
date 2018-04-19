---
layout: entry
title: Computational Lingustic
---

## Universal Dependencies Annotation Guidelines

### Nominals

The UD annotation assumes the nominal, or noun phrase, as one of the basic structures that we expect to find in all languages. A nominal minimally consists of a noun, proper noun or pronoun.

*ann format*

~~~ ann
Barack Obama is the current president.
T1 PERSON 0 12 Barack Obama
~~~


## Testing ConLL Universal Dependencies

*conllu foramt*

~~~ conllu
1    They    they    PRON    PRN    Case=Nom|Num=Plur            2    nsubj    _    _
2    buy     buy     VERB    VBP    Num=Plur|Per=3|Tense=Pres    0    root     _    _
3    books   book    NOUN    NNS    Num=Plur                     2    dobj     _    _
~~~

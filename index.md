---
layout: entry
title: Universal Dependencies Annotation Guidelines
---


## CoNL-U Format

Annotations are encoded in plain text files (UTF-8, LF character as line break + LF char as EOF) with three types of lines:
* Word lines cotaining the annotation of a token in **10 fields separated by single tab characters**; has (sdadasdasdasdsa
* Blank lines marking sentence boundaries;
* Comment lines strarting with ha


Senteces consist of one or more word lines, and word lines cotain the following fields:
1. ID: Word index, integer starting at 1;
2. FORM: Word form or punctuation symbol;
3. LEMMA: Lemma or stem word form;
4. UPOS: Universal part-of-speech tag;
5. XPOS: Language-specific part-of-speech tag (underscore if not available);
6. FEATS: List of morphological features from the unviersal feature inventory or froma defined language-specific extension (underscore if not available)
7. HEAD: Head of the current word, which is either a value of ID or zero;
8. DEPREL: Universal dependency relation to the HEAD or a defined language-specific subtype of one;
9. DEPS: Enhanced dependency graph in the form of a list of head-deprel pairs;
10. MISC: Any other annotation.

## Nominals

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


*test*


~~~ conllu
1	She	she	PRON	PRN	Case=Nom|Num=Sing	2	nsubj	_	_
2	sees	see	VERB	VBP	Num=Sing|Per=3|Tense=Pres	0	root	_	_
~~~

---
layout: entry
title: Universal Dependencies Annotation Guidelines
---


## CoNL-U Format

Annotations are encoded in plain text files (UTF-8, LF character as line break + LF char as EOF) with three types of lines:
* Word lines cotaining the annotation of a token in **10 fields separated by single tab characters**;
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

|                    | Nominals                                 | Clauses                    | Modifier words         | Function words        |
|-------------------:|------------------------------------------|----------------------------|------------------------|-----------------------|
| **Core arguments**     |   nsubj;  obj;  iobj;                  |  csubj;  ccomp;  xcomp; |                        |                       |
| **Non-core arguments** |   obl;  vocative;  expl;  dislocated; |  advcl;                   |  advmod;  discourse; |  aux;  cop;  mark; |
| **Nominal dependents** |    nmod;  appos;  nummod;               |  acl;                     |  amod;                |  det;  clf;  case; |



## Nominals

The UD annotation assumes the nominal, or noun phrase, as one of the basic structures that we expect to find in all languages. A nominal minimally consists of a noun, proper noun or pronoun.



~~~ conllu
1	Dondal	_	NOUN	_	_	2	_	_	_
2	Trump	_	NOUN	_	_	3	nsubj	_	_
3	is	_	VERB	_	_	0	root	_	_
4	the	_	DET	_	_	6	_	_	_
5	current	_	_	_	6	_	_	_	_
6	president	_	_	_	2	obj	_	_	_	

~~~


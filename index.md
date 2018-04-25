---
layout: entry
title: Universal Dependencies Annotation Guidelines
---


## CoNLL-U Format

Annotations are encoded in plain text files (UTF-8, LF character as line break + LF char as EOF) with three types of lines:
* Word lines cotaining the annotation of a token in **10 fields separated by single tab characters**;
* Blank lines marking sentence boundaries;
* Comment lines strarting with hash #.


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

## Syntactic relations Table

|                    | Nominals                                 | Clauses                    | Modifier words         | Function words        |
|-------------------:|------------------------------------------|----------------------------|------------------------|-----------------------|
| **Core arguments**     |   nsubj;  obj;  iobj;                  |  csubj;  ccomp;  xcomp; |                        |                       |
| **Non-core arguments** |   obl;  vocative;  expl;  dislocated; |  advcl;                   |  advmod;  discourse; |  aux;  cop;  mark; |
| **Nominal dependents** |    nmod;  appos;  nummod;               |  acl;                     |  amod;                |  det;  clf;  case; |


### **nsubj**
A nominal subject (nsubj) is a nominal which is the syntactic subject and the proto-agent of a clause. That is, it is in the position that passes typical grammatical test for subjecthood, and this argument is the more agentive, the do-er, or the proto-agent of the clause. This nominal may be headed by a noun, or it may be a pronoun or relative pronoun or, in ellipsis contexts, other things such as an adjective.

**New from v2: The nsubj relation is also used for the nominal subject of a passive verb or verb group, even though the subject is then not typically the proto-agent argument due to valency changing operations**. For languages that have a grammaticalized passive transformation, it is strongly recommended to **use the subtype nsubj:pass** in such cases.

The nsubj role is only applied to semantic arguments of a predicate. *When there is an empty argument in a grammatical subject position (sometimes called a pleonastic or expletive), it is labeled as expl or better expl:impers*

~~~ conllu
1	Clinton	_	_	_	_	2	nsubj;	_	_
2	defeated	_	_	_	_	0	_	_	_
3	Dole	_	_	_	_	2	_	_	_

~~~
~~~ conllu
1	Clinton	_	_	_	_	3	nsubj:pass;	_	_
2	was	_	_	_	_	3	_	_	_
3	defeated	_	_	_	_	0	_	_	_
4	by	_	_	_	_	5	_	_	_
5	Clinton	_	_	_	_	3	_	_	_

~~~

~~~ conllu
1	Si	_	_	_	_	3	expl:impers;	_	_
2	può	_	_	_	_	3	_	_	_
3	procedere	_	_	_	_	0	_	_	_

~~~

### **obj**

The object of a verb is the second most core argument of a verb after the subject. Typically, it is the noun phrase that denotes the entity acted upon or which undergoes a change of state or motion (the proto-patient).

**In general, if there is just one object, it should be labeled obj, regardless of the morphological case or semantic role that it bears. If there are two or more objects, one of them should be obj and the others should be iobj**. In such cases it is necessary to decide what is the most directly affected object (patient).

~~~ conllu
1	She	_	_	_	_	2	_	_	_
2	gave	_	_	_	_	0	_	_	_
3	me	_	_	_	_	2	_	_	_
4	a	_	_	_	_	4	_	_	_
5	raise	_	_	_	_	2	obj	_	_

~~~

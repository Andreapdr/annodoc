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

<table>
<thead>
<tr class="header">
<th></th>
<th>Nominals</th>
<th>Clauses</th>
<th>Modifier words</th>
<th>Function words</th>
</tr>
</thead>
<tbody>
<tr>
<td markdown="span">**Core arguments**</td>
<td markdown="span">nsubj, obj, iobj</td>
<td markdown="span">csubj, ccomp, xcomp</td>
<td markdown="span"></td>
<td markdown="span"></td>
</tr>
<tr>
<td markdown="span">**Non-core arguments**</td>
<td markdown="span">obl, vocative, expl, dislocated</td>
<td markdown="span">advcl</td>
<td markdown="span">advmod, discourse</td>
<td markdown="span">aux, cop, mark</td>
</tr>
<td markdown="span"> **Nominal dependents** </td>
<td markdown="span">nmod, appos, nummod</td>
<td markdown="span">acl</td>
<td markdown="span">amod</td>
<td markdown="span">det, clf, case</td>
<tr>
</tr>
</tbody>
</table>


### **nsubj: nominal subject**
A nominal subject (nsubj) is a nominal which is the syntactic subject and the proto-agent of a clause. That is, it is in the position that passes typical grammatical test for subjecthood, and this argument is the more agentive, the do-er, or the proto-agent of the clause. This nominal may be headed by a noun, or it may be a pronoun or relative pronoun or, in ellipsis contexts, other things such as an adjective.

**New from v2: The nsubj relation is also used for the nominal subject of a passive verb or verb group, even though the subject is then not typically the proto-agent argument due to valency changing operations**. For languages that have a grammaticalized passive transformation, it is strongly recommended to **use the subtype nsubj:pass** in such cases.

The nsubj role is only applied to semantic arguments of a predicate. *When there is an empty argument in a grammatical subject position (sometimes called a pleonastic or expletive), it is labeled as expl or better expl:impers*

~~~ conllu
1	Clinton	_	_	_	_	2	nsubj	_	_
2	defeated	_	_	_	_	0	_	_	_
3	Dole	_	_	_	_	2	_	_	_

~~~
~~~ conllu
1	Clinton	_	_	_	_	3	nsubj:pass	_	_
2	was	_	_	_	_	3	_	_	_
3	defeated	_	_	_	_	0	_	_	_
4	by	_	_	_	_	5	_	_	_
5	Clinton	_	_	_	_	3	_	_	_

~~~

~~~ conllu
1	Si	_	_	_	_	3	expl:impers	_	_
2	può	_	_	_	_	3	_	_	_
3	procedere	_	_	_	_	0	_	_	_

~~~

### **obj: (direct) object**

The object of a verb is the second most core argument of a verb after the subject. Typically, it is the noun phrase that denotes the entity acted upon or which undergoes a change of state or motion (the proto-patient).

**In general, if there is just one object, it should be labeled obj, regardless of the morphological case or semantic role that it bears. If there are two or more objects, one of them should be obj and the others should be iobj**. In such cases it is necessary to decide what is the most directly affected object (patient).

~~~ conllu
1	She	_	_	_	_	2	_	_	_
2	gave	_	_	_	_	0	_	_	_
3	me	_	_	_	_	2	_	_	_
4	a	_	_	_	_	5	_	_	_
5	raise	_	_	_	_	2	obj	_	_

~~~

### **iobj: indirect object**

The indirect object of a verb is any nominal phrase that is a core argument of the verb but is not its subject or (direct) object. The prototypical example is the recipient of ditransitive verbs of exchange:

~~~ conllu
1	She	_	_	_	_	2	_	_	_
2	gave	_	_	_	_	0	_	_	_
3	me	_	_	_	_	2	iobj	_	_
4	a	_	_	_	_	5	_	_	_
5	raise	_	_	_	_	2	_	_	_

~~~

In general, if there is just one object, it should be labeled obj, regardless of the morphological case or semantic role. For example, in English, teach can take either the subject matter or the recipient as the only object, and in both cases it would be analyzed as the obj:

~~~ conllu
1	She	_	_	_	_	2	_	_	_
2	teaches	_	_	_	_	0	_	_	_
3	computational	_	_	_	_	4	_	_	_
4	linguistics	_	_	_	_	2	obj	_	_

~~~

The indirect object of a verb is a pronominal complement which corresponds to a dative object. **In Italian the iobj only appears as clitic pronoun because when the indirect object is realized as a prepositional phrase, it is labeled as nmod (ex. Dare a qualcuno qualcosa, give something to someone).**

~~~ conllu
1	Lui	_	_	_	_	3	_	_	_
2	le	_	_	_	_	3	iobj	_	_
3	regalò	_	_	_	_	0	_	_	_
4	un	_	_	_	_	5	_	_	_
5	salvadanaio	_	_	_	_	3	_	_	_

~~~

~~~ conllu
1	Mi	_	_	_	_	2	iobj	_	_
2	sembra	_	_	_	_	0	_	_	_
3	tutto	_	_	_	_	2	_	_	_
4	un	_	_	_	_	5	_	_	_
5	salvadanaio	_	_	_	_	2	_	_	_

~~~

### **csubj: clausal subject**

A clausal subject is a clausal syntactic subject of a clause, i.e., **the subject is itself a clause**. The governor of this relation might not always be a verb: when the verb is a copular verb, the root of the clause is the complement of the copular verb. The dependent is the main lexical verb or other predicate of the subject clause

New from v2: The csubj relation is also used for the clausal subject of a passive verb or verb group. For languages that have a grammaticalized passive transformation, it is strongly recommended to use the subtype csubj:pass in such cases.

~~~ conllu
1	What	_	_	_	_	3	_	_	_
2	she	_	_	_	_	3	_	_	_
3	said	_	_	_	_	4	csubj	_	_
4	makes	_	_	_	_	0	_	_	_
5	sense	_	_	_	_	4	_	_	_

~~~

~~~ conllu
1	È	_	_	_	_	2	_	_	_
2	stato	_	_	_	_	3	_	_	_
3	facile	_	_	_	_	0	_	_	_
4	ricostruire	_	_	_	_	3	csubj	_	_
5	le	_	_	_	_	6	_	_	_
6	telefonate	_	_	_	_	4	_	_	_

~~~

### **ccomp: clausal complement**

A clausal complement of a verb or adjective is a dependent clause which is a core argument. That is, it functions like an object of the verb, or adjective.

~~~ conllu
1	He	_	_	_	_	2	_	_	_
2	says	_	_	_	_	0	_	_	_
3	that	_	_	_	_	5	mark	_	_
4	you	_	_	_	_	5	_	_	_
5	like	_	_	_	_	2	ccomp	_	_
6	to	_	_	_	_	7	_	_	_
7	swim	_	_	_	_	5	_	_	_

~~~

~~~ conllu
1	He	_	_	_	_	2	_	_	_
2	says	_	_	_	_	0	_	_	_
3	you	_	_	_	_	4	_	_	_
4	like	_	_	_	_	2	ccomp	_	_
5	to	_	_	_	_	6	_	_	_
6	swim	_	_	_	_	4	_	_	_

~~~

Such clausal complements may be finite or nonfinite. However, if the subject of the clausal complement is controlled **(that is, must be the same as the higher subject or object, with no other possible interpretation)** the appropriate relation is xcomp.


### **advcl: adverbial clause modifiers**

A clause which modifies a verb or a predicate, as a modifier not as a core-complement. This includes things such as a temporal clause, consequence, conditional clause, purpose clause, etc. **The dependent must be clausal (or else it is an advmod) and the dependent is the main predicate of the clause**.

~~~ conllu
1	The	_	_	_	_	0	_	_	_
2	accident	_	_	_	_	0	_	_	_
3	happened	_	_	_	_	0	_	_	_
4	as	_	_	_	_	0	_	_	_
5	night	_	_	_	_	0	_	_	_
6	was	_	_	_	_	0	_	_	_
7 falling _ _ _ _ 3 advcl _ _

~~~

~~~ conllu
1	He	_	_	_	_	0	_	_	_
2	talked	_	_	_	_	0	_	_	_
3	to	_	_	_	_	0	_	_	_
4	him	_	_	_	_	0	_	_	_
5	in	_	_	_	_	0	_	_	_
6	order	_	_	_	_	0	_	_	_
7	to	_	_	_	_	0	_	_	_
8	secure	_	_	_	_	2	advcl	_	_
9	the	_	_	_	_	0	_	_	_
10	account	_	_	_	_	0	_	_	_

~~~


### **acl: adnominal clause modifiers**

A clause which modifies a nominal.


~~~ conllu
1	I	_	_	_	_	0	_	_	_
2	have	_	_	_	_	0	_	_	_
3	a	_	_	_	_	0	_	_	_
4	parakeet	_	_	_	_	0	_	_	_
5	named	_	_	_	_	4	acl	_	_
6	cookie	_	_	_	_	0	_	_	_

~~~



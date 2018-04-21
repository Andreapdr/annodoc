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



~~~ conllu
1	Dondal	_	NOUN	_	_	2	_	_	_
2	Trump	_	NOUN	_	_	3	nsubj	_	_
3	is	_	VERB	_	_	0	root	_	_
4	the	_	DET	_	_	6	_	_	_
5	current	_	_	_	6	_	_	_	_
6	president	_	_	_	2	obj	_	_	_	

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
1	E	e	CCONJ	CC	_	2	cc	_	_
2	quel	quello	PRON	PD	Gender=Masc|Number=Sing|PronType=Dem	15	nsubj	_	_
3	che	che	PRON	PR	PronType=Rel	10	nsubj:pass	_	_
4-5	dell’	_	_	_	_	_	_	_	SpaceAfter=No
4	di	di	ADP	E	_	6	case	_	_
5	l’	il	DET	RD	Definite=Def|Number=Sing|PronType=Art	6	det	_	_
6	Europa	Europa	PROPN	SP	_	10	obl	_	_
7	non	non	ADV	BN	PronType=Neg	10	advmod	_	_
8	sarà	essere	AUX	VA	Mood=Ind|Number=Sing|Person=3|Tense=Fut|VerbForm=Fin	10	aux	_	_
9	stato	essere	AUX	VA	Gender=Masc|Number=Sing|Tense=Past|VerbForm=Part	10	aux:pass	_	_
10	consumato	consumare	VERB	V	Gender=Masc|Number=Sing|Tense=Past|VerbForm=Part	2	acl:relcl	_	_
11-12	dalla	_	_	_	_	_	_	_	_
11	da	da	ADP	E	_	13	case	_	_
12	la	il	DET	RD	Definite=Def|Gender=Fem|Number=Sing|PronType=Art	13	det	_	_
13	guerra	guerra	NOUN	S	Gender=Fem|Number=Sing	10	obl:agent	_	SpaceAfter=No
14	,	,	PUNCT	FF	_	2	punct	_	_
15	finirà	finire	VERB	V	Mood=Ind|Number=Sing|Person=3|Tense=Fut|VerbForm=Fin	0	root	_	_
16-17	coll’	_	_	_	_	_	_	_	SpaceAfter=No
16	con	con	ADP	E	_	19	case	_	_
17	l’	il	DET	RD	Definite=Def|Number=Sing|PronType=Art	19	det	_	_
18	essere	essere	AUX	VA	VerbForm=Inf	19	aux:pass	_	_
19	distrutto	distruggere	VERB	V	Gender=Masc|Number=Sing|Tense=Past|VerbForm=Part	15	obl	_	_
20	in	in	ADP	E	_	21	case	_	_
21	breve	breve	ADJ	A	Number=Sing	19	obl	_	SpaceAfter=No
22	,	,	PUNCT	FF	_	19	punct	_	_
23	senza	senza	ADP	E	_	25	case	_	_
24	più	più	ADV	B	_	25	advmod	_	_
25	rimedio	rimedio	NOUN	S	Gender=Masc|Number=Sing	19	obl	_	SpaceAfter=No
26	,	,	PUNCT	FF	_	15	punct	_	_
27-28	dalla	_	_	_	_	_	_	_	_
27	da	da	ADP	E	_	29	case	_	_
28	la	il	DET	RD	Definite=Def|Gender=Fem|Number=Sing|PronType=Art	29	det	_	_
29	pace	pace	NOUN	S	Gender=Fem|Number=Sing	15	obl	_	SpaceAfter=No
30	.	.	PUNCT	FS	_	15	punct	_	SpacesAfter=\n\n

~~~

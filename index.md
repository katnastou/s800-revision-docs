---
layout: entry
title: Documentation for Typed Relation Annotation
---

# General guidelines

Annotations should be made according to the annotator’s best understanding of the __author’s intended meaning in context__. For example, relations expressed using ambiguous verbs such as __"associate"__ that express complex formation in some contexts but not others should be annotated if and only if the annotator interprets the authors as intending to describe complex formation. Annotators __should apply__ their general __background knowledge__ as well as their __domain expertise__ when interpreting author statements.

# Complex formation

Undirected binary relation associating two proteins that form a complex. Annotated for any statement implying the existence of a complex, including statements explicitly discussing the dissociation of a complex.
Relevant ontology terms:
* [GO:0065003](http://amigo.geneontology.org/amigo/term/GO:0065003) (__protein-containing complex assembly__): The aggregation, arrangement and bonding together of a set of macromolecules to form a protein-containing complex.
* [GO:0032984](http://amigo.geneontology.org/amigo/term/GO:0032984) (__protein-containing complex disassembly__): The disaggregation of a protein-containing macromolecular complex into its constituent components.
* [GO:0032991](http://amigo.geneontology.org/amigo/term/GO:0032991) (__protein-containing complex__): A stable assembly of two or more macromolecules, i.e. proteins, nucleic acids, carbohydrates or lipids, in which at least one component is a protein and the constituent parts function together.

Note that by contrast to the scope of [GO:0032991](http://amigo.geneontology.org/amigo/term/GO:0032991) (protein-containing complex) and related terms, the annotated complex formation relation is restricted to cases where both of the associated constituents are _proteins_, _protein complexes_, _protein families_, _protein groups_ or _chemicals_.

## Detailed guidelines

1. Complex formation relations are only annotated between two different protein mentions. In particular, statements such as “homodimerization of A” __are not annotated__
2. Complexes of more than two proteins are annotated by creating __all binary relations__ between the components
3. Nominalized expressions (“interaction of A and B”, “A/B interaction”) and noun phrases with __any surface word__ that can be understood as implying the existence of a complex (“A/B complex”, “A/B heterodimer”) are __annotated__ as expressing complex formation relations. However, in the absence of any such word, text such as “A/B” is not annotated. The text A-B will be annotated based on the understanding of the annotator from the entire context (abstract or paragraph) and not based on former biological knowledge. Exception: Sentences like “A is phosphorylated in vitro using B/C (or B-C)” where B is a kinase and C is a cyclin will be annotated as B_complex_formation_C and we will check the error rate in this specific subproblem
5. __Fusion proteins__ should be treated as one entity for the purposes of annotation and during the creation of the training dataset. These should get an annotator’s note: __Fusion__
  * Note: Due to the inability of marking discontinuous entities, some Fusion proteins have received the Note: __Fusion, discontinuous__ in sentences, example from [11713274](https://pubmed.ncbi.nlm.nih.gov/11713274/)
  ~~~ann
  full-length NRIF3 fused to the DNA-binding domain of Gal4
  T1	GGP 12 17	NRIF3
  T2	GGP 53 57	Gal4
  #1	AnnotatorNotes T1	Fusion, discontinuous
  ~~~
6. Relations __should not be interpreted as combinations__, on the contrary each annotated relation should be __valid on each own__ (e.g. _“A positively regulates the proteolytic degradation of B and that leads to the rapid depletion of B”_, should be annotated as _“A regulation_of_proteolysis B”_ and _“A negative_regulation B”_ and not the combination of relations _“A positive_regulation B”_ and _“A regulation_of_proteolysis B”_)
7. __Co-immunoprecipitation__ can be used as an indicator of complex formation between two protein mentions

## Negation and speculation

1. Statements explicitly __denying__ the formation of a complex (e.g. “A does not bind B”) are __not annotated__ in any way. However, if the negated statement is qualified with conditions in a way that implies that the proteins would normally form a complex, the statement is annotated as if the negation were absent (e.g. _“When A is phosphorylated, it fails to form a complex with B”_).
2. Statements expressed __speculatively__ or with __hedging__ expressions (e.g. _“may form a complex”_) are __annotated__ identically to affirmative statements (in effect, __speculation and hedging are ignored__).

## Specific rules for complexes/families and plural form annotations

1. __Complexes__, __Families__ and __Groups__ of proteins receive a __GGP__ annotation and an Annotator's __Note__ (_“Complex”_, _“Family”_, _"Group"_) stating their type.
2. The words _“complex”_, _“family”_ and _"group"_ should __not__ be part of the entity annotations.
3. Plural forms should be marked as “plural” in the annotation notes only if the protein(s) mentioned do not form a complex, do not belong in the same family or cannot be considered as forming a group.

4. The following complexes/families/groups should get the corresponding annotations (Exception: if in specific organisms a family is only represented by one protein member and in that organism the names of the family and the protein entity __coincide__, then the context should be used to adress how that mention should be annotated).
  * NF-kappaB: __Complex__
  * kappa B: __Complex__
  * NF-kappaB/Rel: __Complex__ (annotated as 1 entity)
  * AP-1: __Complex__
  * AP-2: __Complex__
  * TFIID: __Complex__
  * LPT: __Complex__
  * AMPK: __Complex__
  * Cohesin: __Complex__
  * Condesin: __Complex__
  * SMC: __Complex__
  * NFAT: __Family__
  * Rel: __Family__
  * TNF: __Family__
  * Ets: __Family__
  * EGR: __Family__
  * GATA: __Family__
  * TNFR: __Family__
  * TcR: __Family__
  * CREB/ATF: __Family__
  * RIP: __Family__
  * I kappa B: __Family__
  * STAT: __Family__
  * TRAF: __Family__
  * GPCR (7TMR): __Family__
  * G-protein: __Family__
  * GRK: __Family__
  * EBS: __Family__
  * Caveolin: __Family__
  * HSP: __Family__
  * Presenilin: __Family__
  * Wnt: __Family__
  * Frizzled: __Family__
  * PKC: __Family__
  * JNK: __Family__
  * C-terminal binding proteins (CtBPs): __Family__
  * CDK: __Family__
  * FGFR: __Family__
  * 14-3-3: __Family__
  * SIK: __Family__
  * E2F: __Group__
  * MHC class I: __Group__
  * MHC class II: __Group__
  * ERK: __Group__
  * MEK: __Group__
  * E1: __Group__
  * E2: __Group__
  * E3: __Group__
  * Histones: __Group__
  * TOR: __Group__
  * T Cell Factor (TCF): __Group__
  * HDAC: __Class__
  * Dopamine receptors: __Class__
5. Annotations should be applied to all variants: e.g. __NF kappaB__, __NF-kappaB__, __NFkappaB__ should all be marked as __Complex__

## Topics for discussion

* Cytokines as a group of entities are not annotated. Should we change that rule?
* How should we treat pathways? E.g. TOR pathway? Originally I didn’t annotate those, but later it made more sense to annotate TOR as a group, as one can view that as negative example. Not really sure which approach is best.
* I have added histone acetylation/deacetylation as interactions, not sure if we want those
* Amino acids are not annotated as chemicals unless they are not part of the polypeptide chain
* Should we annotate ubiquitin and E1, E2, E3 ligases? Also when the mention is E3 ubiquitin ligase, should it be annotated as one mention or E3 ligase as one and ubiquitin as another? 
* Do we annotate complex formation for proteins across species? E.g. viral-host interactions. I am not sure if that is consistent across the corpus, but I generally tried to annotate cross-species relationships when they were viral-host interactions.
* How do we annotate interactions between proteins when one or both partners carry mutations that alter their physicochemical behavior?


For information on Annodoc, see <http://spyysalo.github.io/annodoc/>.

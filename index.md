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
~~~ ann
direct inhibition of NFATp/AP-1 complex formation by a nuclear hormone receptor
T1	GGP 21 26	NFATp
T2	GGP 27 31	AP-1
R10	Complex_formation Arg1:T1 Arg2:T2	 
~~~
5. __Fusion proteins__ should be treated as one entity for the purposes of annotation and during the creation of the training dataset. These should get an annotator’s note: __Fusion__
  * Note: Due to the inability of marking discontinuous entities, some Fusion proteins have received the Note: __Fusion, discontinuous__ in sentences, example from [11713274](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/physical-interaction-dbs-abstracts-01/11713274?focus=sent~10)
~~~ ann
full-length NRIF3 fused to the DNA-binding domain of Gal4
T1	GGP 12 17	NRIF3
T2	GGP 53 57	Gal4
~~~
6. Relations __should not be interpreted as combinations__, on the contrary each annotated relation should be __valid on each own__ (e.g. _“A positively regulates the proteolytic degradation of B and that leads to the rapid depletion of B”_, should be annotated as _“A regulation_of_proteolysis B”_ and _“A negative_regulation B”_ and not the combination of relations _“A positive_regulation B”_ and _“A regulation_of_proteolysis B”_)
7. __Co-immunoprecipitation__ can be used as an indicator of complex formation between two protein mentions
8. _“A regulation_of_proteolysis B”_ does not necessarily imply _"A negative regulation of B"_, so this should be annotated with care
9. Post-translational modifications should __not__ receive a binding annotation unless binding is clearly mentioned in context. PTMs imply transient interactions which will not be present in physical interaction databases, so they shouldn't be annotated as such. For an example of a corner case see [General examples](#general-examples-not-from-the-corpus)


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

## Specific Examples discussed

<div class="tip" markdown="1">
* Instances of binding and phosphorylation should be seperately annotated as two events when binding is clearly mentioned in text.
<pre><code>
PPP1R12A is phosphorylated at Ser-473 by CDK1 during mitosis, creating docking sites for the POLO box domains of PLK1. Subsequently, PLK1 binds and phosphorylates PPP1R12A.
 
CDK1 Catalysis_of_phosphorylation PPP1R12A
PLK1 Catalysis_of_phosphorylation PPP1R12A
</code></pre>
2. When _Regulation of Transcription_ is implied, it should be preffered over the parent term _Regulation of Gene Expression_, thus annotating the __authors intended meaning in context__ instead of the most accurate term in the relation hierarchy.
~~~ ann
HSF1 can function as both an activator of heat shock genes and a repressor of non-heat shock genes such as IL1B and c-fos.
~~~
<pre><code>
HSF1 Positive Regulation heat shock genes
HSF1 Negative Regulation non-heat shock genes
HSF1 Negative Regulation IL1B
HSF1 Negative Regulation c-fos
HSF1 Regulation of Transcription IL1B
HSF1 Regulation of Transcription c-fos
</code></pre>
3.	When the level at which the protein product is regulated at is not clear, then the general term _Regulation of Gene Expression_ should be used.
~~~ ann
We demonstrated that IL-12 directly up-regulates IRF-1 to the same extent as IFN-alpha in normal human T cells and in NK cells.
~~~
<pre><code>
IL-12      Regulation of Gene Expression    IRF-1
IFN-alpha             Regulation of Gene Expression    IRF-1
IL-12      Positive Regulation               IRF-1
IFN-alpha             Positive Regulation             IRF-1
</code></pre>
4. When positive/negative regulation of the catalysis of a post-translational modification is mentioned then the generic type _"A Regulation B"_ should be used, and no reference to "positive/negative" should be made, if the effect to protein levels is unclear.
~~~ ann
A negatively regulates the phosphorylation of B
~~~
<pre><code>
A Regulation B
</code></pre>
Note: The idea behind using the general term _Regulation_ is that we want to get in there as much as possible in terms of directionality for the edges. So, in order to do that, we will have to be a little bit more flexible with the hierarchy to include something very general that would allow us to have directionality, even in cases where we don’t know the type of effect A has on B, but we know it is upstream. Also, we would have to be a bit more flexible with what we annotate in general and even in cases where we are not 100% sure, to add an annotation (as long as we are pretty certain it is what the authors mean). The relevant GO term is [Regulation of biological process](http://amigo.geneontology.org/amigo/term/GO:0050789)
5. When _Complex formation_ is not clear, _Regulation_ should be used for annotating a relationship instead e.g. relationship between TNFR1 and TRAF2 in this sentence [9353251](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-02/9353251?focus=sent~6)
6.  In the current scheme we can annotate the semantics of e.g. "A negatively regulates the expression of B" by assigning _two relations_: _A  negatively regulates B_ AND _A Regulation of Gene Expression B_ 
</div>

## Removed abstracts

In this section I will try to explain the reasoning behind marking some abstracts for removal:
* The reasoning behind removal and not leaving abstracts simply unannonated is to make sure that abstracts that couldn't be annotated not only are not present on our positive, but also not on our negative examples.
* Creation of annotations for discontinuous texts (e.g. leaving out a sentence in between two annotated sentences), should be avoided, as this can cause a number of challenges for downstream use, e.g. for ML using contexts larger than isolated sentences. So either entire abstracts are marked for removal or X number of sentences from the beginning or the end of the document (An example is [9845517](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-01/9845517) where only the second to last sentence was confusing, so the last two sentences were removed). These are all indicated with Annotator's notes.
* It is generally a good idea to get rid of abstracts focusing on Immunoglobulin regions ([this article from UniProt](https://www.uniprot.org/help/immunoglobulins ) on how they try to address the immunoglobulin issue when creating new entries for the database, partially refers to what we discuss). Also, since information like that will never end up in STRING, maybe it’s a good idea to not use such examples neither as positive nor as negative contexts for training. For example in [10228008](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-01/10228008) (I wasn't sure how to annotate relationships in sentences 5, 6 and 7 since these are gene regions, and not the genes themselves)

## Topics for discussion

* Add classes for Complex, Family, Group, Class?
* Cytokines as a group of entities are not annotated. Should we change that rule?
* How should we treat pathways? E.g. TOR pathway? Originally I didn’t annotate those, but later it made more sense to annotate TOR as a group, as one can view that as negative example. Not really sure which approach is best.
* I have added histone acetylation/deacetylation as interactions, not sure if we want those
* Amino acids are not annotated as chemicals unless they are not part of the polypeptide chain
* Should we annotate ubiquitin and E1, E2, E3 ligases? Also when the mention is E3 ubiquitin ligase, should it be annotated as one mention or E3 ligase as one and ubiquitin as another? 
* Do we annotate complex formation for proteins across species? E.g. viral-host interactions. I am not sure if that is consistent across the corpus, but I generally tried to annotate cross-species relationships when they were viral-host interactions.
* How do we annotate interactions between proteins when one or both partners carry mutations that alter their physicochemical behavior?
* when will we tag “regulation of proteolysis” and when “catalysis of ubiquitination” if the ubiquitin system is involved?
* Should we rethink homodimers? I have only annotated very few cases with an annotators note.

# Relation type hierarchy (as of 27/02/2020)

* Regulation
  * Positive_regulation  
  * Negative_regulation
* Complex_formation    
* Regulation_of_gene_expression
  * Regulation_of_transcription
  * Regulation_of_translation
* Regulation_of_proteolysis    
* Catalysis_of_protein_modification
  * Catalysis_of_phosphorylation
  * Catalysis_of_dephosphorylation  
  * Catalysis_of_acetylation
  * Catalysis_of_deacetylation
  * Catalysis_of_methylation
  * Catalysis_of_demethylation
  * Catalysis_of_glycosylation
  * Catalysis_of_deglycosylation
  * Catalysis_of_ubiquitination
  * Catalysis_of_deubiquitination
* Other  

# Annotation Dataset Generation

## Complex formation 01

The script converting the __BioNLP Shared Task-style event annotation__ into binary relations is found [here](https://github.com/spyysalo/binarize-events/commit/b289b1506ede543aad5f19770f3b687a3ff63976). The initial converted data was the [training set of the BioNLP ST 2009] (http://www.nactem.ac.uk/GENIA/current/Shared-tasks/BioNLP-ST-2009/bionlp09_shared_task_training_data_rev2.tar.gz). The conversion process was as follows:
<pre><code>
mkdir tmp
for f in data/bionlp09_shared_task_training_data_rev2/*.a1; do cat ${f%.a1}.{a1,a2} > tmp/$(basename $f .a1).ann; done
mkdir binarized
for f in tmp/*.ann; do python3 binarize.py $f > binarized/$(basename $f); done
</code></pre>
The documents in which the converted data contains at least one Complex_formation document were then selected for annotation:
<pre><code>
egrep -c '^R[0-9]+[[:space:]]Complex_formation' binarized/*.ann | egrep -v ':0$' | wc -l
      97
ls binarized/*.ann | wc -l
     800
</code></pre>
That's 97/800 documents in the original data. While the other 703 could at a minimum serve a useful role in providing negative examples for complex formation, I think it's probably good to at least initially focus on documents likely to provide positive examples.

## Complex formation 02

The process is similar to the generation of Complex formation 01 dataset. The initial converted dataset was the [development set of the BioNLP ST 2009] (http://www.nactem.ac.uk/GENIA/current/Shared-tasks/BioNLP-ST-2009/bionlp09_shared_task_development_data_rev1.tar.gz)

## Physical Interaction Databases Abstracts 01

<TODO>

## Physical Interaction Databases Full-text Paragraphs 01

<TODO>



For information on Annodoc, see <http://spyysalo.github.io/annodoc/>.

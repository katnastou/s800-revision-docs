---
layout: entry
title: Documentation for Typed Relation Annotation
---

## General guidelines

Annotations should be made according to the annotator’s best understanding of the __author’s intended meaning in context__. For example, relations expressed using ambiguous verbs such as __"associate"__ that express complex formation in some contexts but not others should be annotated if and only if the annotator interprets the authors as intending to describe complex formation. Annotators __should apply__ their general __background knowledge__ as well as their __domain expertise__ when interpreting author statements.

## Complex formation

Undirected binary relation associating two proteins that form a complex. Annotated for any statement implying the existence of a complex, including statements explicitly discussing the dissociation of a complex.
Relevant ontology terms:
* [GO:0065003](http://amigo.geneontology.org/amigo/term/GO:0065003) (__protein-containing complex assembly__): The aggregation, arrangement and bonding together of a set of macromolecules to form a protein-containing complex.
* [GO:0032984](http://amigo.geneontology.org/amigo/term/GO:0032984) (__protein-containing complex disassembly__): The disaggregation of a protein-containing macromolecular complex into its constituent components.
* [GO:0032991](http://amigo.geneontology.org/amigo/term/GO:0032991) (__protein-containing complex__): A stable assembly of two or more macromolecules, i.e. proteins, nucleic acids, carbohydrates or lipids, in which at least one component is a protein and the constituent parts function together.

Note that by contrast to the scope of [GO:0032991](http://amigo.geneontology.org/amigo/term/GO:0032991) (protein-containing complex) and related terms, the annotated complex formation relation is restricted to cases where both of the associated constituents are _proteins_, _protein complexes_, _protein families_, _protein groups_ or _chemicals_.

### Detailed guidelines

1. Complex formation relations are only annotated between two different protein mentions. In particular, statements such as “homodimerization of A” __are not annotated__
2. Complexes of more than two proteins are annotated by creating __all binary relations__ between the components
3. Nominalized expressions (“interaction of A and B”, “A/B interaction”) and noun phrases with __any surface word__ that can be understood as implying the existence of a complex (“A/B complex”, “A/B heterodimer”) are __annotated__ as expressing complex formation relations. However, in the absence of any such word, text such as “A/B” is not annotated. The text A-B will be annotated based on the understanding of the annotator from the entire context (abstract or paragraph) and not based on former biological knowledge. Exception: Sentences like “A is phosphorylated in vitro using B/C (or B-C)” where B is a kinase and C is a cyclin will be annotated as B_complex_formation_C and we will check the error rate in this specific subproblem
~~~ ann
direct inhibition of NFATp/AP-1 complex formation by a nuclear hormone receptor
T1	GGP 21 26	NFATp
T2	GGP 27 31	AP-1
R1	Complex_formation Arg1:T1 Arg2:T2	 
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


### Negation and speculation

1. Statements explicitly __denying__ the formation of a complex (e.g. “A does not bind B”) are __not annotated__ in any way. However, if the negated statement is qualified with conditions in a way that implies that the proteins would normally form a complex, the statement is annotated as if the negation were absent (e.g. _“When A is phosphorylated, it fails to form a complex with B”_).
2. Statements expressed __speculatively__ or with __hedging__ expressions (e.g. _“may form a complex”_) are __annotated__ identically to affirmative statements (in effect, __speculation and hedging are ignored__).

### Specific rules for complexes/families and plural form annotations

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

### Specific Examples discussed

1. Instances of binding and phosphorylation should be seperately annotated as two events when binding is clearly mentioned in text.
~~~ ann
PPP1R12A is phosphorylated at Ser-473 by CDK1 during mitosis, creating docking sites for the POLO box domains of PLK1. Subsequently, PLK1 binds and phosphorylates PPP1R12A.
T1	GGP 0 8	PPP1R12A
T2	GGP 41 45	CDK1
T3	GGP 113 117	PLK1
T4	GGP 133 137	PLK1
T5	GGP 163 171	PPP1R12A
R1	Catalysis_of_phosphorylation Arg1:T2 Arg2:T1
R2	Catalysis_of_phosphorylation Arg1:T4 Arg2:T5
R3	Complex_formation Arg1:T4 Arg2:T5
~~~
2. When _"regulation of expression"_ is mentioned in text, if the annotator suspects that the intended meaning of the authors is __Regulation of Transcription__ based on the context of the document they have available, then the annotator should annotate __Regulation of Gene Expression__, with a __Note: "Potentially Regulation of Transcription"__.
~~~ ann
HSF1 can function as both an activator of heat shock genes and a repressor of non-heat shock genes such as IL1B and c-fos.
T1	GGP 0 4	HSF1
T2	GGP 107 111	IL1B
T3	GGP 116 121	c-fos
R1 Negative_Regulation Arg1:T1 Arg2:T2
R2 Negative_Regulation Arg1:T1 Arg2:T3
R3 Regulation_of_Gene_Expression Arg1:T1 Arg2:T2
R4 Regulation_of_Gene_Expression Arg1:T1 Arg2:T3
~~~
3.	When the level at which the protein product is regulated at is not clear, then the general term _Regulation of Gene Expression_ should be used.
~~~ ann
We demonstrated that IL-12 directly up-regulates IRF-1 to the same extent as IFN-alpha in normal human T cells and in NK cells.
T1	GGP 21 26	IL-12
T2	GGP 49 54	IRF-1
T3	GGP 77 86	IFN-alpha
R1 Regulation_of_Gene_Expression Arg1:T1 Arg2:T2
R2 Regulation_of_Gene_Expression Arg1:T3 Arg2:T2
R3 Positive_Regulation Arg1:T1 Arg2:T2
R4 Positive_Regulation Arg1:T3 Arg2:T2
~~~
4. When positive/negative regulation of the catalysis of a post-translational modification is mentioned then the generic type _"A Regulation B"_ should be used, and no reference to "positive/negative" should be made, if the effect to protein levels is unclear.
~~~ ann
A negatively regulates the phosphorylation of B
T1	GGP 0 1	A
T2	GGP 46 47	B
R1 Regulation Arg1:T1 Arg2:T2
~~~
Note: The idea behind using the general term _Regulation_ is that we want to get in there as much as possible in terms of directionality for the edges. So, in order to do that, we will have to be a little bit more flexible with the hierarchy to include something very general that would allow us to have directionality, even in cases where we don’t know the type of effect A has on B, but we know it is upstream. Also, we would have to be a bit more flexible with what we annotate in general and even in cases where we are not 100% sure, to add an annotation (as long as we are pretty certain it is what the authors mean). The relevant GO term is [Regulation of biological process](http://amigo.geneontology.org/amigo/term/GO:0050789)
5. When _Complex formation_ is not clear, _Regulation_ should be used for annotating a relationship instead e.g. relationship between TNFR1 and TRAF2 in this sentence [9353251](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-02/9353251?focus=sent~6)
6.  In the current scheme we can annotate the semantics of e.g. "A negatively regulates the expression of B" by assigning _two relations_: _A  negatively regulates B_ AND _A Regulation of Gene Expression B_ 

### Removed abstracts

In this section I will try to explain the reasoning behind marking some abstracts for removal:
* The reasoning behind removal and not leaving abstracts simply unannonated is to make sure that abstracts that couldn't be annotated not only are not present on our positive, but also not on our negative examples.
* Creation of annotations for discontinuous texts (e.g. leaving out a sentence in between two annotated sentences), should be avoided, as this can cause a number of challenges for downstream use, e.g. for ML using contexts larger than isolated sentences. So either entire abstracts are marked for removal or X number of sentences from the beginning or the end of the document (An example is [9845517](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-01/9845517) where only the second to last sentence was confusing, so the last two sentences were removed). These are all indicated with Annotator's notes.
* It is generally a good idea to get rid of abstracts focusing on Immunoglobulin regions ([this article from UniProt](https://www.uniprot.org/help/immunoglobulins) on how they try to address the immunoglobulin issue when creating new entries for the database, partially refers to what we discuss). Also, since information like that will never end up in STRING, maybe it’s a good idea to not use such examples neither as positive nor as negative contexts for training. For example in [10228008](http://ann.turkunlp.org:8088/index.xhtml#/string-relation-corpus/complex-formation-batch-01/10228008) (I wasn't sure how to annotate relationships in sentences 5, 6 and 7 since these are gene regions, and not the genes themselves)

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

## Relation type hierarchy (as of 27/02/2020)

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

## Annotation Dataset Generation

### Complex formation 01

The script converting the __BioNLP Shared Task-style event annotation__ into binary relations is found [here](https://github.com/spyysalo/binarize-events/commit/b289b1506ede543aad5f19770f3b687a3ff63976). The initial converted data was the [training set of the BioNLP ST 2009](http://www.nactem.ac.uk/GENIA/current/Shared-tasks/BioNLP-ST-2009/bionlp09_shared_task_training_data_rev2.tar.gz). The conversion process was as follows:
```shell
mkdir tmp
for f in data/bionlp09_shared_task_training_data_rev2/*.a1; do 
 cat ${f%.a1}.{a1,a2} > tmp/$(basename $f .a1).ann; 
done
mkdir binarized
for f in tmp/*.ann; do 
 python3 binarize.py $f > binarized/$(basename $f); 
done
```
The documents in which the converted data contains at least one Complex_formation document were then selected for annotation:
```shell
egrep -c '^R[0-9]+[[:space:]]Complex_formation' binarized/*.ann | egrep -v ':0$' | wc -l
      97
ls binarized/*.ann | wc -l
     800
```
That's 97/800 documents in the original data. While the other 703 could at a minimum serve a useful role in providing negative examples for complex formation, I think it's probably good to at least initially focus on documents likely to provide positive examples.

### Complex formation 02

The process is similar to the generation of Complex formation 01 dataset. The initial converted dataset was the [development set of the BioNLP ST 2009](http://www.nactem.ac.uk/GENIA/current/Shared-tasks/BioNLP-ST-2009/bionlp09_shared_task_development_data_rev1.tar.gz)

### Physical Interaction Databases Abstracts 01

* __66,757 papers__ (12,575 in PMC OA) extracted from [BioGRID](https://thebiogrid.org/), [IntAct](https://www.ebi.ac.uk/intact/) and [MINT](https://mint.bio.uniroma2.it/) describing 1 to 298534 physical or genetic interactions each
* Remove papers with __>20 interactions__ in the databases. These papers probably do not discuss interactions in the abstract as they will correspond to more high-throughput experiments
* Keep abstracts where __2-40 entities__ have been tagged
* Split data in abstracts containing entities mentioned __more than 1000 times__ in total (32 unique entities) and abstracts containing entities mentioned __less than 1000 times__ in total (77638 unique entities)
* Normalize, shuffle and randomly select __313 abstracts__ to annotate (the selection process has changed 3 times, so we started with 200 abstracts but ended up with 313 to keep the balance)


### Physical Interaction Databases Full-text Paragraphs 01

* __12,577 PMC OA__ extracted from [BioGRID](https://thebiogrid.org/), [IntAct](https://www.ebi.ac.uk/intact/) and [MINT](https://mint.bio.uniroma2.it/) describing 1 to 298534 physical or genetic interactions each
* Remove papers with __>20 interactions__ in the databases. These papers probably do not discuss interactions in the abstract as they will correspond to more high-throughput experiments
* Keep paragraphs containing 50-500 words
* Keep paragraphs where 2-40 entities have been tagged
* Split data in paragraphs containing entities mentioned __more than 1000 times__ in total (532 unique entities) and paragraphs containing entities mentioned __less than 1000 times__ in total (45037 unique entities)
* Normalize, shuffle and randomly select __100 paragraphs__ to annotate
<details>
<summary>A step-by-step process is described herein. This is run on yellow.</summary>
<p>

<pre><code>
## Lists of PMIDs with interactions from BioGrid, IntAct and MINT
# Copy lists to yellow from local
scp PMIDs_all_physical_int.list user@yellow.jensenlab.org:~/full-text-may-2020/ #66757 PMIDs_all_physical_int.list
scp PMIDs_physical_ints_1-20_interactions.list user@yellow.jensenlab.org:~/full-text-may-2020/ #63998 PMIDs_physical_ints_1-20_interactions.list

# Version sort of PMID numbers
## we want this file to be version sorted, because the tsv with all documents is 
## version sorted, and it takes hours to sort that one instead
sort -V PMIDs_physical_ints_1-20_interactions.list > version_sorted_PMIDs_physical_ints_1-20_interactions.list
sort -V PMIDs_all_physical_int.list > version_sorted_PMIDs_all_physical_int.list

## add PMID: at the beginning of all lines (not necessary, can do the comparison without it as well)
sed -i 's/^/PMID:/' version_sorted_PMIDs_physical_ints_1-20_interactions.list

##---------------------------------------##

## Process Full-texts
-Copy all papers from /data/databases/pmc/
cp /data/databases/pmc/PMC0*_xml_unicode.en.merged.filtered.tsv.gz ./texts

# make dir texts
mkdir texts
cd ./texts

# remove doi from all PMIDs from full-texts
for f in /data/databases/pmc/PMC0*_xml_unicode.en.merged.filtered.tsv.gz
do
    zcat $f | awk 'BEGIN{FS="\t"; OFS="\t"} {gsub(/\|.*/, "", $1); print}' > ${f##*}.nodoi
done

##---------------------------------------##

##Get full texts for papers of interest
#Version sort the files
for f in ./texts/*tsv.gz.nodoi; do sort -k1,1 -V $f > ${f}.sorted; done
#find all the full-texts 
for f in ./texts/*.tsv.gz.nodoi.sorted; do awk -F"\t" 'NR==FNR{a[$0];next}$1 in a' version_sorted_PMIDs_physical_ints_1-20_interactions.list $f;done > full_texts_found.tsv

##---------------------------------------##

## Remove short and long paragraphs and feed to tagger
# the script keeps only paragraphs with more than 50 words and less than 500 words
# it can also do word counts if I uncomment the lines needed
# remember tagger file needs PMID: in front
## also I don't remove the first paragraph after the title to remove abstracts 
## since abstracts can span more than one paragraph
# correct script is on yellow - not locally

perl process_full_text_for_tagger_run.pl full_texts_found.tsv full_texts_paragraphs_50_to_500_words.tsv character_counts_per_paragraph.tsv

##---------------------------------------##

## Run tagger on full text articles

-Move to tagger directory
cd ../tagger-master/
-Make directory to store data and results
mkdir full-text
mkdir full-text/data
mkdir full-text/results

-Copy input data to new dir
cp ../full-text-may-2020/full_texts_paragraphs_50_to_500_words.tsv ./full-text/data/

#make sure that the file starts with PMID
head ./full-text/data/full_texts_paragraphs_50_to_500_words.tsv

#Run tagger
./tagcorpus --threads=4 --autodetect --documents=./full-text/data/full_texts_paragraphs_50_to_500_words.tsv --types=./data/entity_type_human.tsv --entities=/data/dictionary/all_entities.tsv --names=/data/dictionary/all_names_textmining.tsv --groups=/data/dictionary/all_groups.tsv --stopwords=/data/dictionary/all_global.tsv --local-stopwords=/data/dictionary/all_local.tsv --out-matches=./full-text/results/tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_auto_blacklists.tsv 

##---------------------------------------##
# Manipulate results file you get from tagger

The results file has 8 columns
1. Pubmed ID
2. paragraph number
3. sentence number
4. first character of the match
5. last character of the match
6. term matched
7. species taxid
8. Serialno

We have multiple hits with different serial numbers that we do not want. E.g.:
18197 2 1 192 201 EC 2.3.2.2 9606 23932809
18197 2 1 192 201 EC 2.3.2.2 9606 23934249
18197 2 1 192 201 EC 2.3.2.2 9606 23928158
18197 2 1 192 201 EC 2.3.2.2 9606 23934046

#Find unique lines in that file
awk '!seen[$1,$2,$3,$4,$5]++' tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints.tsv > tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique.tsv

#find organism lines and remove them
grep -v -- -3 tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique.tsv > tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv

#Since the file is big in order to do the count of entities I will use awk to find those over 1000 times -- this works for single words only
awk '{for(i=1;i<=NF;i++) a[$i]++} END {for(k in a) print k,a[k]}' <(cut -f8 tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv) | sort -k 2 -n > entities_counts.tsv

#Find entities mentioned over 1000 times
awk '{if ($2>=1000) print $1}' entities_counts.tsv > entities_mentioned_over_1000_times.list

##---------------------------------------##

##Find paragraphs with 2-40 entities

#make seperate files for each PMID_paragraph and remove the original file
awk -F'\t' '{printf("%s\n",$0) >> $1"_"$2".tsv"; close($1"_"$2".tsv")}' tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv

rm tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv
#make a list that counts the matches for each file
find . -maxdepth 1 -type f -exec wc -l {} \; > lines_per_file.tsv

sort -V lines_per_file.tsv > lines_per_file_sorted.tsv

perl -pe 's/\.\///g' lines_per_file_sorted.tsv | perl -pe 's/\.tsv//g' > lines_per_file_sorted_clean.tsv

awk '{if ($1>=2 && $1<=40) print $2;}' lines_per_file_sorted_clean.tsv > PMID_par_2_to_40_entities.list

perl -pe 's/\_/\t/g'  PMID_par_2_to_40_entities.list > PMID_paragraph_with_2_to_40_entities.tsv

cp PMID_paragraph_with_2_to_40_entities.tsv ../
cd ../
perl -pe 's/ /\t/g' PMID_paragraph_with_2_to_40_entities.tsv > PMID_paragraph_with_2_to_40_entities_tab.tsv

#Create new tagger results file for these only
awk -F"\t" 'FNR==NR {hash[$0]; next} $1"\t"$2 in hash' PMID_paragraph_with_2_to_40_entities.tsv tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv > tagger_matches_for_paragraphs_with_2_to_40_entities.tsv

##---------------------------------------##
# Find the abstracts with 2 to 40 entity mentions that have entities in the 1000 list

# Find PMIDs and paragraphs mentioning these entities + remove titles from these
awk -F'\t' '{if ($2!=1) print $0}' tagger_matches_for_paragraphs_with_2_to_40_entities.tsv |cut -f1,2,8 | grep -Fw -f entities_mentioned_over_1000_times.list | cut -f1,2 | sort -uV > PMID_parnum_with_entities_with_over_1000_mentions.tsv

# Find the rest of the paragraph entity pairs and remove the titles
awk -F'\t' '{if ($2!=1) print $0}' tagger_matches_for_paragraphs_with_2_to_40_entities.tsv |cut -f1,2 | sort -uV | grep -Fv -f PMID_parnum_with_entities_with_over_1000_mentions.tsv > PMID_parnum_with_entities_with_under_1000_mentions_notitles.tsv

# There are 226426 PMID_parnum pairs that mention the 532 entities with >1000 mentions
# There are 121718 PMID_parnum pairs that mention the 45037 entities with <1000 mentions
# If we select 100 paragraphs from those we need them to be 99 paragraphs from the 121718 and 1 paragraph from the 226426 (this is an approximation since 45000~=500*100)

cd full-text/results
# RandomlySelect the paragraphs
shuf -n 1 PMID_parnum_with_entities_with_over_1000_mentions.tsv > 1_random_paragraphs.list
shuf -n 99 PMID_parnum_with_entities_with_under_1000_mentions_notitles.tsv > 99_random_paragraphs.list
cat *_random_paragraphs.list > 100_random_paragraphs.list

# Make sure they are not from the same paper
cut -f1 100_random_paragraphs.list | sort -u  | wc -l 
#if this isn't 100 randomly reselect

# Make sure they are not from the papers I have already annotated
#Upload list to yellow
scp manually_annotated_abstracts_CFB01_CFB02_PIB01.list user@yellow.jensenlab.org:~/tagger-master/full-text/results/
#compare pmids I selected with the list
grep -Fv -f manually_annotated_abstracts_CFB01_CFB02_PIB01.list 100_random_paragraphs.list | wc -l
#if it's not 100 reselect

# Find tagger results for these paragraphs
while read ptn; do grep -e "^$ptn\b" tagger_matches_full_text_paragraphs_50_to_500_words_1_to_20_ints_unique_no_org.tsv; done < 100_random_paragraphs.list > tagger_matches_for_100_paragraphs.tsv

##---------------------------------------##

# Generate ann files
# Copy perl script to generate the correct entity starts and ends for brat annotations yellow
scp correct_entity_start_end.pl user@yellow.jensenlab.org:~/tagger-master/full-text/results

cd annotation_results
# Run perl script
perl correct_entity_start_end.pl character_counts_per_paragraph.txt tagger_matches_for_100_paragraphs.txt tagger_matches_for_100_paragraphs_correct_coordinates.txt

# add incremental indexing to files produced
for f in *.tsv
do
    awk -F "\t" '{$1=++i FS $1; printf("T%s\n",$0)}' OFS="\t" $f > "$(basename "$f" .tsv).ann";
done

###!!!!!!!
rm *.tsv (!!!!!be careful that the other files are txt before removing

# And .ann files are now ready :) Let's make the text files for each paragraph.

##---------------------------------------##

# Generate text files

cd ../../../../full-text-may-2020
#get file with PMID and paragraph number
cp ../tagger-master/full-text/results/100_random_paragraphs.list ./

# Make the results file smaller
# Grep the 100 PMIDs
cut -f1 100_random_paragraphs.list > 100_PMIDs_list.list
while read ptn; do grep ^PMID:$ptn full_texts_paragraphs_50_to_500_words.tsv; done < 100_PMIDs_list.list > 100_full_texts.tsv

cd ../tagger-master/full-text/results/
cp ../../../full-text-may-2020/100_full_texts.tsv .
mkdir paragraph_text_results
cp 100_random_paragraphs.list ./paragraph_text_results/
cp 100_full_texts.tsv ./paragraph_text_results/

# Copy perl script over
cd ./paragraph_text_results/
scp ./Desktop/take_paragraphs_for_brat.pl user@yellow.jensenlab.org:~/tagger-master/full-text/results/paragraph_text_results/

sort -V 100_random_paragraphs.list > 100_random_paragraphs_sorted.list
sort -V 100_full_texts.tsv > 100_full_texts_sorted.tsv 

# I am not sure if I need to sort
perl take_paragraphs_for_brat.pl 100_random_paragraphs_sorted.list 100_full_texts_sorted.tsv 

##---------------------------------------##

# Copy files to annotation server
# Connect to brat server
cd /home/ubuntu/git_checkout/brat/data/stringdb/physical-interaction-dbs-01/full-text
scp user@yellow.jensenlab.org:~/tagger-master/full-text/results/annotation_results/\*.ann ./
scp user@yellow.jensenlab.org:~/tagger-master/full-text/results/paragraph_text_results/\*.txt ./
chmod 666 *
</code></pre>

</p>
</details>


### Datasets used to train the models

* __80-20_pos-neg-only-shuffled__: which contains examples from positive (complex formation) and negative (no relationship) examples that have been manually annotated
* __80-20_pos-other-rel-neg-neg-shuffled__: which contains examples from positive (complex formation) and negative examples that consist of both other relationships (other than complex formation) and no relationships between the entities that have been manually annotated
* __Positive set__: All complex formation relationships. Because I saw that some entities might be part of multiple relationships (and I thought that this might introduce some bias in our dataset if we kept the context of those entities multiple times) I tried to reduce that by keeping __only one complex formation relationship for each entity that shows up first in the relationship__ (that roughly means that if the relationship is: A interacts with B and C, and B interacts with C and D, and C interacts with D, I would keep A-B, B-C, C-D and the context around them). I shuffle first, so that not only the first entity in a complex is selected each time.
* __Other relationship set (negative)__: I made this dataset to go into the negative set later. This comprises all other relationship types (other than complex formation) in the data. I masked entities the same way I did for the positive set and used the same bias reduction strategy.
* __No relationship set (negative)__: For this dataset I found all entities that were not in relationship with each other, that were in the same sentence with a distance less that 18 words and which were not equivalent (since, I usually didn’t mark entities more than 5 words away as equivalent if they were not in a relationship, in this case I also checked that the two entities are not the same based on text – of course we will miss some cases this way, but probably not a lot). Afterwards I applied the same technique as above to reduce multiple instances of similar context.
* __Masking__: Entity 1 has been replaced with the [unused1] token, entity 2 with [unused2] all other entities in context with [unused3], thus ignoring equiv entities completely. This should be fixed to mark relationships for all entities and equiv entities. 
* For the creation of all datasets I only kept relationships where the entities have __less than 20 words distance__ and then I kept 100 words to the left and 100 to the right. For the positive and other relationship dataset (see below) I kept relationships even if they spanned more than one sentence, while for the negative I only kept relationships that were on the same sentence. Due to the 18 words restriction in both datasets these cases are fairly limited and no bias is introduced.

For information on Annodoc, see <http://spyysalo.github.io/annodoc/>.

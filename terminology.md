# Terminology

<a name="bel_statement"></a>
### BEL Statement

A BEL Statement is an expression that represents knowledge of the existence of biological entities and relationships between them that are known to be observed within a particular experiment context (i.e. *Experiment Context*), based on some source of prior knowledge such as a scientific publication or newly generated experimental data.

<a name="namespace"></a>
### Namespace

A set of biological identifiers that are curated and maintained by an organization. An example of a namespace is the [Gene Ontology][Gene Ontology] or [HGNC][HGNC] database. These biological identifiers are referenced within a [BEL Statement][BEL Statement].

Examples: `p(HGNC:AKT1) => bp(GO:"apoptotic process")`
- References the *AKT1* gene symbol from the *HGNC* database.
- References the *apoptotic process* process term from the *GO* database.

<a name="annotation"></a>
### Annotation

A name/value property that expresses knowledge about an aspect of a [BEL Nanopub][BEL Nanopub]. You can apply an annotation to the *Experiment Context* or *Metadata* of a [BEL Nanopub][BEL Nanopub].

Examples: Given the [BEL Statement][BEL Statement] `p(HGNC:XRCC5,pmod(R)) => cat(p(HGNC:WRN))`
- We can apply an *Ncbi Taxonomy* annotation value of *Homo sapiens* to the *Experiment Context* section of the [BEL Nanopub][BEL Nanopub].
- We can apply a *Curation Method* annotation value of *Text Mining* to the *Metadata* section of the [BEL Nanopub][BEL Nanopub].

<a name="bel_nanopub"></a>
### BEL Nanopub

A Nanopub is defined by [nanopub.org][nanopub.org]. Quoting their definition:

> A nanopublication is the smallest unit of publishable information: an assertion about anything that can be uniquely identified and attributed to its author.
> 
> Individual nanopublications can be cited by others and tracked for their impact on the community.
> 
> Nanopublications are a natural response to the explosion of high-quality contextual information that overwhelms the capacity of conventional research articles in scholarly communication.

A BEL Nanopub is an instance of a BEL Nanopub to represent biological interactions with an experimental context and provenance. A BEL Nanopub consists of the following parts:

- Citation
  - The identification for the scientific literature where the interaction was stated.
- [BEL Statement][BEL Statement]
  - The biological interaction curated from the Citation.
- Support
  - The section within the Citation that supports the [BEL Statement][BEL Statement]. For example, this may be a text quotation, figure, or table within the Citation.
- Experiment Context
  - The biological context within the experiment where the [BEL Statement][BEL Statement] is observed. For example if the experiment sample was a biopsy on Human, Lung tissue then you might provide an [Annotation][Annotation] of *Ncbi Taxonomy* with value *Homo sapiens* and *Uberon* with value *lung epithelium*.
- Metadata
  - Additional data about the Nanopub itself. For example if the Nanopub was curated using a text mining approach we may provide a *CurationMethod* [Annotation][Annotation] with value *Text Mining*.
- References
  - Identifies the [Annotation][Annotation] and [Namespace][Namespace] databases used in the [BEL Statement][BEL Statement], Experiment Context, and Metadata. For example *Ncbi Taxonomy* may refer to an [Annotation][Annotation] identified by the URI *http://www.openbel.org/bel/namespace/ncbi-taxonomy*.

<a name="asserted_bel_nanopubs"></a>
### Asserted BEL Nanopubs

[BEL Nanopubs][BEL Nanopubs] that are curated by the user and saved in the [Nanopub Store][Nanopub Store] are said to be *asserted*. Although they are created by the user there may be additional provenance associated within the [BEL Nanopub][BEL Nanopub].

Examples:
- We create an individual [BEL Nanopub][BEL Nanopub] and save it to the [Nanopub Store][Nanopub Store]. The [BEL Nanopub][BEL Nanopub] is saved as assertion made by the user.
- We create a [BEL Document][BEL Document] (e.g. BEL Script) with one or more [BEL Nanopubs][BEL Nanopubs] encoded within. When we import the [BEL Document][BEL Document] into the [Nanopub Store][Nanopub Store], each [BEL Nanopub][BEL Nanopub] from the [BEL Document][BEL Document] is an assertion made by the user.

<a name="derived_bel_nanopubs"></a>
### Derived BEL Nanopubs

[BEL Nanopubs][BEL Nanopubs] that can be reasoned from other [BEL Nanopubs][BEL Nanopubs] are said to be *derived*. These derivations are associated to the original [BEL Nanopub][BEL Nanopub] with a description of the reasoning rules.

Example:

*Note*: The items here represent asserted and derived [BEL Nanopubs][BEL Nanopubs]. Here we only include the BEL statement for brevity.

Asserted
- `p(HGNC:TGFB1) increases deg(complex(SCOMP:"Nfkb Complex"))`
  - An increase of the *TGFB1* protein causes more of the *Nfkb Complex* complex to degrade.
- Derived
  - `deg(complex(SCOMP:"Nfkb Complex")) directlyDecreases complex(SCOMP:"Nfkb Complex")`
    - The degradation of the *Nfkb Complex* directly causes a decrease in the abundance of *Nfkb Complex*.
  - `complex(SCOMP:"Nfkb Complex") hasComponents (p(HGNC:NFKB1), p(HGNC:NFKB2), p(HGNC:REL), p(HGNC:RELA), p(HGNC:RELB), p(MGI:Nfkb1), p(MGI:Nfkb2), p(MGI:Rel), p(MGI:Rela), p(MGI:Relb), p(RGD:Nfkb1), p(RGD:Nfkb2), p(RGD:Rela))`
    - The *HGNC:NFKB1*, *HGNC:NFKB1*, *HGNC:REL*, *HGNC:RELA*, *HGNC:RELB*, *MGI:Nfkb1*, *MGI:Nfkb2*, *MGI:Rel*, *MGI:Rela*, *MGI:Relb*, *RGD:Nfkb1*, *RGD:Nfkb2*, and *RGD:Rela* proteins are components of the *Nfkb Complex* complex.

<a name="bkn"></a>
### BKN - BEL Knowledge Network

Pronounced like 'beacon', this is a nodes and edges BEL network built from assembling [Asserted BEL Nanopubs][Asserted BEL Nanopubs] and [Derived BEL Nanopubs][Derived BEL Nanopubs]. The [BEL Statement][BEL Statement] triple of `<Term> <Relationship> <Term>` is represented as an edge with nodes for each `<Term>`.

The nodes and edges of a *BKN* can be *Equivalenced* and *Orthologized*. Review [BEL RDF Model][BEL RDF Model] for a description of how equivalences are computed using the BEL RDF representation.

<a name="bel_document"></a>
### BEL Document
A file containing a collection of [BEL Nanopubs][BEL Nanopubs] with document metadata like Name, Description, and Version. The supported document formats are BEL script, XBEL, JSON, and RDF.

<a name="dataset"></a>
### Dataset
The representation of a [BEL Document][BEL Document] within the OpenBEL API. This provides access to document metadata as well as the collection of [BEL Nanopubs][BEL Nanopub] stored in the OpenBEL API that originate from the [BEL Document][BEL Document].

<a name="expression"></a>
### Expression
A string encoded in BEL that may represent a parameter (e.g. *AKT1*, *GO:"apoptotic process"*), term (e.g. *bp(GO:"apoptotic process")*), or statement (e.g. *p(HGNC:AKT1) increases bp(GO:"apoptotic process")*).

<a name="bel_nanopub_store"></a>
### BEL Nanopub Store
A database used to store [BEL Nanopubs][BEL Nanopubs]. It facilitates management of [BEL Nanopubs][BEL Nanopubs] and connection to other data sources.

[Gene Ontology]:           http://resource.belframework.org/belframework/20150611/namespace/go-biological-process.belns
[HGNC]:                    http://resource.belframework.org/belframework/20150611/namespace/hgnc-human-genes.belns
[nanopub.org]:             http://nanopub.org
[BEL Statement]:           #bel_statement
[Namespace]:               #namespace
[Annotation]:              #annotation
[BEL Nanopub]:             #bel_nanopub
[BEL Nanopubs]:            #bel_nanopub
[Asserted BEL Nanopubs]:   #asserted_nanopubs
[Derived BEL Nanopubs]:    #derived_nanopubs
[BEL Knowledge Network]:   #bkn
[BEL Document]:            #bel_document
[Dataset]:                 #dataset
[Expression]:              #expression
[Nanopub Store]:           #bel_nanopub_store
[BEL RDF Model]:           http://wiki.openbel.org/display/OBP/BEL+RDF+Model

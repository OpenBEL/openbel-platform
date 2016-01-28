# OpenBEL Platform

The OpenBEL Platform enables the building of computable BEL networks from a collection of managed BEL evidence.

### Table of Contents

- [What is provided?][What is provided?]
- [Terminology][Terminology]
- [Projects][Projects]
- [Roadmap][Roadmap]

<a name="what_is_provided"></a>
### What is provided?

- API of BEL tools
- Storage of BEL evidence
- Expansion of BEL knowledge through reasoning
- Build BEL networks from evidence

<a name="projects"></a>
### Projects

- [libbel](https://github.com/OpenBEL/libbel)
  - Low-level parser for BEL expressions and BEL Script format.

- [bel.rb](https://github.com/OpenBEL/bel.rb)
  - Library to provide tools for working with BEL Evidence.

- [openbel-api](https://github.com/OpenBEL/openbel-api)
  - Web-based API that enables storage of BEL evidence and construction of BEL networks.


<a name="roadmap"></a>
### Roadmap

*1.0.0, Milestone 1*

- Evidence store
- API to access annotations/namespaces
- API for completion of BEL expressions
- Standardization and expansion of BEL evidence
- Store and retrieve datasets of BEL Evidence (e.g. BEL Script documents)

*1.0.0, Milestone 2*

- Biological Expression Language, version 2.x support
- Knowledge graph reasoning (e.g. Gene activation pathways)
- Creation of BEL networks

[What is provided?]: #what_is_provided
[Terminology]:       ./terminology.md
[Projects]:          #projects
[Roadmap]:           #roadmap

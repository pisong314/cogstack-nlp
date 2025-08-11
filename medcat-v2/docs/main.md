# Medical  <img src="https://github.com/CogStack/cogstack-nlp/blob/main/media/cat-logo.png?raw=true" width=45>oncept Annotation Tool (v2)

**There's a number of breaking changes in MedCAT v2 compared to v1.**
Details are outlined [here](breaking_changes.md).

[![Build Status](https://github.com/CogStack/cogstack-nlp/actions/workflows/medcat-v2_main.yml)](https://github.com/CogStack/cogstack-nlp/actions/workflows/medcat-v2_main.yml)
[![Documentation Status](https://readthedocs.org/projects/cogstack-nlp/badge/?version=latest)](https://readthedocs.org/projects/cogstack-nlp/badge/?version=latest)
[![Latest release](https://img.shields.io/github/v/release/CogStack/cogstack-nlp?filter=medcat/*)](https://github.com/CogStack/cogstack-nlp/releases/latest)
[![pypi Version](https://img.shields.io/pypi/v/medcat.svg?style=flat-square&logo=pypi&logoColor=white)](https://pypi.org/project/medcat/)

MedCAT(*v2*) can be used to extract information from Electronic Health Records (EHRs) and link it to biomedical ontologies like SNOMED-CT and UMLS. Paper on [arXiv](https://arxiv.org/abs/2010.01165).

**Official Docs [here](https://cogstack-nlp.readthedocs.io/)**

**Discussion Forum [here](https://discourse.cogstack.org/)**

<!-- **Available Models (requires UMLS license) [here](https://uts.nlm.nih.gov/uts/login?service=https://medcat.rosalind.kcl.ac.uk/auth-callback)** -->

## News
- **MedCAT v2 beta** \[1. April 2025\] MedCATv2 beta 0.1.5 was released 1. April 2025.
- **Paper** [A New Public Corpus for Clinical Section Identification: MedSecId](https://aclanthology.org/2022.coling-1.326.pdf)
- **New Release** \[5. October 2022\]**: Logging changes, and various small updates. [Full changelog](https://github.com/CogStack/MedCAT/compare/v1.3.0...v1.4.0)
- **New Downloader \[15. March 2022\]**: You can now [download](https://uts.nlm.nih.gov/uts/login?service=https://medcat.rosalind.kcl.ac.uk/auth-callback) the latest SNOMED-CT and UMLS model packs via UMLS user authentication.
- **New Feature and Tutorial \[7. December 2021\]**: [Exploring Electronic Health Records with MedCAT and Neo4j](https://towardsdatascience.com/exploring-electronic-health-records-with-medcat-and-neo4j-f376c03d8eef)
- **New Minor Release \[20. October 2021\]** Introducing model packs, new faster multiprocessing for large datasets (100M+ documents) and improved MetaCAT.
- **New Release \[1. August 2021\]**: Upgraded MedCAT to use spaCy v3, new scispaCy models have to be downloaded - all old CDBs (compatble with MedCAT v1) will work without any changes.
- **New Feature and Tutorial \[8. July 2021\]**: [Integrating 🤗 Transformers with MedCAT for biomedical NER+L](https://towardsdatascience.com/integrating-transformers-with-medcat-for-biomedical-ner-l-8869c76762a)
- **General \[1. April 2021\]**: MedCAT is upgraded to v1, unforunately this introduces breaking changes with older models (MedCAT v0.4),
  as well as potential problems with all code that used the MedCAT package. MedCAT v0.4 is available on the legacy
  branch and will still be supported until 1. July 2021
  (with respect to potential bug fixes), after it will still be available but not updated anymore.

## Demo
A demo application is available [here](https://medcatv2.rosalind.kcl.ac.uk).

## Tutorials
Some guides on how to use MedCAT v2 are available at [MedCAT Tutorials](https://github.com/CogStack/cogstack-nlp/tree/main/medcat-v2-tutorials).

## Related Projects
- [MedCAT](https://github.com/CogStack/cogstack-nlp/blob/main/medcat-v2/) - the original version of MedCAT that this v2 is based one.
- [MedCATtrainer](https://github.com/CogStack/cogstack-nlp/tree/main/medcat-trainer/) - an interface for building, improving and customising a given Named Entity Recognition and Linking (NER+L) model (MedCAT) for biomedical domain text.
- [MedCATservice](https://github.com/CogStack/cogstack-nlp/blob/main/medcat-service/) - implements the MedCAT NLP application as a service behind a REST API.

## Install using PIP (Requires Python 3.9+)
Installation instructions are to follow upon a release of this version on PyPI.
Though installation is likely to be simply `pip install "medcat>=2.0"` at that time.
Currently the installation for the 2.0 beta release is simply:
```
pip install medcat~=2.0.0b
```
Though note the extras you might need (e.g `spacy`, `meta-cat`, `rel-cat`, `deid`).
If you need them, they need to be specified in brackets, e.g:
```
pip install medcat[spacy,meta-cat,rel-cat,deid]~=2.0.0b
```

2. Quickstart (MedCAT v2+):
```python
from medcat.cat import CAT

# Download the model_pack from the models section in the github repo.
cat = CAT.load_model_pack('<path to downloaded zip file>')

# Test it
text = "My simple document with kidney failure"
entities = cat.get_entities(text)
print(entities)

# To run unsupervised training over documents
data_iterator = <your iterator>
cat.train(data_iterator)
#Once done, save the whole model_pack 
cat.create_model_pack(<save path>)
```


## Models
### SNOMED-CT and UMLS
Access to v2 models is upcoming. They will initially (probably) be converted models from v1.
<!-- If you have access to UMLS or SNOMED-CT, you can download the pre-built CDB and Vocab for those databases by signing in and filling out [the online form](https://uts.nlm.nih.gov/uts/login?service=https://medcat.rosalind.kcl.ac.uk/auth-callback). This link first requires you to authenticate your ontology access via the NIH portal. -->

<!-- ### MedMentions
A basic trained model is made public. It contains ~ 35K concepts available in `MedMentions`. This was compiled from MedMentions and does not have any data from [NLM](https://www.nlm.nih.gov/research/umls/) as that data is not publicaly available.

Model packs:
- MedMentions with Status (Is Concept Affirmed or Negated/Hypothetical) [Download](https://cogstack-medcat-example-models.s3.eu-west-2.amazonaws.com/medcat-example-models/medmen_wstatus_2021_oct.zip)

Separate models:
- Vocabulary [Download](https://cogstack-medcat-example-models.s3.eu-west-2.amazonaws.com/medcat-example-models/vocab.dat) - Built from MedMentions
- CDB [Download](https://cogstack-medcat-example-models.s3.eu-west-2.amazonaws.com/medcat-example-models/cdb-medmen-v1.dat) - Built from MedMentions
- MetaCAT Status [Download](https://cogstack-medcat-example-models.s3.eu-west-2.amazonaws.com/medcat-example-models/mc_status.zip) - Built from a sample from MIMIC-III, detects is an annotation Affirmed (Positve) or Other (Negated or Hypothetical) -->

## Acknowledgements
Entity extraction was trained on [MedMentions](https://github.com/chanzuckerberg/MedMentions) In total it has ~ 35K entites from UMLS

The vocabulary was compiled from [Wiktionary](https://en.wiktionary.org/wiki/Wiktionary:Main_Page) In total ~ 800K unique words


## Powered By
A big thank you goes to [spaCy](https://spacy.io/) and [Hugging Face](https://huggingface.co/) - who made life a million times easier.

<!-- 
## Citation
```
@ARTICLE{Kraljevic2021-ln,
  title="Multi-domain clinical natural language processing with {MedCAT}: The Medical Concept Annotation Toolkit",
  author="Kraljevic, Zeljko and Searle, Thomas and Shek, Anthony and Roguski, Lukasz and Noor, Kawsar and Bean, Daniel and Mascio, Aurelie and Zhu, Leilei and Folarin, Amos A and Roberts, Angus and Bendayan, Rebecca and Richardson, Mark P and Stewart, Robert and Shah, Anoop D and Wong, Wai Keong and Ibrahim, Zina and Teo, James T and Dobson, Richard J B",
  journal="Artif. Intell. Med.",
  volume=117,
  pages="102083",
  month=jul,
  year=2021,
  issn="0933-3657",
  doi="10.1016/j.artmed.2021.102083"
}
``` -->

# Welcome to the IK-NLP Course! 🎉

These lab sessions are designed to help you follow along with the contents presented during the lectures, and introduce you to the skills and tools needed to complete the final projects.

## What to expect?

The lab sessions will be a mix of tutorials and exercises. The **tutorials** will present modern frameworks and tools to implement advanced NLP analyses and pipelines. The **exercises** are designed to teach you the skills needed for final projects. Here is a brief overview of the schedule:

| Week | Lecture topic    | Lab Tutorial                                                 | Lab Exercise | Assignments |
|------|------------------|--------------------------------------------------------------|--------------|-------------|
| 1 | Introduction to NLP | [Intro, Setup work environment and team creation](README.md) | -            | - Answer questionnaire |
| 2 | The Evolution of Language Modeling | [Intro to 🤗 Transformers and Datasets](notebooks/W2T_Intro_Transformers_Datasets.ipynb) | [🤗 Pipelines & Sentence Transformers for semantic search and QA](notebooks/W2E_Pipelines_Sentence_Transformers.ipynb) | - `[A]` Count FFNN parameters <br/> - `[E]` 1 and 2 (3 optional) |
| 3 | Looking for Words   | [Introduction to spaCy](notebooks/W3T_Intro_Spacy.ipynb)     | [Training a BPE tokenizer and a lexicon-based transduction model](notebooks/W3E_BPE_Transduction.ipynb) | - `[A]` Build Regexes <br/> - `[A]` SLP LM Exercises <br/> - `[E]` 1 (2 optional) |
| 4 | Labeling Sequences  | [Text tagging with spaCy and 🤗 Transformers](notebooks/W4T_Text_Tagging.ipynb) | [Non-textual information for NLP](notebooks/W4E_NonTextual_Information.ipynb) | - `[A]` Find wrong POS tags, most-frequent tagger<br/> - `[A]` calculate hmm-viterbi, viterbi complexity <br/> - `[E]` 1 (2 optional) |
| 5 | Trees of Words      | [Dependency parsing with spaCy](notebooks/W5T_Dependency_Parsing.ipynb) | - | - `[A]` parsing eval compute UAS/LAS <br/> - `[A]` transition parser steps, crossing arcs 
| 6 | Encode and Decode   | **Optional**: Training with 🤗 Transformers | - |
| 7 | Transfer Learning & Opening the Blackbox | -       | -       |

Some notes:

- The `[A]` tag in the Assignments column indicate a written assignment that you should complete. The `[E]` tag indicates an exercise in that week's exercise notebook that you should complete. All assignments and exercises that are not marked as optional are mandatory for the midterm portfolio.

- The core contents are covered in the first few weeks of the course to kickstart your work. Exercise sessions are dropped from week 5 onwards to allow you to focus on the final project.

- Participation to the lab sessions is **highly encouraged**, as they offer you a chance to ask questions related to the midterm portfolio and/or the final projects.

- The tutorial session for week 6 can be relevant to many projects and will be covered upon request.

## Tools and Frameworks

The lab sessions make use of the [Jupyter](https://jupyter.org/) environment. You can use the following links to get started:

- [Jupyter Notebook/Lab Installation](https://jupyter.org/install)
- [Jupyter Quickstart](https://docs.jupyter.org/en/latest/running.html)

Alternatively, it is possible to use the notebooks via the [Google Colab](https://colab.research.google.com/) web environment simply by clicking on the [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]() button at the beginning of each notebook. If you’re running on Windows, we recommend following along using a Colab notebook. If you’re using a Linux distribution or macOS, you can use either approach described here. For an intro to the Colab environment, refer to:

- [Colab Quickstart](https://colab.research.google.com/notebooks/intro.ipynb)

Since the lab session will introduce you to OSS libraries such as [spaCy](https://spacy.io/), [Scikit-learn](https://scikit-learn.org), [🤗 Transformers](https://huggingface.co/transformers/) and [🤗 Datasets](https://huggingface.co/docs/datasets/), most of the material is simply adapted from the official tutorials and docs. Here is a non-exhaustive list of the most relevant sources for additional reference:

- [Advanced NLP with spaCy](https://course.spacy.io/en)
- [spaCy Linguistic Features](https://spacy.io/usage/linguistic-features)
- [HuggingFace Course, Chapter 1](https://huggingface.co/course/chapter1/1)
- [HuggingFace Transformers Docs](https://huggingface.co/docs/transformers/index)
- [HuggingFace Datasets Docs](https://huggingface.co/docs/datasets/)
- [Scikit-learn "Working with Text Data" Tutorial](https://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html#tutorial-setup)
- [NLP class materials by Dirk Hovy](https://github.com/dirkhovy/NLPclass)

The file `requirements.txt` in this repository contains the list of all the packages required to run the lab sessions. You can create a Python virtual environment (Python>=3.6) and install them using the following command:

```shell
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Make sure the virtual environment is activated before running Jupyter. If you are using Colab, simply run the cell at the beginning of each notebook to install the required packages. Refer to [Using a Python Virtual Environment](https://huggingface.co/course/chapter0/1#using-a-python-virtual-environment) for more details on how to create and activate a virtual environment.

## About us

[**Arianna Bisazza**](https://www.cs.rug.nl/~bisazza/) is an Assistant Professor in Computational Linguistics and Natural Language Processing at the [Computational Linguistics Group](https://www.rug.nl/research/clcg/research/cl/) of the University of Groningen. She is passionate about the statistical modeling of languages, particularly in a multilingual context, and her long-term goal is to design robust NLP algorithms that can adapt to the large variety of linguistic phenomena observed around the world. She is part of the Dutch consortium [InDeep: Interpreting Deep Learning Models for Text and Sound](https://interpretingdl.github.io/), leading the work package on interpretability for neural machine translation.

[**Gabriele Sarti**](https://gsarti.com) is a doctoral researcher at the [Computational Linguistics Group](https://www.rug.nl/research/clcg/research/cl/) of the University of Groningen. He is part of the consortium [InDeep](https://interpretingdl.github.io/), working on interpretability for neural machine translation. His research focuses on interpretability for sequence-to-sequence NLP models, in particular from a user-centric perspective and by leveraging human behavioral signals.

[**Anjali Nair**](https://nl.linkedin.com/in/anjalinair012) is a MSc candidate in AI at the University of Groningen. *To be completed.*

## You see something wrong or missing?

Please open as issue here on Github! This is the first year we are using these contents for the course and although most of them come from battle-tested online tutorials, we are always looking for feedback and suggestions.

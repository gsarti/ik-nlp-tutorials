# Welcome to the IK-NLP Course! 🎉

These lab sessions are designed to help you follow along with the contents presented during the lectures, and introduce you to the skills and tools needed to complete the final projects.

## What to expect?

The lab sessions will be a mix of tutorials and exercises. The **tutorials** will present modern frameworks and tools to implement advanced NLP analyses and pipelines. The **exercises** are designed to teach you the skills needed for final projects. Here is a brief overview of the schedule:

| Week | Lab Tutorial                                                 | Lab Exercise |
|------|--------------------------------------------------------------|--------------|
| 1 | · [Intro, Setup work environment and team creation](README.md) <br/> · Start [Intro to 🤗 Transformers](notebooks/W2T_Intro_Transformers_Datasets.ipynb) | -            |
| 2 | [Intro to 🤗 Transformers and Datasets](notebooks/W2T_Intro_Transformers_Datasets.ipynb) | [🤗 Pipelines & Sentence Transformers for semantic search and QA](notebooks/W2E_Pipelines_Sentence_Transformers.ipynb) |
| 3 | [Linguistic analysis with spaCy and Stanza](notebooks/W3T_Analysis_Spacy_Stanza.ipynb)     | [Training a BPE tokenizer and a lexicon-based transduction model](notebooks/W3E_BPE_Transduction.ipynb) | 
| 4 | · Intro to the Peregrine cluster <br/> · Text tagging and dependency parsing with spaCy **TBD** | Combining Textual and Non-textual Features in NLP Models **TBD** |
| 5 | Natural Language Generation with 🤗 Transformers **TBD** | Exploring MT model saliency on the DivEMT corpus **TBD** |
| 6 | Fine-tuning and Efficient Modeling with 🤗 Transformers **TBD** | - |
| 7 | Final Project Progress Report | -       |

Some notes:

- The core contents are covered in the first few weeks of the course to kickstart your work. Exercise sessions are dropped from week 6 onwards to allow you to focus on the final project.

- The current notebooks for W4 and W5 are outdated and will be updated according to the schedule above.

- Participation to the lab sessions is **highly encouraged**, as they cover fundamental notions for the assignment portfolios and the final projects. Instructors will be available to answer questions and provide guidance.

## Tools and Frameworks

The lab sessions make use of the [Jupyter](https://jupyter.org/) environment. You can use the following links to get started:

- [Jupyter Notebook/Lab Installation](https://jupyter.org/install)
- [Jupyter Quickstart](https://docs.jupyter.org/en/latest/running.html)

Alternatively, it is possible to use the notebooks via the [Google Colab](https://colab.research.google.com/) web environment simply by clicking on the [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)]() button at the beginning of each notebook. If you’re running on Windows, we recommend following along using a Colab notebook. If you’re using a Linux distribution or macOS, you can use either approach described here. For an intro to the Colab environment, refer to:

- [Colab Quickstart](https://colab.research.google.com/notebooks/intro.ipynb)

Since the lab session will introduce you to OSS libraries such as [spaCy](https://spacy.io/), [Stanza](https://stanfordnlp.github.io/stanza/), [Scikit-learn](https://scikit-learn.org), [🤗 Transformers](https://huggingface.co/transformers/) and [🤗 Datasets](https://huggingface.co/docs/datasets/), most of the first few sessions' contents are adapted from official tutorials and docs. Here is a non-exhaustive list of the most relevant sources for additional reference:

- [Advanced NLP with spaCy](https://course.spacy.io/en)
- [Stanza tutorials](https://stanfordnlp.github.io/stanza/tutorials.html)
- [spaCy Linguistic Features](https://spacy.io/usage/linguistic-features)
- [HuggingFace Course, Chapter 1](https://huggingface.co/course/chapter1/1)
- [HuggingFace Transformers Docs](https://huggingface.co/docs/transformers/index)
- [HuggingFace Datasets Docs](https://huggingface.co/docs/datasets/)
- [Scikit-learn "Working with Text Data" Tutorial](https://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html#tutorial-setup)
- [NLP class materials by Dirk Hovy](https://github.com/dirkhovy/NLPclass)
- [HuggingFace "How to Generate" Tutorial](https://huggingface.co/blog/how-to-generate)
- [A Gentle Introduction to 8-bit Matrix Multiplication for transformers at scale using Hugging Face Transformers, Accelerate and bitsandbytes](https://huggingface.co/blog/hf-bitsandbytes-integration)
- [HuggingFace PEFT: Parameter-Efficient Fine-Tuning of Billion-Scale Models on Low-Resource Hardware](https://huggingface.co/blog/peft)

The file `requirements.txt` in this repository contains the list of all the packages required to run the lab sessions. You can create a Python virtual environment (Python>=3.6) and install them using the following command:

```shell
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Make sure the virtual environment is activated before running Jupyter. If you are using Colab, simply run the cell at the beginning of each notebook to install the required packages. Refer to [Using a Python Virtual Environment](https://huggingface.co/course/chapter0/1#using-a-python-virtual-environment) for more details on how to create and activate a virtual environment. Alternatively, you can use [Poetry](https://python-poetry.org/docs/) to manage the dependencies.

For any troubleshooting, please consult the [FAQ](FAQ.md) before asking for help. You are encouraged to contribute to it by adding your solutions!

## About us

<table>
  <tr>
    <td style="width:100px"><img src="http://www.cs.rug.nl/~bisazza/fig/arianna-2020.jpg" alt="Arianna Bisazza" style="width:800px"/></td>
      <td>
        <a href="https://www.cs.rug.nl/~bisazza/"><b>Arianna Bisazza</b></a> is an Assistant Professor in Computational Linguistics and Natural Language Processing at the <a href="https://www.rug.nl/research/clcg/research/cl/">Computational Linguistics Group</a> of the University of Groningen. She is passionate about the study of human languages, how they differ from each other, and how they can be modeled by computational tools. Her primary interest is in the development of language technologies supporting a large variety of languages around the world. She is also interested in the new knowledge about that computational models can reveal about the nature of language.
      </td>
  </tr>
  <tr>
    <td style="width:100px"><img src="https://gsarti.com/authors/gsarti/avatar_hu02574c73d8d5cf0c41465216db38be2a_239118_250x250_fill_q90_lanczos_center.jpg" alt="Gabriele Sarti" style="width:800px"/></td>
    <td>
      <a href="https://gsarti.com"><b>Gabriele Sarti</b></a> is a PhD student at the <a href="https://www.rug.nl/research/clcg/research/cl/">Computational Linguistics Group</a> of the University of Groningen. He is part of the Dutch consortium <a href="https://interpretingdl.github.io/">InDeep</a>, working on interpretability for language generation and neural machine translation. Previously, he was a research scientist at <a href="https://www.aindo.com/">Aindo</a> and a research intern at Amazon Translate NYC. His research interests involve interpretability for NLP, human-AI interaction and the usage of behavioral information like eye-tracking patterns to improve language understanding systems.
    </td>
  </tr>
<tr>
    <td style="width:100px"><img src="https://media.licdn.com/dms/image/C4D03AQHC30RRdIjJhQ/profile-displayphoto-shrink_400_400/0/1594219498972?e=1680739200&v=beta&t=4PdgVKwMUmzEIOFir7yHUfYWUJMRYETJYTEIFWGbRrQ" alt="Ludwig Sickert" style="width:800px"/></td>
    <td>
      <a href="https://www.linkedin.com/in/lsickert/"><b>Ludwig Sickert</b></a> is a MSc candidate in AI at the University of Groningen and a senior consultant in Cloud and AI technologies at IBM Netherlands. He attended the IK-NLP course in 2022 and is now working on interpreting formality in machine translation systems for his master thesis under the supervision of Gabriele and Arianna. He will serve as TA for the 2023 edition of the course.
    </td>
  </tr>
</table>

## You see something wrong or missing?

Please open as [issue](https://github.com/gsarti/ik-nlp-tutorials/issues) here on Github! This is the second year we are using these contents for the course and although most of them come from battle-tested online tutorials, we are always looking for feedback and suggestions.

## Alumni

**2022**

<table>
  <tr>
    <td><img src="https://avatars.githubusercontent.com/u/25927244?v=4" alt="Anjali Nair" style="width:150px"/></td>
    <td>
      <a href="https://nl.linkedin.com/in/anjalinair012"><b>Anjali Nair</b></a> is a MSc candidate in AI at the University of Groningen. She served as teaching assistant for the 2022 edition of the Natural Language Processing course.
    </td>
  </tr>
</table>

We thank our past students Georg Groenendaal, Robin van der Noord and Ayça Avcı for their contributions in spotting errors in the course materials.

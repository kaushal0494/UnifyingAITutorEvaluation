
# 🎓 Unifying AI Tutor Evaluation

## An Evaluation Taxonomy for Pedagogical Ability Assessment of LLM-Powered AI Tutors

<p align="center">

<a href="https://aclanthology.org/2025.naacl-long.57/">
<img src="https://img.shields.io/badge/Paper-ACL%20Anthology-red?style=for-the-badge">
</a>

<img src="https://img.shields.io/badge/NAACL-2025-blue?style=for-the-badge">
<img src="https://img.shields.io/badge/Award-SAC%20Award-gold?style=for-the-badge">
<img src="https://img.shields.io/badge/BEA%20Shared%20Task-2025-purple?style=for-the-badge">
<img src="https://img.shields.io/badge/IndoML-2025-green?style=for-the-badge">

<a href="https://creativecommons.org/licenses/by-sa/4.0/">
<img src="https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey?style=for-the-badge">
</a>

</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/kaushal0494/UnifyingAITutorEvaluation/main/Thumbnail.png" 
       width="750">
</p>

---

<h2 align="center">Authors</h2>

<p align="center">
  <a href="https://kaushal0494.github.io/">Kaushal Kumar Maurya</a> ·
  <a href="https://scholar.google.com/citations?user=cs5-j9EAAAAJ&hl=en&oi=ao">KV Aditya Srivatsa</a> ·
  <a href="https://scholar.google.com/citations?user=XsiLKJcAAAAJ&hl=en&oi=ao">Kseniia Petukhova</a> ·
  <a href="https://ekochmar.github.io/about/">Ekaterina Kochmar</a>
</p>

---

# 📌 Overview

This repository is the official implementation of:

> **Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessment of LLM-Powered AI Tutors** <br>
> 📍 Published at **NAACL 2025 (Long Paper)** <br>
> 🏆 Recipient of the **Senior Area Chair (SAC) Award**

📄 **Paper (ACL Anthology):**
[https://aclanthology.org/2025.naacl-long.57/](https://aclanthology.org/2025.naacl-long.57/)

## About



* Evaluates whether state-of-the-art LLMs are effective AI tutors and exhibit essential pedagogical abilities in educational dialogues.
* Proposes a unified taxonomy of eight pedagogical dimensions, grounded in learning science principles, to assess the quality of tutor responses to student mistakes in mathematics.
* Introduces MRBench, a benchmark comprising responses from seven state-of-the-art LLM-based and human tutors, with gold annotations across all eight dimensions.

## Evaluation Taxonomy (8 Dimensions)

1. **Mistake Identification**
2. **Mistake Location**
3. **Revealing of the Answer**
4. **Providing Guidance**
5. **Actionability**
6. **Coherence**
7. **Tutor Tone**
8. **Humanlikeness**

---
# 📊 MRBench Dataset

## 🔄 Versions

| Version                  | #Dialogues             | Dimensions | Description                                                                                                                       |
| ------------------------ | ----------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **MRBench_V1**           | 192     | 8          | Original dataset reported in NAACL 2025 paper                                                                                     |
| **MRBench_V2**           | 200      | 8          | Extended release with additional annotated examples                                                                               |
| **MRBench_V3** | 300 | 4         | Includes all previous versions, along with additional examples; annotations are provided for only four dimensions for the additional examples|

---

## ⚠ Important Note on MRBench_V3

The full taxonomy contains eight pedagogical dimensions. MRBench_V3 extends MRBench_V2 only with respect to the only **four** dimensions. This dataset has been used as a training set for the [BEA Shared Task 2025](https://sig-edu.org/sharedtask/2025) and [IndoML 2025](https://kaushal0494.github.io/datathon/). All resources related to these two shared tasks are available in the ```BEA_Shared_Task_2025_Datasets``` and ```IndoML_Datathon``` folders, respectively.

---

# 📂 Dataset Deatils

## Dataset Schema
Each example in MRBench follows the schema below:

```json
{
  "conversation_id": "Unique identifier",
  "conversation_history": "Tutor–student interaction context",
  "Data": "MathDial or Bridge",
  "Split": "train/test/validation",
  "Topic": "Mathematics topic",
  "Ground_Truth_Solution": "Reference solution (if available)",
  "anno_llm_responses": {
    "Model_Name": {
      "response": "Tutor response",
      "annotation": {
        "Mistake_Identification": "Yes/To some extent/No",
        "Mistake_Location": "Yes/To some extent/No",
        "Revealing_of_the_Answer": "Yes (correct)/Yes (incorrect)/No",
        "Providing_Guidance": "Yes/To some extent/No",
        "Actionability": "Yes/To some extent/No",
        "Coherence": "Yes/To some extent/No",
        "Tutor_Tone": "Encouraging/Neutral/Offensive",
        "Humanlikeness": "Yes/To some extent/No"
      }
    }
  }
}
```

## Field Descriptions

1. **conversation_id** – Unique identifier for each dialogue.
2. **conversation_history** – Contextual tutor–student interaction.
3. **Data** – Source dataset (MathDial or Bridge).
4. **Split** – Train, test, or validation split.
5. **Topic** – Mathematical topic or sub-topic.
6. **Ground_Truth_Solution** – Reference step-by-step solution (if available).
7. **anno_llm_responses** – Model responses with fine-grained pedagogical annotations.

---

## Sample Example

```json
{
  "conversation_id": "2895106109",
  "conversation_history": 
      "Tutor: What is the name of a 5-sided polygon?\n"
      "Student: a octogon",
  "Data": "Bridge",
  "Split": "train",
  "Topic": "4.5A.Geometric Lines",
  "Ground_Truth_Solution": "Not Available",
  "anno_llm_responses": {
    "GPT4": {
      "response": "Good try, but a five-sided polygon is actually called a pentagon. An octagon is an eight-sided polygon. Keep practicing, you're doing great!",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    }
  }
}
```

---

## Human Annotation Guideline Resources

To support transparency and reproducibility, we release:

* Training and testing annotation forms
* Detailed dimension-wise guidelines
* Definitions and illustrative examples
* FAQ documentation

All materials are available in ```Human_Annotation_Guidelines_Resources``` folder. 

# License

MRBench builds upon the [MathDial](https://github.com/eth-nlped/mathdial) and [Bridge Dataset](https://github.com/rosewang2008/bridge) datasets. Accordingly, MRBench is released under the **[Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) license](https://creativecommons.org/licenses/by-sa/4.0/)**, which requires users to provide proper attribution and to distribute any derivative works under the same license.

---

# BibTeX Citation

If you find our work or dataset useful, please cite:

```bibtex
@inproceedings{maurya-etal-2025-unifying,
    title = "Unifying {AI} Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessment of {LLM}-Powered {AI} Tutors",
    author = "Maurya, Kaushal Kumar  and
      Srivatsa, Kv Aditya  and
      Petukhova, Kseniia  and
      Kochmar, Ekaterina",
    editor = "Chiruzzo, Luis  and
      Ritter, Alan  and
      Wang, Lu",
    booktitle = "Proceedings of the 2025 Conference of the Nations of the Americas Chapter of the Association for Computational Linguistics: Human Language Technologies (Volume 1: Long Papers)",
    month = apr,
    year = "2025",
    address = "Albuquerque, New Mexico",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.naacl-long.57/",
    doi = "10.18653/v1/2025.naacl-long.57",
    pages = "1234--1251",
    ISBN = "979-8-89176-189-6",
    abstract = "In this paper, we investigate whether current state-of-the-art large language models (LLMs) are effective as AI tutors and whether they demonstrate pedagogical abilities necessary for good AI tutoring in educational dialogues. Previous efforts towards evaluation have beenlimited to subjective protocols and benchmarks. To bridge this gap, we propose a unified evaluation taxonomy with eight pedagogical dimensions based on key learning sciences principles, which is designed to assess the pedagogical value of LLM-powered AI tutor responses grounded in student mistakes or confusions in the mathematical domain. We release MRBench {--} a new evaluation benchmark containing 192 conversations and 1,596 responses from seven state-of-the-art LLM-based and human tutors, providing gold annotations for eight pedagogical dimensions. We assess reliability of the popular Prometheus2 and Llama-3.1-8B LLMs as evaluators and analyze each tutor{'}s pedagogical abilities, highlighting which LLMs are good tutors and which ones are more suitable as question-answering systems. We believe that the presented taxonomy, benchmark, and human-annotated labels will streamline the evaluation process and help track the progress in AI tutors' development."
}
```

---

# Contact

For inquiries, collaborations, or feedback:

**Kaushal Kumar Maurya**<br>
📧 [kaushalmaurya.iith@gmail.com](mailto:kaushalmaurya.iith@gmail.com)<br>
🌐 [Homepage](https://kaushal0494.github.io/)

---

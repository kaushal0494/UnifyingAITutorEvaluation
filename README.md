# **Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessment of LLM-Powered AI Tutors**
[Kaushal Kumar Maurya](https://kaushal0494.github.io/), [KV Aditya Srivatsa](https://scholar.google.com/citations?user=cs5-j9EAAAAJ&hl=en&oi=ao), [Kseniia Petukhova](https://scholar.google.com/citations?user=XsiLKJcAAAAJ&hl=en&oi=ao), and [Ekaterina Kochmar](https://ekochmar.github.io/about/)

---

## Overview
This repository serves as the official implementation hub for the paper (To be appear in NAACL 2025):

> *[Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessment of LLM-Powered AI Tutors.](https://arxiv.org/pdf/2412.09416)*

Our work presents a comprehensive evaluation taxonomy aimed at assessing the pedagogical abilities of large language model (LLM)-powered AI tutors. This repository will provide the community with the tools, data, and methodologies necessary to benchmark AI tutors effectively. 


---

## MRBench Dataset

### Version Update
- **MRBench_V1:** The original dataset with 192 dialogues as deatiled in the paper.  
- **MRBench_V2:** An updated version with additional 8 dialogues, bringing the total to 200 examples.

### File Structure

```json
{
  "conversation_id": "String: Unique identifier for the dialogue.",
  "conversation_history": "String: Partial conversation between the tutor and the student.",
  "Data": "String: Dataset name (e.g., MathDial or Bridge).",
  "Split": "String: Dataset split (e.g., test, train).",
  "Topic": "String: Topic category (e.g., sub topic in Math).",
  "Ground_Truth_Solution": "String: Step-by-step correct solution with explanation.",
  "anno_llm_responses": {
    "Model_Name": {
      "response": "String: Tutor's response to the student's answer.",
      "annotation": {
        "Mistake_Identification": "String: Has the tutor identified a mistake in the student’s response? (Yes/To some extent/No)",
        "Mistake_Location": "String: Does the tutor’s response accurately point to a genuine mistake and its location? (Yes/To some extent/No)",
        "Revealing_of_the_Answer": "String: Does the tutor reveal the final answer (whether correct or not)? (Yes (and the revealed answer is correct)/Yes (but the revealed answer is incorrect)/No)",
        "Providing_Guidance": "String: Does the tutor offer correct and relevant guidance, such as an explanation, elaboration, hint, examples, etc.? (Yes/To some extent/No)",
        "Actionability": "String: Is it clear from the tutor’s feedback what the student should do next? (Yes/To some extent/No)",
        "Coherence": "String: Is the tutor’s response logically consistent with the student’s previous response? (Yes/To some extent/No)",
        "Tutor_Tone": "String: Is the tutor’s response encouraging, neutral, or offensive? (Encouraging/Neutral/Offensive)",
        "Humanlikeness": "String: Does the tutor’s response sound natural rather than robotic or artificial? (Yes/To some extent/No)"
      }
    }
  }
}
```

### Notes
1. **`conversation_id`**: Serves as a unique identifier to track each dialogue in the dataset.  
2. **`conversation_history`**: Captures the dialogue context relevant to the ongoing interaction.  
3. **`Data`**: Specifies the dataset used for the interaction, such as MathDial or Bridge.  
4. **`Split`**: Indicates whether the data point belongs to the test, train, or validation set.  
5. **`Topic`**: Categorizes the dialogue into broad sub topics in Mathematics for easier filtering and analysis.  
6. **`Ground_Truth_Solution`**: Provides a step-by-step solution to the problem discussed in the conversation, serving as a gold standard for evaluation.  
7. **`anno_llm_responses`**: Stores LLM-specific responses with detailed annotations for evaluation based on multiple dimensions like mistake identification, guidance, etc.

### Sample Example
```json
{
  "conversation_id": "2895106109",
  "conversation_history": 
      "Tutor: What is the name of a 5-sided polygon? \n"
      "Student: a octogon"
  "data": "Bridge",
  "split": "train",
  "topic": "4.5A.Geometric Lines",
  "ground_truth_solution": "Not Available",
  "anno_llm_responses": {
    "Llama31405B": {
      "response": "That's close, but remember we just talked about a 5-sided polygon, and I think you might be thinking of an 8-sided polygon, which is an octagon, whereas a 5-sided polygon is actually called a pentagon.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    },
    "Mistral": {
      "response": "Remember, an octagon has 8 sides; a 5-sided polygon is called a pentagon.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Neutral"
      }
    },
    "GPT4": {
      "response": "Good try, but a five-sided polygon is actually called a pentagon. An octagon is an eight-sided polygon. Keep practicing, you're doing great!",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    },
    "Llama318B": {
      "response": "That's close, but the correct term for a 5-sided polygon is actually a pentagon.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "No",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Neutral"
      }
    },
    "Novice": {
      "response": "Try to recheck your answer.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "No",
        "Revealing_of_the_Answer": "No",
        "Providing_Guidance": "No",
        "Actionability": "No",
        "Humanlikeness": "No",
        "Coherence": "To some extent",
        "Tutor_Tone": "Neutral"
      }
    },
    "Phi3": {
      "response": "That was a good try! However, a five-sided polygon is called a pentagon, not an octagon which has eight sides. Let's review together!",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    },
    "Expert": {
      "response": "Great try! An octagon has 8 sides (I remember this by thinking about an octopus having 8 tentacles). The prefix for 5 is pent.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "No",
        "Providing_Guidance": "Yes",
        "Actionability": "To some extent",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    },
    "Sonnet": {
      "response": "Actually, an octagon has 8 sides, but you're on the right track thinking about polygons with multiple sides - can you remember the name for a shape with 5 sides?",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "No",
        "Providing_Guidance": "Yes",
        "Actionability": "Yes",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Neutral"
      }
    },
    "Gemini": {
      "response": "That's a great guess! Remember, an octagon has eight sides. A five-sided polygon is called a pentagon.",
      "annotation": {
        "Mistake_Identification": "Yes",
        "Mistake_Location": "Yes",
        "Revealing_of_the_Answer": "Yes (and the answer is correct)",
        "Providing_Guidance": "To some extent",
        "Actionability": "No",
        "Humanlikeness": "Yes",
        "Coherence": "Yes",
        "Tutor_Tone": "Encouraging"
      }
    }
  }
```

---

## BibTeX Citation
If you find our work useful, please cite us:

```bibtex
@article{maurya2024unifying,
  title={Unifying AI Tutor Evaluation: An Evaluation Taxonomy for Pedagogical Ability Assessment of LLM-Powered AI Tutors},
  author={Maurya, Kaushal Kumar and Srivatsa, KV and Petukhova, Kseniia and Kochmar, Ekaterina},
  conference
  journal={arXiv preprint arXiv:2412.09416},
  year={2024}
}
```

---

## Stay Updated
We are committed to fostering open science and will release all related resources here soon. Stay tuned for updates!

For inquiries or feedback, feel free to reach out via [Kaushal.Maurya@mbzuai.ac.ae](mailto:Kaushal.Maurya@mbzuai.ac.ae)

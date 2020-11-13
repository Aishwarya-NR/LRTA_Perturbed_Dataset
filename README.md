# LRTA_Perturbed_Dataset
This repository contains the perturbed datasets (val and testdev) presented in the paper- **LRTA: A Transparent Neural-Symbolic Reasoning Framework with Modular Supervision for Visual Question Answering (NeurIPS 2020)**\
The zip files contain masked (attribute and relationships) version of the GQA evaluation dataset. (https://cs.stanford.edu/people/dorarad/gqa/download.html). Mask term used is "XXXunknownXXX", the json structure remains the same as the original dataset with an extra field "question_orig" that denotes the original unmasked question.


# Format
- attribute_masked_data.zip
  - val_balanced_attribute_masked_questions.json
  - testdev_balanced_attribute_masked_questions.json
- vrb_prpn_masked_data.zip
  - val_balanced_vrb_prpn_masked_questions.json
  - testdev_balanced_vrb_prpn_masked_questions.json

# Example entry
### Image id: n411121.jpg
![Alt text](https://github.com/Aishwarya-NR/LRTA_Perturbed_Dataset/blob/main/n411121.jpg?raw=true "Title")

### Question json after masking
<pre>
'20903190': {
    "semantic": [
        {"operation": "select", "dependencies": [], "argument": "person (7)"},
        {"operation": "filter gender", "dependencies": [0], "argument": "female"},
        {"operation": "relate", "dependencies": [1], "argument": "train,near,s (-)"},
        {"operation": "exist", "dependencies": [2], "argument": "?"},
    ],
    "entailed": [],
    "equivalent": ["20903190"],
    "question": "Do you see a train near the XXXunknownXXX person?",
    "imageId": "n411121",
    "isBalanced": True,
    "groups": {"global": None, "local": "13-person_train"},
    "answer": "no",
    "semanticStr": "select: person (7)->filter gender: female [0]->relate: train,near,s (-) [1]->exist: ? [2]",
    "annotations": {
        "answer": {},
        "question": {"7:9": "7"},
        "fullAnswer": {"4": "6", "7": "7"},
    },
    "types": {"detailed": "existRelSC", "semantic": "rel", "structural": "verify"},
    "fullAnswer": "No, there is a van near the person.",
    "question_orig": "Do you see a train near the female person?",
}
</pre>

# Snippets from data generation code
The below snippets give a broad overview of the masking procedure used to generate the perturbed datasets, the question mentioned in the functions is a string containing the question text.
## Attribute masking
<pre>
#ATTRIBUTES is a list of attributes obtained from https://github.com/wenhuchen/Meta-Module-Network/blob/master/Constants.py
MASK_TOKEN = "XXXunknownXXX"

def mask_attributes(question):
  for word in question.split(" "):
    if word in ATTRIBUTES:
      masked_question = question.replace(word,MASK_TOKEN) 
  return masked_question        
</pre>

## Relationship masking
<pre>
MASK_TYPES = ('VERB', 'PROPN') #verbs and prepostions are masked to capture relationships
pos_tagger = spacy.load("en_core_web_sm") #spacy POS Tagger is used
MASK_TOKEN = "XXXunknownXXX"

def mask_relationship(question):
    tagged_dict = pos_tagger(question)
    masked_question = " ".join([ x.text if x.pos_ not in MASK_TYPES else MASK_TOKEN for x in tagged_dict])
  return masked_question        
</pre>


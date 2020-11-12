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
<pre>
'20644644': {
    "semantic": [
        {"operation": "select", "dependencies": [], "argument": "scene"},
        {"operation": "query", "dependencies": [0], "argument": "room"},
    ],
    "entailed": ["20644645", "20644643"],
    "equivalent": ["20644644"],
    "question": "Which room XXXunknownXXX it ?",
    "imageId": "n250821",
    "isBalanced": True,
    "groups": {"global": "room", "local": "02q-room"},
    "answer": "bedroom",
    "semanticStr": "select: scene->query: room [0]",
    "annotations": {"answer": {}, "question": {}, "fullAnswer": {}},
    "types": {"detailed": "place", "semantic": "global", "structural": "query"},
    "fullAnswer": "It is a bedroom.",
    "question_orig": "Which room is it?",
}
</pre>

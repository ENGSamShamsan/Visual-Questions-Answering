# Visual-Questions-Answering
The task  of  answering  basicquestions about images, such as ”What coloris the ball?” and ”How many cars are there?”

- Download the datasets to the current directory: 
Annotations (question types, etc.):
https://s3.amazonaws.com/cvmlp/vqa/mscoco/vqa/v2_Annotations_Train_mscoco.zip
https://s3.amazonaws.com/cvmlp/vqa/mscoco/vqa/v2_Annotations_Val_mscoco.zip
Questions:
https://s3.amazonaws.com/cvmlp/vqa/mscoco/vqa/v2_Questions_Train_mscoco.zip
https://s3.amazonaws.com/cvmlp/vqa/mscoco/vqa/v2_Questions_Val_mscoco.zip
https://s3.amazonaws.com/cvmlp/vqa/mscoco/vqa/v2_Questions_Test_mscoco.zip

First traing the model for detection the question type in train_VQA_clf.ipynb.


Second save the model to be used later to generate a response in the main file. 

The STT and TSS is an optional plug and play feature that you can integrate it into the system to serve the purpose of the end-to-end system.

Finally run main.ipynb, make sure to install all libraries needed. Run the model top to bottom to eventually get the proper answer generated.



Visual Question Answering

Raghav Chaudhary, Adam Fidler, Sam Shamsan

This visual question answering system parses a user input question into a corresponding question type, the topic of interest, and uses them in conjunction with features extracted from an input image to answer the question. The system consists of four major components:

Question-type classifier
Dependency parser
YOLO CNN (image recognition)
Question answering module
VQA Flow

Question-type Classification

The question-type classifier is a support vector machine with a stochastic gradient descent optimizer. The model was trained and scored on the questions and labels from the VQA Dataset (https://visualqa.org/download.html). Rather than training on the 65 specialized labels in the dataset, we opted to consolidate the question types into 5 generalized labels:

is there
what color
where
how many
other
These were sufficient for our purposes in developing a question answering system.

Topic Extraction

The topic extraction module uses stanza, a StanfordCoreNLP Python wrapper (https://stanfordnlp.github.io/stanza/), and inflector, a Python library to pluralize or singularize nouns (https://pypi.org/project/Inflector/), in order to determine the topic of an input question. After performing a dependency parse, if there is only a single noun is found in the sentence, then it is used as the topic. Otherwise, the noun most likely to be the topic has the nsubj tag, and is returned from the function. Any other nouns are added to a list, which is yet to be utilized in the current version.

The question type, the topic noun, and the list of other nouns are returned from from the extract_intention function as a respective tuple.

YOLO CNN

We use YOLO v4, introduced in the previous section, for object recognition and classification. The pretrained model comes with support for hundreds of images such as cars, people, etc. Using OpenCV for inference using the YOLO weights, we were able to extract object locationsnbounding boxes.

Weights file: https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights

Question Answering

Rather than training on the 65 specialized question-type labels from VQA, for our purposes we consolidated them into 5 generalized question types: "How many", "Is there', "What color", "Where", and "Other". In order to produce the response, we feed the output from the perivouse sub-systems into a functions to match the topic noun with the info dictionary.

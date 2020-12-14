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


Second save the model to be use it later to generate a response. 


The STT and TSS is an optional plug and play feature that you can integrate it into the system to serve the purpose of the end-to-end system.

Finally run main.ipynb, make sure to install all libraries needed. Run the model top to bottom to eventually get the proper answer generated.




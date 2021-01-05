[<img src='https://s3.amazonaws.com/drivendata-public-assets/logo-white-blue.png' width='600'>](https://www.drivendata.org/)
<br><br>

[<img src='https://drivendata-public-assets.s3.amazonaws.com/three-mean-memes.png' width='600'>](https://www.drivendata.org/)
<br><br>

# Hateful Memes

## Goal of the Competition

**Your goal is to create an algorithm that identifies multimodal hate speech in internet memes.**

Take an image, add some text: you've got a meme. Internet memes are often harmless and sometimes hilarious. However, by using certain types of images, text, or combinations of each of these *data modalities*, the seemingly non-hateful meme becomes a *multimodal type of hate speech*, a hateful meme.

At the massive scale of the internet, the task of detecting multimodal hate is both extremely important and particularly difficult. As the illustrative memes above show, relying on *just* text or *just* images to determine whether or not a meme is hateful is insufficient. **Your algorithm needs to be multimodal to excel at this task!**

The team at Facebook AI has decided to take the challenge head on—and they want your help! The team defines hate speech as:

  > A direct or indirect attack on people based on
   characteristics, including ethnicity, race, nationality, immigration status, religion, caste, sex, gender identity, sexual orientation, and disability or
   disease. We define attack as violent or dehumanizing (comparing people to non-human things,
   e.g. animals) speech, statements of inferiority,
   and calls for exclusion or segregation. Mocking
   hate crime is also considered hate speech.

This definition mirrors the [community standards on hate speech employed by Facebook](https://www.facebook.com/communitystandards/hate_speech), and is intended to provide an actionable classification label: if something is hate speech according to this definition, it should be taken down; if not, even if it is distasteful or objectionable, it is allowed to stay. 

[Starter code](https://github.com/facebookresearch/mmf/tree/master/projects/hateful_memes) from Facebook AI's MMF is also available on GitHub to help you get started.

This challenge provides an opportunity to help advance multimodal machine learning systems and push forward state-of-the-art performance on a novel data set.

**Note on Annotator Accuracy**

As is to be expected with a dataset of this size and nature, some of the examples in the training set have been misclassified. We are not claiming that our dataset labels are completely accurate, or even that all annotators would agree on a particular label. Misclassifications, although possible, should be very rare in the dev and seen test set, however, and we will take extra care with the unseen test set.

As a reminder, the annotations collected for this dataset were not collected using Facebook annotators and we did not employ Facebook’s hate speech policy. As such, the dataset labels do not in any way reflect Facebook’s official stance on this matter.

<center>
   <video controls height="400">
      <source src="https://s3.amazonaws.com/drivendata-public-assets/benign-confounder.mp4" type="video/mp4" >
</video>
<p>*Why detecting hateful memes requires a multimodal approach.*</p>
</center>

## What's in this Repository

This repository contains **links** to the code from winning competitors in the [Hateful Memes: Phase 2](https://www.drivendata.org/competitions/70/hateful-memes-phase-2/) DrivenData challenge. If you notice a problem with the link, please open an issue in this repository to let us know!

**Winning code for other DrivenData competitions is available in the [competition-winners repository](https://github.com/drivendataorg/competition-winners).**

## Winning Submissions

Place | Team or User | Code | Paper | Score | Summary of Model
----- | ------------ | --- | --- | ---   | ---
1     | alfred lab   | [link](https://github.com/HimariO/HatefulMemesChallenge) | [link](https://arxiv.org/abs/2012.08290) | 0.8450 | First using OCR and inpaint model to find and remove the text from the image. This will improve the quality of both object detection and web entity detection. Using the clean meme image to do bottom-up-attention feature extraction, web entity detection, human race detection. Those tags will give the transformer models much more diverse information to work with. Train the following models: extended VL-BERT, UNITER-ITM / VILLA-ITM, vanilla ERNIE-Vil. Average all predictions. Apply simple rule-base racism detection using meme text, race tag, entity tag, skin tone.
2     | Muennighoff  | [link](https://github.com/Muennighoff/vilio)  | [link](https://arxiv.org/abs/2012.07788) | 0.8310 | Since the problem at hand requires combining image & text input, it lends itself to the opportunity of applying the same NLP transformers to images. Yet since images contain far more information than words, it makes sense to pre-extract the most important content first via CNN’s such as FasterRCNN due to hardware limits. The transformer models I have implemented then take two different approaches of dealing with the extracted images and the text: (A) Run them through separate transformers and then combine them at the very end; A two-stream model. (B) Run them in parallel through the same, big, transformer; A one-stream model.
3     | HateDetectron| [link](https://github.com/rizavelioglu/hateful_memes-hate_detectron) | [link](https://arxiv.org/abs/2012.12975) | 0.8108 | The approach could be summed up as follows: Growing training set by finding similar datasets on the web, Extracting image features using object detection algorithms (Detectron), Fine-tuning a pre-trained V+L model (VisualBERT) Hyper-parameter search and applying Majority Voting Technique.
4     | kingsterdam | [link](https://github.com/Nithin-Holla/meme_challenge) | [link](https://arxiv.org/abs/2012.12871) | 0.8053 | We found that UNITER performed the best, which could perhaps be attributed to its diverse set of pre-training tasks. We decided to upsample these text confounders to give additional weight to these examples. Additionally, we added more weight to the hateful examples to combat the class imbalance. Furthermore, we performed cross-validation style training for better generalizability of the model. The final prediction was obtained as a weighted ensemble where the ensemble weights were optimized using an evolutionary algorithm (EA) on the development set predictions.
5     | burebista   | [link](https://github.com/vladsandulescu/hatefulmemes) | [link](https://arxiv.org/abs/2012.13235) | 0.7943 | I adapted a couple of multimodal pretrained architectures and did simple ensembling to smooth out the predictions. I also tried LXMERT and VLP, because I wanted to see how the architectures and pre-training procedures impacted the finetuning for a downstream task.

Additional solution details can be found in each winner's repository.

**Benchmark Blog Post: ["Hateful Memes - Benchmark"](https://www.drivendata.co/blog/hateful-memes-benchmark/)**
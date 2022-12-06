## Video-Based Person Re-Identification

### Project Description:

The goal of this project is to implement a video-based Person Re-Identification algorithm on a single camera. We assess and select existing publicly-available algorithms [here](https://paperswithcode.com/task/video-based-person-re-identification) and identify their relevance (if any) for this case.

The algorithm selected is GitHub user [deropty's PiT model](https://github.com/deropty/PiT). Instructions to implement the algorithm can be found on the GitHub.

### Datasets Summary:

Dataset | MARS | DukeMTMC | iLIDS | Airport 
--- | --- | --- | --- |--- 
ids | 1261 | 2700 | 300 | 9651 
images | - | 2000000 | - | 39902
tracklets | 20478 | - | 600 | -
bboxes | 1191003 | - | 43800 | -
distractors | 3248 | 0 | 0 | 0
cameras_num | 6 | 8 | 2 | 6

**Simple Comparison:**
Dataset | MARS | DukeMTMC | iLIDS | Airport 
--- | --- | --- | --- |--- 
Sample Size | ✓✓ | ✓✓ | ✓ | ✓✓✓
Image Variations | ✓✓ | ✓✓✓ | ✓ | ✓✓
Image Quality | ✓✓ | ✓✓ | ✓ | ✓
Raw | - | ✓ | ✓ | ✓

**Training Dataset Selection**

To create a robust model, we seek to train the algorithm with a dataset that is **large** and one consisting of **images or frames with similar quality** (pixels) as its intended use case.
- Image quality
  - Based on the previews, the iLIDS-VID and Airport dataset seem to consist blurrer images.
  - If the quality of the videos or images we are trying to re-identify people are of similar image quality, training the algorithm with the aforementioned dataset would be adequate.
- Size of dataset 
  - Although 'Airport' is the largest dataset, it has the least number of independent studies and exposure which does not inspire the most confidence in the data's integrity.
  - The DukeMTMC dataset is the second largest dataset. However, it has since been retracted due to external factors, thus we refrain from using it as well.
  - The **MARS dataset** is relatively big and widely used in numerous papers & studies, and it seems to be the most appropriate dataset so far.
  - The iLIDs dataset only consists of 300 unique individuals and may be too small to create a robust model due to underfitting.

### Algorithm Selection:

**Top publicly-available models (MARS) comparison**:
1. B-BOT + OSM + CL Centers*
  - Although this model achieved a higher rank on the metric mean Average Precision (mAP) for the MARS dataset, it's rank varied more across other metrics which does not reflect consistency.
  - It obtained rank 1 in another dataset PRID2011 as well, but extra training data was used which likely provided it with an advantage.
2. PiT
  - The PiT model score rank 1 for 6 metrics between MARS and iLIDS-VID dataset and rank 3 for the remaining 2 metrics which makes it the most ideal model.
3. mgh
  - The mgh model was only tested on the MARS dataset and achieved admirable top 5 ranks in 4 different metrics.
4. PSTA
  - The PSTA model ranked 1 on mAP for the DukeMTMC dataset, 2nd for a metric in iLIDS-VID, and ranked 5th on the MARS dataset for the mAP metric.

**Selection Criteria**:
- Applicability:
  - Since the application is undefined, we seek to implement a flexible model that performs well in as many situations as possible.
    - To achieve this, the model should return a respectable score with the iLIDs dataset as there may be cases where the model has to be retrained with new data and we have some level of assurance that it can perform well with small datasets
- Feasibility:
  - With access to only a local terminal to test the model, a large and complex dataset may prove to be unfeasible to train and test.
- Model Accuracy:
  - The selected model ideally will perform well with different datasets as it will increase the likelihood of it performing well in new unseen data.
  - The model PiT obtained the highest scores for 4 metrics with the iLIDS-VID dataset and top 3 for 4 metrics with the MARS dataset

**Conclusion**
All things considered, the PiT model is most appropriate for our use case and is selected as the ideal video-based person reidentification algorithm for the following reasons:
  1. Consistent when tested with different datasets & metrics
  2. File is somewhat large for a local terminal but is manageable
  3. Image quality of the dataset (MARS) it performed well on seems to be closest to a typical image produced by a typical camera used today

### Model Evaluation:

Given the focus of projects on security and retail, we test the model on a video with a shoplifting occurence to see if we can re-identify individuals captured by different cameras in a gas station. 

>> insert result observations here

- If the model did not perform up to standard, there are some possible solutions
  1. Provide a more exhaustive dataset
    - Larger sample size
  2. Provide a more relevant dataset
    - Images or frames closer to the test images/videos or future input
    - If unavailable, take some samples and personally annotate them
  3. Identify any reasons that may impact the algorithm
    - Eg. location where test or input images/frames are taken may be poorly lit resulting in the algorithm's inability to generate ideal results


### Acknowledgement:
- This repository is cloned from the repository [PiT](https://github.com/deropty/PiT).
- This repository is built upon the repository [TranReID](https://github.com/damo-cv/TransReID).
- The test video was retrieved from the Youtube channel [Gas Station Encounters](https://youtu.be/LamLq3dlqyI).

### Citation:
@ARTICLE{9714137,
  author={Zang, Xianghao and Li, Ge and Gao, Wei},
  journal={IEEE Transactions on Industrial Informatics}, 
  title={Multidirection and Multiscale Pyramid in Transformer for Video-Based Pedestrian Retrieval}, 
  year={2022},
  volume={18},
  number={12},
  pages={8776-8785},
  doi={10.1109/TII.2022.3151766}
}

### Project Status:
- Pending availability of training dataset
## Project: Perception Pick & Place

---

[//]: # (Image References)

[image1]: ./pics/noise.png
[image2]: ./pics/denoise.png
[image3]: ./pics/table.png
[image4]: ./pics/object.png
[image5]: ./pics/clustering.png
[image6]: ./pics/matrix_1.png
[image7]: ./pics/Label_test_1.png
[image8]: ./pics/matrix_2.png
[image9]: ./pics/Label_test_2.png
[image10]: ./pics/matrix_3.png
[image11]: ./pics/Label_test_3.png

## [Rubric](https://review.udacity.com/#!/rubrics/1067/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Exercise 1, 2 and 3 pipeline implemented
In this part, I will show the pipeline in test1.world environment. The pipeline is implemented in project_template.py.
#### 1. Complete Exercise 1 steps. Pipeline for filtering and RANSAC plane fitting implemented.
The original point cloud contains cetain amount of noise as figure below

![alt text][image1]

Firstly, a voxel downsampling filter is used to recude the number of data point (line 57 to line 69 in project_template.py). Then a passthrough filter is used to extract the point cloud of table and objects (line 71 to line 94 in project_template.py). A statistical outlier filter is applied to filter out the noise (line 96 to line 112 in project_template.py), finally the denoised point cloud is shown below

![alt text][image2]

Applying the RANSAC plane fitting algorithm gives us the separate point cloud of table and object as figures below (line 114 to line 133 in project_template.py)

![alt text][image3]
![alt text][image4]

#### 2. Complete Exercise 2 steps: Pipeline including clustering for segmentation implemented.  
The Euclidean clustering algorithm is used for obejct clustering (line 135 to line 166 in project_template.py), and the clustered objects are shown in figure below

![alt text][image5]

#### 2. Complete Exercise 3 Steps.  Features extracted and SVM trained.  Object recognition implemented.
compute_color_histograms() and compute_normal_histograms() functions in features.py have been filled out to generate the object's feature. For each object, 20 training datas are collected. SVM with linear kernel is used to train the model and the normalized confusion matrix is shown below

![alt text][image6]

The trained model is used to classify different objects in the scene (line 180 to line 220 in project_template.py), and the final object recognition for test1.world is shown in figure below and 3/3 objects are successfully identified. 

![alt text][image7]

### Pick and Place Setup

#### 1. For all three tabletop setups (`test*.world`), perform object recognition, then read in respective pick list (`pick_list_*.yaml`). Next construct the messages that would comprise a valid `PickPlace` request output them to `.yaml` format.

For test1.world environment, the object recgonition result is shown in previous section. 

For test2.world, the normalized confusion matrix of SVM model and the final object recognition are shown below. 5/5 objects are successfully identified.

![alt text][image8]
![alt text][image9]

For test3.world, the normalized confusion matrix of SVM model and the final object recognition are shown below. 7/8 objects are successfully identified. In this case, the biscuits is mistakenly identified as soap.

![alt text][image10]
![alt text][image11]

All the output*.yaml files are included in the project.

In this project, I basically use the various filters introduced in class to extract the object clusters. By tuning the parameters, the objects in all three environment can be clustered successfully. But for test3.world, not all the objects are correctly identified. Thus, for a complex world like test3.world, I need to further improve the learning model by collecting more data, or tuning the learning hyperparameters, or enginneering other relevant feartures or trying other learning model. 

In current project_template.py, I commented out the part of 'pick_place_routine' service. I need to add the collision avoidance function and finally make the PR2 robot to successfully pick up the identified object. 




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
[image8]: ./pics/Label_test_2.png
[image9]: ./pics/Label_test_3.png

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
compute_color_histograms() and compute_normal_histograms() functions in features.py have been filled out to generate the object's feature. For each object, 20 training datas are collected. SVM is used to train the model and the normalized confusion matrix is shown below

![demo-1](https://user-images.githubusercontent.com/20687560/28748231-46b5b912-7467-11e7-8778-3095172b7b19.png)




Here's | A | Snappy | Table
--- | --- | --- | ---
1 | `highlight` | **bold** | 7.41
2 | a | b | c
3 | *italic* | text | 403
4 | 2 | 3 | abcd


### Pick and Place Setup

#### 1. For all three tabletop setups (`test*.world`), perform object recognition, then read in respective pick list (`pick_list_*.yaml`). Next construct the messages that would comprise a valid `PickPlace` request output them to `.yaml` format.

And here's another image! 
![demo-2](https://user-images.githubusercontent.com/20687560/28748286-9f65680e-7468-11e7-83dc-f1a32380b89c.png)

Spend some time at the end to discuss your code, what techniques you used, what worked and why, where the implementation might fail and how you might improve it if you were going to pursue this project further.  




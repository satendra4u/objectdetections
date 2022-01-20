# object detections faster RCNN - inception_resnet model:

Faster R-CNN is a deep convolutional network used for object detection, that appears to the user as a single, end-to-end, unified network.
The Object detection model is using faster RCNN and based on **inception_resnet model** which is improvised by tensorflow team and it is pre-trained with millions of images.The network can accurately and quickly predict the locations of different objects

This model reads any image as an input and then download and resize it before sending to the inception_resnet model . Once it is sent it to the model thousands of regions proposal (2000)  have been generated using selective search algorithm inside the image. A new layer called ROI Pooling that extracts equal-length feature vectors from all proposals (i.e. ROIs) in the same image.

**Based on the inception_resnet model I have developed an alogorithm which takes input as an image and gives you the objects' region in box inside images and predicts / classify various objects inside the image.
**

I have simplified the algorithm so that any developer can run it by using tensor flow env and tensorflow_hub. It is pretty simple code with few functions mentioned below.

The code is in github repo:


-- Take input as an image
def detect_img(image_url):

-- function to convert the image into numpy multi-dimensiona arry and call the detector function to define region proposal
def run_detector(detector, path):

--functions to draw the boxes on images to show the % match of the region inside the image with classification defined by CNN model.
def draw_boxes(image, boxes, class_names, scores, max_boxes=10, min_score=0.1): - 

--functions to drawing the region boxes and labeling as proposed objects region
def draw_bounding_box_on_image(image,ymin,xmin,ymax, xmax,color,font, thickness=4, display_str_list=()):

![image](https://user-images.githubusercontent.com/2432102/150046416-612d0802-2ebc-4291-8751-92746aa73eec.png)


**Fast RCNN concepts:**

The feature map from the last convolutional layer is fed to an ROI Pooling layer. The reason is to extract a fixed-length feature vector from each region proposal. The GIF below shows how the ROI Pooling layer works.



![image](https://user-images.githubusercontent.com/2432102/150331485-c298e1b5-9f9d-4f38-81e6-329c01fbefb7.png)


Simply put, the ROI Pooling layer works by splitting each region proposal into a grid of cells. The max pooling operation is applied to each cell in the grid to return a single value. All values from all cells represent the feature vector. If the grid size is 2×2, then the feature vector length is 4.

Below are the steps which demonstarte how the ROI pooling layer works in the fast RCNN :

![image](https://user-images.githubusercontent.com/2432102/150331554-2fbf89a6-370c-478d-b828-d4cfeeeb0429.png)
-------------------------------------------------------------------------------------------------------------------
![Snip20220120_21](https://user-images.githubusercontent.com/2432102/150337295-fa21c98b-8f30-424e-8f25-394d7b0b02cf.png)
-------------------------------------------------------------------------------------------------------------------
![Snip20220120_22](https://user-images.githubusercontent.com/2432102/150337309-bc0af853-a863-484a-8202-efa8f538d22d.png)
-------------------------------------------------------------------------------------------------------------------
![Snip20220120_24](https://user-images.githubusercontent.com/2432102/150337324-a93058cc-d56a-4116-851c-d5ab9ffc35e2.png)
------------------------------------------------------OutPut-------------------------------------------------------------
![Snip20220120_25](https://user-images.githubusercontent.com/2432102/150337337-d60f6a73-38b1-450a-8c37-57c1952b37bb.png)



Lets talk about RPN which is the main differentiating factor between Fast RCNN and Faster RCNN model, in fast RCNN or RCNN model the biggest challange was to come up regions proposals faster and pass on to connected layer to define the feature vectors and then pass on to CNN to classify those regions. To come up with the faster approach for region proposals. Below is one of the faster approach: 

Proposing region proposal network (RPN) which is a fully convolutional network that generates proposals with various scales and aspect ratios. The RPN implements the terminology of neural network with attention to tell the object detection (Fast R-CNN) where to look.

Rather than using pyramids of images (i.e. multiple instances of the image but at different scales) or pyramids of filters (i.e. multiple filters with different sizes), there is a concept of anchor boxes. An anchor box is a reference box of a specific scale and aspect ratio. With multiple reference anchor boxes, then multiple scales and aspect ratios exist for the single region. This can be thought of as a pyramid of reference anchor boxes. Each region is then mapped to each reference anchor box, and thus detecting objects at different scales and aspect ratios.

The convolutional computations are shared across the RPN and the Fast R-CNN. This reduces the computational time.

The architecture of Faster R-CNN is shown in the next figure. It consists of 2 modules:

**RPN: For generating region proposals.
Fast R-CNN: For detecting objects in the proposed regions.**

The RPN module is responsible for generating region proposals. It applies the concept of attention in neural networks, so it guides the Fast R-CNN detection module to where to look for objects in the image.


![image](https://user-images.githubusercontent.com/2432102/150366250-3a2f44f6-aaf1-4fad-b705-6337d03d6b65.png)



Q1. Describe what would be the best instance segmentation model to get the highest precision. Explain why do you think it will be the best performing model.

Ans. I have read about three instance segmentation model.
FCIS
Mask-RCNN
Yolact
Yolact++

I have used Mask-RCNN and Yolact for my projects.

**We can also look into the benchmark **
![1](https://user-images.githubusercontent.com/60669591/132464568-d78a696e-6164-4a2c-b56f-630e2712e6fb.png)


For me Yolact is the best instance segmentation model because it is a single stage detector extension which performs instance segmentation by breaking into subtasks , they forgo explicitly the localisation step.

The network learns to localise masks on its own where visually , spatially and semantically similar instances appear in the prototypes .The number of prototype masks in YOLACT is independent of the number of categories ,this leads to distributed representation in the prototype space , this behaviour leads to following advantages

Some prototype spatially partition the image
Some localize the instances
Some detect instance contours
Some encode position-sensitive directional maps
Some do the combo of the above operations

They have many practical advantages with this approach which are mentioned below

Lightweight assembly process due to parallel structure
Marginal amount of computational overhead to one-stage detectors like ResNet101[5]
Masks quality are high
Generic concept of adding of generating prototypes and mask coefficients
which could be added to almost any modern object detector

**For large objects, the quality of the masks is even better than those of two-stage detectors.**
![2](https://user-images.githubusercontent.com/60669591/132464656-10c343ab-3e90-4449-abf2-db1a0b58f1fc.png)


Q.2 List some possible challenges if implementing such model into production. For this question, assume that you will have enough images for training the model.

**Challenges:**

**Localization Failure :** If there are too many objects in one spot in a scene, the network can fail to localize each object in its own prototype. In these cases, the network will output something closer to a foreground mask than an instance segmentation for some objects in the group.
Suppose we are capturing field images with low resolution(10 meter resolution) and some fields will be small in that region. With 10 meter resolution area of small fields in image would we small. If there are multiple small fields align to each other. Mask of our model going to overlap on each other.

![000000100005](https://user-images.githubusercontent.com/60669591/132453437-d790fc16-02de-4d19-8fd6-f6cfe55addf2.png)
![000000100006](https://user-images.githubusercontent.com/60669591/132453444-c38940fb-f1ce-4d9b-914f-7ab73fc7b2cf.png)


**Leakage :** The network leverages the fact that masks are cropped after assembly, and makes no attempt to suppress noise outside of the cropped region. This works fine when the bounding box is accurate, but when it is not, that noise can creep into the instance mask, creating some “leakage” from outside the cropped region. This can also happen when two instances are far away from each other, because the network has learned that it doesn’t need to localize far away instances the cropping will take care of it.

Experiment with an instance segmentation model using the images provided (you can do image augmentation) and explain the results. It can be any model (you can re-use anything you have done previously or clone any repo of your choice and use it); it does not need to be the model described in 1). We are not testing precision only; we are going to evaluate how you solve open challenges.


![000000100005_bbox](https://user-images.githubusercontent.com/60669591/132453370-141e2d7d-bdd6-4a13-afcb-a6b9f785cfaf.png)
![000000100006_bbox](https://user-images.githubusercontent.com/60669591/132453381-5a2ee2ef-dab9-420d-a09d-10fbd3c12312.png)


![000000100005](https://user-images.githubusercontent.com/60669591/132453437-d790fc16-02de-4d19-8fd6-f6cfe55addf2.png)
![000000100006](https://user-images.githubusercontent.com/60669591/132453444-c38940fb-f1ce-4d9b-914f-7ab73fc7b2cf.png)


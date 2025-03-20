Description
Landmarks and historical sites are some of the most frequently photographed places on Earth. Yet, each shot has a slightly different angle and shadows vary on times of day or year.
One photo could be taken from the ground, another up some steps, and a third from a drone. Matching many images across different viewpoints is a fundamental Computer Vision problem that
is far from solved. Factors like surface texture or surroundings can cause an otherwise well-performing algorithm to degrade.

The process of reconstructing a 3D model of an environment from a collection of images is called Structure from Motion (SfM). These images are often captured by trained operators or with additional sensor data. 
This ensures homogeneous, high-quality data. It’s much more difficult to build 3D models from assorted images, the real-world examples we’ve put together for this competition. 
In fact, we’ve designated 6 categories, each with its distinct challenge:

Phototourism and historical preservation: different viewpoints, sensor types, time of day/year, and occlusions. Ancient historical sites add a unique set of challenges

Night vs day and temporal changes: combination of day and night photographs, including poor lighting, or photographs taken months or years apart, in different weather

Aerial and mixed aerial-ground: images from drones, featuring arbitrary in-plane rotations, matched against similar images and also images taken from the ground

Repeated structures: symmetrical objects require details to disambiguate perspective

Natural environments: highly non-regular structures such as trees and foliage

Transparencies and reflections: objects like glassware are lacking in texture and create reflections and specularities which pose a different set of problems

Your efforts could contribute to a better understanding of this fundamental problem in Computer Vision. We hope to encourage knowledge sharing between traditional 
image-matching techniques and cutting-edge machine learning by including many categories.

Evaluation
Submissions are evaluated on the mean Average Accuracy (mAA) of the registered camera centers C=−RTT
. Given the set of cameras of a scene, parameterized by their rotation matrices R
 and translation vectors T
, and the hidden ground truth, we compute the best similarity transformation T
 (i.e. scale, rotation and translation altogether) that is able to register onto the ground-truth the highest number of cameras starting from triplets of corresponding camera centers.

A camera is registered if ||Cg−T(C)||<t
, where Cg
 is the ground-truth camera center corresponding to C
 and t
 is a given threshold. Using a RANSAC-like approach, all the possible (N3)
 feasible similarity transformations T′
 that can be derived by the Horn's method on triplets of corresponding camera centers (C,Cg)
 are verified exhaustively, where N
 is the number of cameras in the scene. Each transformation T′
 is further refined into T′′
 by registering again the camera centers by the Horn's method, but including at this time the previous registered cameras together with the initial triplets. The best model T
 among all T′′
 with the highest number of registered cameras is finally returned.

Assuming that ri
 is the percentage of the cameras in a scene, excluding the original camera center triplets, successfully registered by Ti
 setting a threshold ti
, the mAA for that scene is computed by averaging ri
 among several thresholds ti
. The thresholds ti
 employed range from roughly 1 cm to 1 m according to the kind of scene. The final score is obtained by averaging the mAA among all the scenes in the dataset.

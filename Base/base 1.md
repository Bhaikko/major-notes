# Base 1
## Abstract
The architecture is based on a stack of hourglass modules trained 
on a large dataset of 3D rigged characters
It operates on volumetric representation of the inpupt 3D shapes
augmented with geometric shape features that provide additional cues
for joint and bone locations

## Intro
Method learns a generic model of skeleton prediction for 3D models
Method does not require input textual description of joins,
nor requires prior knowledge of the input shape category.

Architecture based on stack of hourglass modules trained on large dataset of 3D rigged character mined from web.
It operates on volumetric representation of input 3D shades augmented with geometric shape features that provide additional cues for joint and bone locations.
Deep learning approach to predict animation skeletons of 3D models representing articulated characters.
Learns a generic method of skeleton prediction for 3D models

### IRRELEVANT NOW
### Related Work 
* Geometric Skeletons: Most deep learning approaches treat the skele-
ton extraction problem as a binary classification problem
where the goal is to detect pixels that lie close to the medial
axis of the object in the image (2D). Same work in case of 3D by extracting skeleton from medial surfaces in case of 3D. 
Extracts animation skeletons rather than geometric ones

**Many references to Deep architectures for extraction of skeleton in Section 2. 3D pose estimation.**

Recovery of underlying connectivity of the animation skeleton through minimum spanning tree algorithm driven by neural network.

Doesnt need a predefined template, shape class information or specific set of target joints

### Overview ###
Since joint and bone predictions are not independent of each other,
our method simultaneously learns to extract both through a shared
stack of encoder-decoder module

#### Input representation
Voxelizing the 3D model loses surface detail. Hence implicit shape representation, SDF is used as input to volumetric network.
Additional geometric cues: Surface curvature (2), shape diameter and mesh vertex density also calculated.
Combination of above cues with SDF provided best accuracy

Input representation show in Architecture image. Fig 3

* Input shape representation: polygon mesh soup converted into implicit representation can be processed by deep networks.
* Volumetric network is used for the task. 
* Signed distance function(SDF) extracted through a fast marching method  used as input. Additional input in form of surface curvature(2), shape diameter and mesh vertex density were used. Reason given in the section itself. 
* Also takes input controlling desired LOD for output
* Cross Category generalization

For each model in the dataset, the signed distance function is applied to the mesh to convert the voxel representation to a volumetric representation. 
Local vertex density is a Gaussian heatmap
that identifies key landmarks on the mesh with a high density of vertices.
Principal surface curvatures indicate the rate of change in the direction of the normals at any point on the mesh’s surface.
Local shape diameter provides a link from the surface of the mesh to its volume through the medial axis transform and helps identify
mesh partitions through segmentation 


### Architecture ###
* input3d model -> voxelized volumetric grid -> discretized implicit surface(SDF) with geometric features. 
* the resulting representation processed through a deep network that outputs bone and join prob.
* the final stage extracts the animation skeleton based on the predicted probabilites

Xu hourglass differ by two ways to Newell 2016
* user controlled granularity param is provided when encoder has finished contextualizing
* separate output prediction block responsible for producing bone heatmaps. 

input consist of five channels:
SDF, two principal curvatures, local shape diameter and vertex density. Hence 88 x 88 x 88 x 5.
The learning process then weighs the input channels depending on the input accordingly

Guassian kernel used for vertex density for smoothing

Hourglass module: input processed through 3D hourflass network variant. The variant processes the input shape through a volumetric convolutional layer and a residual block whose goal is to learn combination of different input features.

LOD: [0, 1] - 0 corresponding the most fine grained. (Refer to architecture diagram for its usage). User defined parameter mentioned min paper. Default value: 0.02. A map of 11x11x11x4 is attached after encoder changes input from 88^3 to 11^3

Output of Model: 88x88x88x8 map same as input whose dimensionality is decreased to 88x88x88x1.

Output: using sigmoid function which outputs two probability maps indiviually: P(i) reqpresents probability for each voxel to contain a skeletal joint and P(b) represents the probability for each voxel to be a bone. 

The output maps above are against processed through another 3 modules to get final maps. we stack multiple hour-
glass modules to progressively refine the joint and bone
predictions based on previous estimates

### Post processing ###
output of module give probablistic skeletal joints and bones. 
To avoid multiple near duplicate joint prediction, non max suppression applied to obtain joints of  skeleton. 

Threshold maintained to discard joints with less than the threshold values

For connecting the points, MST algo that minimize cost function over edges between extracted joints is used. cost function heuristics in paper itself and is driven by the bone probability map extracted by our network. Low bone probability means high cost
Root selected being the one closest to the shape centroid

## Training ##
Everything mentioned in paper
Augmentation applied to models in terms of rotation and scaling which resulted in 15526 training models
PyTorch used for implementation

## Results ##
Compared with Pinocchio, L1-median
Comparison metrics mentioned on paper. four metrics used

The higher the value of chamfer distance, the more errornous the prediction is. How chamfer distance is calculated is mentioned.


## Future Work ##
input method can be improved
Suggested to use other networks
post processing can be imporved

## Extra notes
* May no need to change anything in architecture having 82x82x82x5 input. 
* Can ask for curve skeleton dataset from Robert




















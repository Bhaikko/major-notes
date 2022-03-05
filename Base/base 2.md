## Input as five combinations of geometric features
* topology with SDF
* topology with SDF and local vertex density
* topology with SDF and 2 principle surface curvatures
* topology with SDF and local shape diameter
* topology with all features above
Topology means curve skeleton

```
SDF is used to convert 3D mesh into volumetric representation
The hourglass design uses autoencoders to contextualize the
image within the global scope, capturing features at every scale of the resolution, while simultaneously using residual blocks to maintain knowledge of local details.
```
```
Base 1 did not obtained direct info about medial surface, 
surface portion of the body that comprises the middle of the shape.
Ideal location for animation rig is generally along the medial surface of mesh
```
### Abstract
Mesh contraction processes can produce and extract curve skeletons. 
Curve skeletons contain properties consistent with general animated
rig principles and provide valuable information about medial surfaces. <br/>

Curve skeletons were extracted from dataset and used as geometric input feature to a Stacked hourglass network. <br/>

Stacked hourglass networks can identify joint and bone locations
while learning local detailing within global context.

Results compared using average chamfer distance metric

curve skeletons, stick-like 1D representations of 3D objects that capture the essential topology of the underlying object

Deep learning pose estimation networks approximate landmark 
locations in 2D pixels and 3D voxels for articulating limbs and identifying postures

### Overview
```
- Extracts curve skeletons using Skeletor plugin for each model
- Grid search to optimize extracted skeletons
- these extracted skeletons as an additional geometric input for every voxel
- ablation study to determine optimal threshold to suppress duplicate joints vertices
- 5 exp using combination of topology data + SDF + other features seperately
- chamfer distance for accuracy evaluation
```

```
Mesh contraction is skeleton extraction algo that applies a Laplacian
smoothing operator moving each vertex along its inner normal curvature, 
creating a zero volume skeletal shape. 
Has math related to it but its implementation can be found
```

```
Soft non max supression algo used to remove duplicate joint vertex landmarks
The point probability decreases by half for its surroundings
```

### Methodology
```
encoders downscales the data and extract features within global context

decoder performs a topdown sequence of upsampling and combining features from the lower resolutions

the final output of network is round of convolutions producing
a set of heatmaps, detailing per pixel likelihood for key joint locations

```

### Experiment Designs
```
Features mentioned in Experiment design

Dataset same as Xu et
mesh voxelized using binvox, rastered into 82x82x82 voxel grid
Other 5 input features extracted during process of creating dataset
Curve skeleton to provide features of medial surface and increase accuracy in joint and bone heatmaps

Triangulating the faces is required for mesh contraction process
Parameters for Contraction given below fig 4.3

Method of extracting curve skeletons mentioned here 4.2

```
**50 epochs and 10e-4 learning rate for training Training 30-50 min per epoch**
**Google colab max runs for 12 hours**

**Best model according to this is only topology model** 


### What we can contribute to 
* Consider this paper as base and since only topology gave best results, we can add one more feature to it creating a 82x82x82x* input and train our model.

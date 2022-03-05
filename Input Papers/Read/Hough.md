## Hough Transform and 3D SURF

```
two types of features: local shape features and global shape features

SURF used in context of 3D shapes

global features: features that need complete, isolated shape for their extraction
eg. Fourier or spherical harmonics, shape histograms, vertex density

use of local rathar than global features is advantageous
local features: heat kernel signatures, shape, 3D SURF
integral shape descriptors and scale dependent features 

A 3D extension to SURF serves as local descriptor
```

### Shape Representation as set of 3D surf
```
First, voxelize a shape in 3D cube of size 256x256x256
then saliency meansure for each grid bin x and several scale calculated

Finally Km unique features are extracted from volume using non maximal suppression

162 dimensional 3D SURF descriptor vector for feature obtained
```

```
https://www.linkedin.com/in/jan-knopp-75159479/?originalSubdomain=cz
```
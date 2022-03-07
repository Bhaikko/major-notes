## Final inputs
### Local Features (Sarthak)
// * harris 3D     
// * heat kernel                                   
* SURF 3D
* Shape index
* Curvature index
* Mean curvature                    - Ritika    1202
* Normal distribution               - Ritika    1202
// * Princiapl curvature estimations   - Ritika    1202
*Use PCL library*



### Global Features (Ritika)
* vertex density               - avaiable in base 1
// * Spherical harmonic
// * shape histogram
// * Ensemble of shape functions

### Input Representation
* 3d curve - Fix                    1
* similar to SDF                    1
* A local and global descriptor     4
* input based on other papers

Curve Skeleton - Robert
SDF - Xu
2 local 
1 global - vertext density - Xu

### Notes
Padding can be attached to data obtained from other descriptors

82x82x82x5

### Comparison
* XU et al
* Thesis
* Pinochio
* Ours

100%| 2555/2555 [1:17:35<00:00,  1.82s/it] - train
100%| 319/319 [09:10<00:00,  1.73s/it] - test
100%| 319/319 [08:33<00:00,  1.61s/it] - validation

#### Links
```
* heat kernel - 
https://github.com/ctralie/pyhks
https://github.com/DominikPenk/mesh-signatures
https://github.com/ChunyuanLI/spectral_descriptors
```

```
binvox to nparray data
https://stackoverflow.com/questions/37896090/how-to-represent-a-3d-obj-object-as-a-3d-array/37936160

```

```
Mean curvature
https://github.com/cuge1995/curvature-calculation-python
https://github.com/alecjacobson/geometry-processing-curvature
https://github.com/sujithTSR/surface-curvature

```

## 3D Library
```
  https://sourceforge.net/projects/meshprocessing/ 
  https://github.com/marcomusy/vedo
  https://pcl.readthedocs.io/projects/tutorials/en/master/how_features_work.html#how-3d-features-work
```
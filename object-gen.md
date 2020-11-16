## Notes
- **2D image -> 3D object requires prior knowledge of the 3D object itself**

### Representations 
    - 2D images (pixels)
    - 3D objects (voxel or polygon mesh or point cloud)

### Voxel
- aka volumetric pixel
- direction extension of spatial-grid pixels into volumetric grid voxels
- ![alt text](https://miro.medium.com/max/454/1*tU7Gogi4KusZUqMhaE5nUA.png)
    - most voxels are empty
    - ???locality of ConvNet holds true in volumetric format???
        - locality of ConvNet?
- ![alt text](https://miro.medium.com/max/1000/1*BraYPHcvslfsBu8zWsmDow.png)
    - density of useful voxels decrease, as resolution increase
- **Advantage**
    - can directly apply CNN from 2D to 3D represenation
- **Disadvantage**
    - wasteful reprsentation
    - high tradoffs between details and resources

### Polygon and Point Cloud 
- Polygon Mesh
    - collection of vertics, edges, and faces
    - capture granular details in a fairly compact representation
- Point Cloud
    - collection of points in 3D, forming the shape of the object
    - more collection points = more details
- **Advantages**
    - compact representation
    - focus on detail's surface
- **Disadvantages**
    - cannot apply CNN directly

## Approach 1
- Use point cloud's compact representation with traditional 2D ConvNet to learn the prior knowledge

### **2D CNN Structure Generator**
![alt text](https://miro.medium.com/max/1000/1*XBsH_-daV7GgHSSarDp-Wg.png)
- **leanrs the mapping from a single image to multiple 2D project of a point cloud**
    - with a 2D project defined as: `2D projection == 3D coordinates (x,y,z) + binary mask (m)`
    - Input:    single RGB image
    - Output:   2D project at predetermined viewpoints
    - Notes: presumabley, more viewpoints (slices) = better resolution
- Pseudo-code
```#--------- Pytorch pseudo-code for Structure Generator ---------#
class Structure_Generator(nn.Module):
    # contains two module in sequence, an encoder and a decoder
    def __init__(self):
        self.encoder = Encoder()
        self.decoder = Decoder()
    def forward(self, RGB_image):
        # Encoder takes in one RGB image and 
        # output an encoded deep shape-embedding
        shape_embedding = self.encoder(RGB_image)
        
        # Decoder takes the encoded values and output  
        # multiples 2D projection (XYZ + mask)
        XYZ, maskLogit = self.decoder(shape_embedding)
 
       return XYZ, maskLogit
```

### **Point Cloud Fusion**
![alt text](https://miro.medium.com/max/1000/1*U6pFwN2u2IdWjGpLROKy6w.png)
- **fuse the predicted 2D projections into a native 3D point cloud data**
    - possible due to predetermined viewpoints (aka slices)
    - Input: 2D projections at predetermined viewpoints
    - Output: point cloud

## **Pseudo-Renderer**
![alt text](https://miro.medium.com/max/1000/1*xNnbni5_HOfnCbCndznAWA.png)
- **generates new 2D projections at **new** viewpoints**
    - reason: if the point cloud is of any good, different 2D projections at new viewpoits should resemble the ground truth object too
    - Input: point cloud
    - Output: depth images (2D projections) at novel viewpoints
    - **Notes**: kinda like upscaling? point of failure? more loss functions to consider...

## References

[pytorch single image 3d reconstruction](https://medium.com/vitalify-asia/create-3d-model-from-a-single-2d-image-in-pytorch-917aca00bb07)
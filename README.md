# Overview:
The goal of this Repository is to do image rectification that removes projective and affine distortions. 

When we use our cameras to take photos of a large planar scene (such as buildings facade, or a wall decorated with pictures hanging, or a great expanse of the flat outdoors), we can see the distortions in the captured images. In general parallel lines on a scene plane are not parallel in the image but instead converge to a finite point. We can see that a central projection image of a plane (or section of a plane) is related to the original plane via a projective transformation, and so the image is projective distortion of the original. It is possible to “UNDO” this projective transformation. 

<img width="820" alt="Screen Shot 2023-02-24 at 1 16 32 PM" src="https://user-images.githubusercontent.com/53145353/221127541-5c520de7-35c5-48de-bdd0-1815e03aa00b.png">

The result will be a new synthesized image in which the objects in the plane are shown with their correct geometric shape.

## Removing perspective distortion:
We know, parallel lines intersect at infinity, whereas in a perspective image of a plane parallel lines meet at a finite point, that may be out of image boundaries. 

We have also studied that the parallel lines remain parallel under affine distortion. 

So, we can recover the affine properties from images by finding a transformation ​H​, that maps the vanishing line back into the line at infinity.

In summary, three steps should be applied to remove projective distortions:
1. Choose two sets of image lines which are physically parallel
2. Find the vanishing line ​lv​ ​ = [​l​1,​ l​2,​ l3​ ]​ T​ ​ using the above two sets of lines
3. Form Matrix ​H​ and apply ​H​ to camera images to get affinely rectified image.
 
## Removing Affine Distortion
Now, we get the affinely rectified image, we want to find the affine transformation matrix
Such that Xa = HAXs , where Xs is the scene image in the real world.
Suppose we have a pair of physically orthogonal lines l ⊥ m . Let l′, m′ be the
transformed lines under affine transformation H (e.g. l′ = H−T l ) i.e. lines l′, m′ are from AA
the affinely rectified image Xa . By orthogonality, we know that (l1/l3, l2/l3) (m1/m3, m2/m3)T = 0
 then Where
lm +lm =lTC*m=0 1122∞
 is the dual degenerate conic. Since C* = H C* HT , we have ∞ 2∞2
Therefore,
We have (l′ , l′ )AAT (m′ , m′ )T = 0 1212
In order to get A , let S = AAT , where S =
Because S is symmetric. Note that the last element of S is set as 1 considering the scale problem.
    
 can be written as AX = B .
 Figure 3: Physically Orthogonal lines shown in Red color.
Therefore, a pair of orthogonal lines provides an equation. ​We need two pairs of orthogonal lines l1⊥m1 and l2⊥m2 to solve the matrix S which has two unknown parameters. Note that these two pairs of lines should be non-parallel, otherwise the two equations will be equivalent.
We will get four points from user that will give us two pairs of orthogonal lines as shown in Figure 3 (Note, the lines has to be orthogonal physically).
The system of linear equation AX = B can be formed using four points:
Solving this system will give us X1 and X2 , that are used to form the matrix S :
Since the symmetric matrix S can be written as S = UDUT , where U−1 = UT we can get
A = U√DUT and HA can be formed using values of A, which is a 2 × 2 matrix.
Now, HA is available and we can get the rectified image. 

In summary, three steps should be applied to remove projective distortions:
1. Identify Affine Distortion
2. Calculate Transformation Matrix
3. Apply the inverse Transformation Matrix


For more details, please read section 2.7 “Recovery of affine and metric properties from images” of Multiview Geometry.

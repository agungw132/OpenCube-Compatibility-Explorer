OpenCube Compatibility Explorer
===============

The main role of the OpenCube Compatibility Explorer is to: 
+ identify compatible cubes for potential merge and
+ establish typed links to facilitate discovery 
 

###How it works

The OpenCube Compatibility Explorer is developed as a separate component of the OpenCube toolkit and is part of the “Data Expanding” lifecycle step. It identifies compatible cubes and establishes links between then to facilitate discovery. The cubes can be stored either at the native triple store or at remote SPARQL end-points. The OpenCube Compatibility Explorer can be initialized by creating a widget giving as input the URI of the remote SPARQL end-point (in the second case).

 Widget configuration for use with the native triple store:

```
{{#widget: LinkCreator|asynch='true'}}
```

Widget configuration for use with the remote SPARQL end-point containing data for the 2011 Irish Census:

```
{{#widget: LinkCreator| sparqlService='<http://data.cso.ie/sparql>'| asynch='true' }}
``` 

###Functionality

The OpenCube Compatibility Explorer mainly deals with two merge related operations:

Add measure. An expansion cubes is compatible to add a new measure to an original cube if: i) both cubes have the same dimensions, ii) the expansion cube has at least the same values at each dimension of the original cube (it may contain and more values than the original cube) and iii) the expansion cube has at least one measure that does not exist at the original cube.
Add value to dimension. An expansion cubes is compatible to add a new value to a dimension of an original cube if: i) both cubes have the same dimensions, ii) both cubes have the same measures and iii) the expansion cube has at least one value more than the original cube at the expansion dimension and has the same values with the original cube at all the rest dimensions.
After detecting compatible cubes based on the compatibility types presented above, OpenCube Compatibility Explorer creates links in order to be able to easily identify compatibility when requested (e.g. when browsing a cube). Two types of links are created:

+ **Measure compatible**. When two cubes are identified to be compatible to add a measure, then a link measureCompatible is created from the original cube to the expansion cube.

+ **Dimension value compatible**. When two cubes are identified to be compatible to add a new value to a dimension then a new blank node of type LinkSpecification is created. The original cube is associated to the blank node through the dimensionValueCompatible property, while the blank node is connected to the expansion cube with the property compatibleCube and with the expansion dimension with the property compatibleDimension.




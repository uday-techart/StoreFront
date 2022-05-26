# **Building Generator**

##  Intent
To create a building procedurally with a variety of modular mesh pieces pertaining to certain family or style.

Once building is generated, should be easy to customize the look and feel just by changing the order/pattern of the rooms.


## Overview
___

The key aspect of building generator is entirely based on the creation of a single floor. 

The key parameters are divided into two categories:
 - Basic Parameters<br>
  <img src="/images/img01.jpg/">

    - Setting Up number of rooms and floors
    - Adding modular mesh pieces
<br>

- Detailed Parameters<br>
    <img src="/images/img02.jpg/">
    - providing options for selecting variants for modular mesh pieces.
    
    - Each room /unit is created with the information provided in the  Facade and Side pattern. Similarly the corner pieces can be altered by changing the Select Corner Piece parameter.
<br>
> *<font color="orange">The blueprint lacks support for roof generation and material variations support.</font>*
## Brakedown
___

The functionality is divided into four main areas.
- Collection of modular mesh pieces for the room units, corner units and the roof units and setting up instances.
- Setting up arrays for the units along the facing units and units along the side.
- Calculating the over dimensions for the building and also identifying positions for each room unit and corner unit for a floor.  
- Creating a function to generate one floor and iterate over the desired number of rooms and floors.


### **`Modular Pieces`**

Storing moduring pieces for room,corners and roof in arrays in order to provide variations.

All mesh pieces in a floor need to be of certain height and width.

<img src="/images/img04.jpg">
For every mesh in the array an Hierarchial InstanceMesh array is also generated in order have optimization.
![detail params](/images/img03-1.jpg)


### **`Room Variation Arrays`**

Each floor has two arrays, One array is mapped to builing facing and rear and other is one for the sides of the building. 

<img src="/images/img05.jpg">

Each value in the array is mapped to the indices of the array where the list of meshes are stored.
<img src="/images/img06.jpg">


### **`Calculating Unit and Total Dimensions`**

Calculating key dimension values required in further functions.

<img src="/images/img07.jpg">

### **`Generating Floors`**
The floor variation parameters are stored in an array of struct and each then passed on to a floor generator function.
<img src="/images/img08.jpg">

The floor generator function is futher divided into three functions.
<img src="/images/img09.jpg">

- Calculation positions for each room unit based on the pattern and storing it in an array.

<img src="/images/img10.jpg">
<img src="/images/img11.jpg">

- Identifying corner positions and adding corner piece instances

![detail params](/images/img12.jpg)

- Finally passing the array of positions and adding instances for each unit. Also calculating position for opposites sides as well
![detail params](/images/img13.jpg)

## 
___
## Improvements for the Building generator

- Floor pattern generation could be automated and simplified for better end user experience.
- Need to accomodate material variations as well.
- Functions could have been more efficient and re-usable.
___

# **Storefront Material**

##  Inspiration

>UE4 Live Training session by Ryan Brucks on [Creation of Semi Procedural Materials](https://www.youtube.com/watch?v=1b3v5kyCTz4).

## Overview

The main aspect of the store front material is to render a fake interiors with the help of a baked cube map, and have parameters to control look and feel.
![detail params](/images/img21.jpg)


## Brakedown
___

The cube map is manipulated with UV tiling and UV offsets and on top the variations like random values of  the brightness,contrast, glow are overlayed with Roughness and Reflections.

![detail params](/images/img15.jpg)

Creating UV Tiling and UV Offsets for the interior Cube map
![detail params](/images/img14.jpg)

Creating UVs for Color Overlay Variation
![detail params](/images/img22.jpg)

Setting up Cube Map Textures and GlowMap Textures
![detail params](/images/img16.jpg)

Setting up Normals,Roughness and Reflections to simulate reflection on the Glass 
![detail params](/images/img17.jpg)
![detail params](/images/img18.jpg)
Mapping Scalar Parameters to a blueprint 
![detail params](/images/img19.jpg)
![detail params](/images/img20.jpg)


## Improvements
- Features like adding curtains or blinds. <br>
*Needed more understanding and experimentation*

- Adding Glass grunge around the borders of the glass
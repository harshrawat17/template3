---
title: Place and Route
layout: page
---
## Description

Certain assignments were given and completed to help 
understand the usage of TCL in the PnR domain. The algorithms and scripts used by 
these softwares are usually in TCL. TCL commands can be used to query various 
information from a given partition whose database is opened on these tools. Shown 
below are the 3 assignments (and their solutions), which required using TCL 
commands to perform tasks on a partition.

## PnR Flow
The PnR flow can be categorised into the steps shown in the image below.
![image](https://user-images.githubusercontent.com/33692444/149570095-b7873cc0-2a17-4961-8588-3e949bf7e10a.png)

## Assignment 1 – Finding different components of the chip

### Question 

1. Try to list out all the RAMs and soft macros ( instance and ref name) 
2. Try to list out the area occupied by the macros and RAMs.The output should be 
directed to a local file. Format should be : <Macro_name> <Area> 
3. Try to list out all the sequential cells ( unique ref name) and their count. 
4. Report the information for IO ports such as direction, layer and physical 
location 
5. Find out the floating output pins of all standard cells in the design 
6. Report dangling ports in the design 
7. Create a 200x200 hard placement blockage at topmost right corner of the block 
and convert it into partial blockage with 60% util. 

### Algorithm 
1. Filtered out the cells using name tag and attributes and then wrote this into a 
file. 
2. Extracted out the required info (name and area) and wrote that into a file. 
3. Filtered out all cells based on the attributes and then stored only the unique 
cells in a list. 
4. Extracted out the required info for ports (direction, layer, location) and wrote 
that into a file 
5. Filtered pins based on direction and then ran a loop to extract the pins that had 
no connected nets. 
6. Extracted all ports and then checked which ones were not connected to any pin 
(through a net) in the design. 
7. Directly implemented using an available command. 

## Assignment 2 – Finding the overlapping regions

### Question 
Write a proc, to get all shield net shapes in VM1 layer and find their overlap with 
VM2 PG straps.
a. Color all the VM1 shield shapes with red
b. Color the VM2 PG shapes with blue
c. Color the overlapping area between VM1 shield and VM2 PG straps 
with yellow. 
  
### Algorithm 
Wrote a proc that does the following -
1. Extracted all net shapes in the VM1 layer which had a shield type. 
2. Extracted all net shapes in the VM2 layer which were PG straps. 
3. Found the overlap region between the above 2 shapes by performing an AND 
operation on the 2 shapes. 
4. Found the region which was covered only by net shape 1 and not net shape 2 
by performing a NOT operation. 
5. Coloured the overlap region yellow using an in-built command. 
6. Couloured the non-overlap region red using the same command. 
7. Coloured the shape 2 region blue using the same command again. 

## Assignment 3 -  Tracing the Clock Tree

## Question 
Given a net, write a proc that will return its root driver pin by tracing through 
buffers/inverters.
  
## Algorithm 
Wrote a proc involving the following functionality. 
1. The proc takes a net as an input. 
2. Calculates the pins based on output direction. 
3. Get the respective cells of the pins. 
4. If Cell is not a buffer or inverted return the cell 
5. Otherwise take the input net of the Cell. 
6. Call the proc again for that net (Recursion). 

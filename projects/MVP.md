---
title:  Manhattan vs P2P Resistance  
layout: page
---
## Objective

To determine the relation between Manhattan Distance and P2P Resistance to get the ideal 
coefficient which can tell if a net is properly routed or not and which also helps to determine 
if any of these metrics such as detour, preferred layer usage, jogs etc. is likely to be off from 
its expected value

## Description

Manhattan Distance which is the distance between two points measured along axes at 
right angles. In a plane with p1 at (x1, y1) and p2 at (x2, y2), it is |x1 - x2| + |y1 - y2|.
Point to Point Resistance is the resistance between two points of a net.
The project mainly deals with the pre-route stage as there are certain nets in the design 
that are critical in terms of the signal they carry. These include nets that have high 
activity and are more susceptible to noise. They have special routing rules specified 
for them as they have extra spacing, width and shielding requirements (to prevent 
crosstalk). These special rules are called NonDefault Rules (NDR’s) and they take 
care of the extra requirements for these nets. Each metal layer in the design has a 
default width and spacing that is used during routing. However, the nets for which 
NDR has been specified, use non-default values for width and spacing as per the non 
default rule applied. The NDR’s are stored in a file, and are accessed by the tool while 
pre-routing such nets.
The project captures the Manhattan Distance and Point to Point Resistance along with 
their respective NDR for a net with the help of pre-defined procs and then it helps to
determine the variation of the above by plotting graphs for the same.

## Step 1 - Use the defined procs to get the data from the blocks 

The first block tested had very less pre-route nets hence not fit for the analysis.
Ran a python script across all the blocks of blocks . Used the glob function which 
searched for a particular file inside each partition to check the number of pre-route 
nets and which is also responsible for creating the tcl file from make setup and then I 
save the output to a csv file
Picked up a block with highest number of pre-route nets to have good set of data 
points.
The first block I ran had enough pre -route nets to anaylse as you can see the graph 
below.
![image](https://user-images.githubusercontent.com/33692444/149575261-615ef0a2-7cbd-477d-beec-9fd916b91594.png)


## Step 2 – Analysis of the graph

As seen from the graph above the green nets are the io nets and the red ones are the 
non io nets, as we can also observe the io nets have less resistance per manhattan 
compared to non io nets . 
The reason for the above is because for the io nets the ports are mainly on the top 
layers such as VM1 , VM2 so tapping is done only on one end where the layer is TM 
where the macro connection is there whereas in the non_io nets the pins are mainly 
situated in the TM layers so tapping is done twice and the via cost is fixed .
The block above is a grout which is not suitable for the Analysis since it is basically a 
interface block which will be carrying the most of the wires to enhance speedy 
connectivity across chiplets . Lots of connectivity means lots of traffic which in turn 
means lots of violations.

## Step 3 – Analysis of block with less nets 

The earlier block was not fit for the analysis so the next block picked had little less nets , but as you 
can see the slopes of the in these graph below is negative which is not expected as the Resistance 
should increase with increasing Manhattan .
![image](https://user-images.githubusercontent.com/33692444/149575479-a559812d-59db-4c93-a7ea-97f5ad6f84be.png)



## Step 4 – Reason for the negative slope

I find out the expected value of resistance from the line equation and compared them 
with the actual value , the major reasons for higher resistance was the following 2 
points 
1. There was detour in the path
2. Unpreferred layer usage which caused jogs
So further filtration was done and removal of the antenna fixed nets and the io nets
was done to just get the plot according to similar pin layers . The reason antenna fixes 
are removed is because there are the following two methods to fix antenna violations 
• Metal jumper - Which means breaking the long metal layer and 
introducing extra vias to the higher metal layer to break the connection so 
that connection to the gate is also broken and there is path for charge to 
discharge. 
• Inserting the diode along the metal layer so that the charge is grounded 
when the diode is on. 
Both of the above methods results in the increase of resistance as the extra vias in the 
first method contributes to jogs and detour and the second method involves 
multifanout net where one sink is a diode which has high resistance as it is reverse 
biased 

## Step 5 – Filtered graph and further analysis 

The graph below is according to the similar pin layers and there are not enough data 
points to capture so I searched for blocks with least violations to have more data 
points
![image](https://user-images.githubusercontent.com/33692444/149575590-baaa1d16-cad6-4e82-a9d4-364bdf1fda17.png)

## Step 6 – Analysing different blocks

Found a block with very less violations
The following graph seems very accurate as it according to the expectations so 
searched for more such blocks
![image](https://user-images.githubusercontent.com/33692444/149575651-3f0d969a-51a8-4695-a0b9-727daa004ab8.png)

# CONCLUSION

The blocks can be researched on with the respective NDR , we can combine all NDR 
together since all of them are physically equivalent to study further and determine 
the relation between Manhattan and P2P Resistance .



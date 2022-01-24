---
title:  Frequency Dividers
layout: page
---
## Description

Calculated the delay time from clock to q for the Static and Dynamic Flip flops 

Static CMOS and CML was made using Gpdk45n and Dynamic CMOS was made using UMC_180n. 
 Simulations were carried out in Cadence Virtuoso

## Static CMOS flip flop Circuit Diagrams

![image](https://user-images.githubusercontent.com/33692444/150675352-ef9012e3-70fb-45b0-82f8-3a254a7b24af.png)

&nbsp;

![image](https://user-images.githubusercontent.com/33692444/150675370-1768e98c-8a51-4bcc-a41f-d27a81406d2f.png)


&nbsp;

![image](https://user-images.githubusercontent.com/33692444/150675387-52c1326f-8c26-4b92-ac8e-36e9f0d9ffdd.png)
&nbsp;
![image](https://user-images.githubusercontent.com/33692444/150675396-10714a95-59fc-4595-a06a-2bf816edc983.png)
&nbsp;
![image](https://user-images.githubusercontent.com/33692444/150675406-509eafaf-271d-41ca-a13e-c4c16f07305c.png)

## Waveforms and Results


![image](https://user-images.githubusercontent.com/33692444/150675523-4531d05a-dc5a-4282-b4a6-87f4cbd10cc6.png)



## Dynamic CMOS flip flop Circuit Diagram

![image](https://user-images.githubusercontent.com/33692444/150675498-df1e489a-1153-4c62-ba9f-b1575de922a7.png)

## Waveforms and Results

![image](https://user-images.githubusercontent.com/33692444/150680018-4b47365e-9b25-4fd1-9831-e15f8103b7a9.png)

### As we can see dynamic CMOS flip flop is slower than static CMOS flip flop .
&nbsp;
## Static CMOS divider 

![image](https://user-images.githubusercontent.com/33692444/150680055-2461f9c7-a009-4437-993d-9d92900959c1.png)

## Output Waveforms and Explanation

![image](https://user-images.githubusercontent.com/33692444/150680068-7c4c65e7-77be-45d8-99c0-a3d48a816386.png)

## Divide by 3 static CMOS

![image](https://user-images.githubusercontent.com/33692444/150680091-48c96e48-9460-483e-a816-ee248df8bd8a.png)

## Output Waveforms and Explanation

![image](https://user-images.githubusercontent.com/33692444/150680106-691a1a1f-75cd-43e3-827a-e7f692a6c164.png)

### The circuit fails after the required frequency as it no longer is able to match the frequency speed , in order for this to work , a faster logic like a CML logic needs to be used.
&nbsp;

## Divide by 1024 Static CMOS and CML.

![image](https://user-images.githubusercontent.com/33692444/150681570-c6004d7f-6bfa-49f0-8509-90f237b1cb8b.png)

### There were a total of 10 stages . The first two stages were not working with Static CMOS , hence CML logic had to be implemented for the first two stages followed by CMOS .


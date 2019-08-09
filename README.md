## Implementation steps for the 2D CFAR process

1. Select the number of Training Cells in both the dimensions Tr and Td; and select the number of Guard Cells in both dimensions around the Cell under test(CUT) Gr and Gd. 
<br/>

2. Design a loop such that it slides the CUT across range doppler map.
<br/>

3. For every iteration sum the signal level within all the training cells. To sum convert the value from logarithmic to linear using db2pow function.
<br/>

4. Average the summed values for all of the training cells used. After averaging convert it back to logarithimic using pow2db.
<br/>

5. Further adding the offset to it to determine the threshold. 
<br/>

6. Compare the signal under CUT with this threshold. If the CUT level > threshold assign it a value of 1, else equate it to 0.
<br/>

7. To keep the map size as it was before CFAR, assign 0 to all the non-thresholded cell to 0.


## Selection of Training, Guard cells and offset

* the number of Training Cells in range dimension Tr = 10
* the number of Training Cells in doppler dimension Td = 8
* the number of Guard Cells in range dimension Gr = 4
* the number of Guard Cells in doppler dimension Gd = 4
* offset the threshold by SNR value in dB, offset = 1.4


## Steps taken to suppress the non-thresholded cells at the edges
The process above will generate a thresholded block, which is smaller than the Range Doppler Map as the CUT cannot be located at the edges of matrix. Hence,few cells will not be thresholded. To keep the map size same set those values to 0. By this way:
```
RDM(RDM~=0 & RDM~=1) = 0;
```
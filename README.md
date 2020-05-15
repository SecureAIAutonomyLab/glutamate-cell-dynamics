# glutamate-cell-dynamics

## Abstract ##:
Glutamate is the main excitatory neurotransmitter produced in the brain. It is produced physiologically to communicate information between neurons. However, after a traumatic brain injury (TBI) glutamate is over produced. High levels of glutamate after a TBI are associated to the occurrence of seizures, cognitive impairment and cell death. There is an article published studying a promising treatment for TBI, Retigabine. Such drug was able to impair some of the TBI-induced deleterious effects like seizures and cell death. We now aim to investigate the mechanism by which this drug is acting. To do so they have recorded videos imaging the levels of glutamate that “bath” neurons in the brain of mice before and after a TBI. Half of the animals will receive retigabine treatment and half willreceive only vehicle injection. The mice will be imaged in the morning, subjected to a TBI and image again immediately after the TBI, all within the same day. As explained in their grant proposal, the neurons of these mice express a fluorescent reporter that emits light when glutamate binds to it. Therefore, they expect that the intensity of the fluorescence signal per cell, as well as the number of cells emitting light, increase after the TBI. So, they need a script that can identify these cells and quantify the intensity of fluorescent signal in each cell throughout the video recording.


Additionally, it is important to quantify the number of cells in each video. As neurons use glutamate physiologically, they expect the fluorescent signal of the cells to vary during the video recording evenbefore the TBI. Big variations in the fluorescent signal indicates that neurons are actively firing. To analyze this kind of data and identify moments where neurons are firing what they do is normalize the fluorescent signal of the cell in each image/frame in a video (F) to the signal of the same cell obtain in the first image/frame of the video (F0). The calculation is ΔF/F0, where ΔF = F - F0. After obtaining the data they set a threshold of variation. If the variation is bigger than the threshold set, they consider that the neuron has fired. They expect neurons to fire more after the TBI and they expect that retigabine will reduce this TBI-induced excessive firing. 


A second level of analysis is to correlate the firing of one neuron to the firing of another, so they can identify network of neurons that are communicating with each other. Neurons that fire in synchrony with each other are networking and we believe that TBI might change the neuronal networks.


### Project pipeline from technical stand-point ###
Each video recording has 2000 frames where alternate frames are recorded with two different lens. Basically, we are concentrating on even number of frames starting with 0 through 1999 as they have used better lens while recording even numbered frames. Now, lets go through the steps involved to achieve final result.

1. Load the video and extract all the 2000 frames and store them in a seperate folder.
2. As the frames almost looks like blank to human eye, to start working on neuron segmentation task and to get to know whether our algorithm is giving better result, we took an average of the pixels of all the even numbered frames(staring with zero).
3. After getting Average of pixels image, next task is to improve contrast. For that we performed percentile contrast stretching. On top of that we performed adaptive thresholding and then Median blurring and then image sharpening using filter2D.
4. Labeling, finding and drawing contours.
5. Numbering all the contours detected on the average image.
6. Save each contour as a different mask into a seperate folder.
7. Now, copy each mask starting zeroth contour/neuron detected onto all even numbered frames and take an average of all pixels for each frame and save them to a pandas dataframe.
8. Now we, have a dataframe where each row is contour/ neurons detected through segmentation and each column(1000 columns) is a frame.
9. Calculate deltaF/F0 (as explained in absract section above) values in the dataframe and plot a graph for each neuron of your choice.
10. We have given an option to set a threshold value and to find which frames of a particular neuron crossed the threshold and save results to excel sheet.

#### Running Code ####
The script is in jupyter notebook. So run each cell by using keyboard shortcut (Shift+Enter) or there is an option to run all the cells at a time.



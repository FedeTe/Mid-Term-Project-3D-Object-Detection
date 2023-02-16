# Mid-Term-Project-3D-Object-Detection
This project has several task to be performed, divided as follow:
* Step 1
* Step 2
* Step 3
* step 4

## Reference code
[loop_over_dataset.py](loop_over_dataset.py)
<br>
[objdet_pcl.py](objdet_pcl.py)
<br>
[objdet_detect.py](objdet_detect.py)
<br>
[objdet_eval.py](objdet_eval.py)

## Step 1
The aim of this step is to extract Lidar data from the image, both range image and intensity channels, stack them together and eventually compute the Lidar point-cloud using Open3D library.
<br>
The results of the steps are the following:
![range+intensity](Pics/range_intensity.png)
In the following images are shown some example of point cloud; I've taken some screenshots on different scenarios (straight line, T-junction, X-junction) where it's possible to identify front and rear bumpers of the following and upcoming vehicles respectively, pedestrians, road poles, walls. In the screenshots shape and vehicle's direction are easy to determine, tail lights aren't visible nor interfere with Lidar return signal, probably measurements were taken in day-light condition.

![pcl1](Pics/pcl1.png "pcl1") *Bumpers of preceeding and following vehicles* 
![pcl2](Pics/pcl2.png "pcl2") *Tails of preceeding vehicles*
![pcl3](Pics/pcl3.png "pcl3") *Tails of preceeding vehicles and pedestrians on the left*
![pcl4](Pics/pcl4.png "pcl4") *Preceeding vehicles in a T-junction*
![pcl5](Pics/pcl5.png "pcl5") *Preceeding vehicles, walls and trees on the road side*
![pcl6](Pics/pcl6.png "pcl6") *Preceeding vehicles in a X-junction*

## Step 2
The aim of this step is to extract to create Bird's Eye View image from point-cloud data and then compute intensity and height lchannels of the BEV map.

### BEV map
Coordinates from the sensor space have been converted to BEV coordinates.
![bev](Pics/bev.png) *BEV map*

### Intensity channel
Here is the plot of the intensity channel with "raw" values (no modification on the insensity value); the contrast in this picture isn't high, so I've tried to change point distribution to increase it.

![int_bef_1](Pics/int_bef_1.png) ![int_bef_2](Pics/int_bef_2.png) ![int_bef_3](Pics/int_bef_3.png)

Intensity distribution points were concentrated between 0.01 and 0.1:

```
b = np.array([0, 1e-5, 1e-4, 1e-3, 1e-2, 1e-1, 1, 1e+1, 1e+3, 1e+3, 1e+4, 1e+5, 1e+6, 1e+7])
hist,bins = np.histogram(lidar_pcl_cpy[:,3], bins=b)
print(hist)
```

![distrib](Pics/distrib.png) *Intensity points distribution*

In order to achieve an higher contrast in the intensity layers I've applied the following correction to the raw values; the idea is to "lower" the points with higher intensity to the mean value and, doing so, increase the contrast.

```
lidar_pcl_cpy[lidar_pcl_cpy[:, 3] > 0.1, 3] = 0.01
```

The result after the correction is the following:

![int_aft_1](Pics/int_aft_1.png)
![int_aft_2](Pics/int_aft_2.png)

### Height channel
Resulting height channel picture has good contrast, no modification have been applies to the raw values.

![hei_1](Pics/hei_1.png)
![hei_2](Pics/hei_2.png)

## Step 3
The aim of this step is to set configuration for the resnet model, run the model on a couple of frames and evaluate the output.
I've used the following configuration for the resnet model:

```
inserire config
```

At this point, the detection arrays (on 2 sample frames) look like this:

![detect](Pics/detect.png) *Detection arrays*

In order to visualize the bounding boxes on the pitcure (only for vehicle class), BEV coordinates has to be converted into metric coordinates. The result of the operation is shown in the next picture; the model successfully detected and classified the object as vehicle.

![bb1](Pics/bb1.png)

## Step 4
In this step evaluation of the object detection is performed; at first some evaluation is performed on a couple of frames then precision and recall are calculated on a larger pool of samples. 

![iou](Pics/iou.png) *Frame 50 results*

The project requests to run precision and recall on 100 samples, here the result.

![pr1](Pics/pr1.png) *Precision and recall on object detection model results*

Then I repeated the same steps using ground truth data instead of the darknet model results; in this case precision and recall are equal to 1.

![pr2](Pics/pr2.png) *Precision and recall on ground truth data*

## General comment
There're some inconsistency in the code provided for the project so the students has to check/modify code even if it's not part of the exercise. 

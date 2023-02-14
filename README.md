# Mid-Term-Project-3D-Object-Detection
This project has several task to be performed, divided as follow:
* Step 1
* Step 2
* Step 3
* step 4

## Step 1
The aim of this step is to extract Lidar data from the image, both range image and intensity channels, stack them together and eventually compute the Lidar point-cloud using Open3D library (source code is in [objdet_pcl.py](objdet_pcl.py)).
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

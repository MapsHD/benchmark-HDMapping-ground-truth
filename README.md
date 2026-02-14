# benchmark-HDMapping-ground-truth
With this instruction You will prepare ground truth trajectory.

## Step 1 (download reference ground truth TLS data)
Download the dataset 'map_gt_0.01.pcd' from 
[link](https://charleshamesse.github.io/bunker-dvi-dataset/docs/download.html) and convert it to '*.laz' using CloudCompare [link](https://www.cloudcompare.org/).
Create 'ground_truth/TLS-FARO-Focus' folder and copy donloaded data with following commands:

```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus
cd ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus
cp <download_folder>/map_gt_0.01.pcd .
```

Convert 'map_gt_0.01.pcd' file to map_gt_0.01.laz with foillowing command

```shell
cd <hdmapping folder with executables> //follow installation instruction at https://github.com/MapsHD/HDMapping
./pcd_to_laz ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus/map_gt_0.01.pcd ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus/map_gt_0.01.laz 
```

Alternatively You can use CloudCompare.
Movie how to convert data from *.pcd to *.laz  [[movie]](https://youtu.be/IxEMLGVlDdQ).

## Step 2 (download reference mobile mapping LiDAR data that includes LiVOX MID360)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)) 

Create 'ground_truth/MobileMappingSystemLivoxMID360_ROS1' folder and copy downloaded data with following commands:

```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360_ROS1
cd ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360_ROS1
cp <download_folder>/reg-1.bag .
```

## Step 3 (prepare code)
```shell
mkdir -p ~/hdmapping-benchmark
cd ~/hdmapping-benchmark
git clone https://github.com/MapsHD/mandeye_to_bag.git --recursive
```

## Step 4 (build docker)
```shell
cd ~/hdmapping-benchmark/mandeye_to_bag
docker build -t mandeye-ws_noetic --target ros1 .
```

## Step 5 (run docker)
```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/HDMappingGroundTruth
cd ~/hdmapping-benchmark/mandeye_to_bag
chmod +x mandeye-convert.sh 
./mandeye-convert.sh ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360_ROS1/reg-1.bag ~/hdmapping-benchmark/data/ground_truth/HDMappingGroundTruth ros1-to-hdmapping
```

## Step 6 (prepare ground truth data using 'lidar_odometry_step_1')
Follow procedure in this movie [[movie]](https://youtu.be/8sHyUNC3mZs).

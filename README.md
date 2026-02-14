# benchmark-HDMapping-ground-truth

## Step 1 (download reference ground truth TLS data)
Download the dataset 'map_gt.pcd', 'map_gt_0.01.pcd' and 'map_gt_0.05.pcd' from 
[link](https://charleshamesse.github.io/bunker-dvi-dataset/docs/download.html) and convert it to '*.laz' using CloudCompare [link](https://www.cloudcompare.org/).
Create 'ground_truth/TLS-FARO-Focus' folder and copy donloaded data with following commands:

```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus
cd ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus
cp <download_folder>/map_gt.pcd .
cp <download_folder>/map_gt_0.01.pcd .
cp <download_folder>/map_gt_0.05.pcd .
```

movie how to convert data

## Step 2 (download reference mobile mapping LiDAR data that includes LiVOX MID360)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)) 

Create 'ground_truth/MobileMappingSystemLivoxMID360_ROS1' folder and copy donloaded data with following commands:

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

 

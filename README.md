# benchmark-HDMapping-ground-truth

## Step 1 (download reference ground truth TLS data)
Download the dataset 'map_gt.pcd', 'map_gt_0.01.pcd' and 'map_gt_0.05.pcd' from 
[link](https://charleshamesse.github.io/bunker-dvi-dataset/docs/download.html) and convert it to '*.laz' using CloudCompare [link](https://www.cloudcompare.org/).
Create 'ground_truth/TLS-FARO-Focus' folder and copy donloaded data with following commands:

```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/TLS-FARO-Focus
cd ~/hdmapping-benchmark/data/ground_truth/TLS
cp <download_folder>/map_gt.pcd .
cp <download_folder>/map_gt_0.01.pcd .
cp <download_folder>/map_gt_0.05.pcd .
```

## Step 2 (download reference mobile mapping LiDAR data, incluidng LiVOX MID360)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)) 

Create 'ground_truth/MobileMappingSystemLivoxMID360' folder and copy donloaded data with following commands:

```shell
mkdir -p ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360
cd ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360
cp <download_folder>/reg-1.bag .
```

## Step 3 (prepare code)
```shell
mkdir -p ~/hdmapping-benchmark
cd ~/hdmapping-benchmark
git clone https://github.com/MapsHD/livox_bag_aggregate.git --recursive
```

## Step 4 (build docker)
```shell
cd ~/hdmapping-benchmark/livox_bag_aggregate
docker build -t livox_bag_aggregate_noetic .
```

## Step 5 (run docker)
```shell
cd ~/hdmapping-benchmark/livox_bag_aggregate
mkdir -p cd ~/hdmapping-benchmark/data/ground_truth/HDMappingGroundTruth
cd ~/hdmapping-benchmark/data/ground_truth/HDMappingGroundTruth
~/hdmapping-benchmark/livox_bag_aggregate/livox_bag.sh ~/hdmapping-benchmark/data/ground_truth/MobileMappingSystemLivoxMID360/reg-1.bag .
```


 

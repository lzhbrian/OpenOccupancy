
# Prepare nuScenes-Occupancy
**1. Download nuScenes V1.0 full dataset data [HERE](https://www.nuscenes.org/download). Folder structure:**
```
OpenOccupancy
├── data/
│   ├── nuscenes/
│   │   ├── maps/
│   │   ├── samples/
│   │   ├── sweeps/
│   │   ├── lidarseg/
│   │   ├── v1.0-test/
│   │   ├── v1.0-trainval/
```


**2. Download the generated [train](https://github.com/JeffWang987/OpenOccupancy/releases/tag/train_pkl)/[val](https://github.com/JeffWang987/OpenOccupancy/releases/tag/val_pkl) pickle files and put them in data. Folder structure:**
```
OpenOccupancy
├── data/
│   ├── nuscenes/
│   │   ├── maps/
│   │   ├── samples/
│   │   ├── sweeps/
│   │   ├── lidarseg/
│   │   ├── v1.0-test/
│   │   ├── v1.0-trainval/
│   │   ├── nuscenes_occ_infos_train.pkl/
│   │   ├── nuscenes_occ_infos_val.pkl/
```

**2. Pre-compute depth map for fast training (depth-aware view transform module, same logic as [BEVDepth](https://github.com/Megvii-BaseDetection/BEVDepth)):**
```
python ./tools/gen_data/gen_depth_gt.py
```
**Folder structure:**
```
OpenOccupancy
├── data/
│   ├── nuscenes/
│   ├── depth_gt/
```

**3. Download and unzip our annotation for nuScenes-Occupancy:**
| Subset | Google Drive <img src="https://ssl.gstatic.com/docs/doclist/images/drive_2022q3_32dp.png" alt="Google Drive" width="18"/> | Baidu Cloud <img src="https://nd-static.bdstatic.com/m-static/v20-main/favicon-main.ico" alt="Baidu Yun" width="18"/> | Size |
| :---: | :---: | :---: | :---: |
| trainval | [TODO]() | [link](https://pan.baidu.com/s/1BRRaxBCuVbEvz4cL0-I8hg) (code:BS95) | approx. 24G |

We will release annotation (with more iterations of augmenting and purifying) in the future.
```
mv nuScenes-Occupancy-v0.0.7z ./data
cd ./data
7za x nuScenes-Occupancy
```
**Folder structure:**
```
OpenOccupancy
├── data/
│   ├── nuscenes/
│   ├── depth_gt/
│   ├── nuScenes-Occupancy/

```

## Basic information of nuScenes-Occupancy

<div align="center">
  
| Type |  Info |
| :----: | :----: |
| train           | 28,130 frames |
| val             | 6,019 frames |
| cameras         | 6 |
| voxel size      | 0.2m |
| range           | [-51.2, -51.2, -5m, 51.2, 51.2m, 3m]|
| volume size     | [512, 512, 40]|
| classes         | 0 - 16 (see bellow) |
  
</div>

<div align="center">

| Label |  Category |
| :----: | :----: |
| 0*      | noise |
| 1      | barrier |
| 2      | bicycle |
| 3      | bus |
| 4      | car |
| 5      | construction |
| 6      | motorcycle  |
| 7      | pedestrian  |
| 8      | trafficcone  |
| 9      | trailer  |
| 10      | truck  |
| 11      | driveable_surface  |
| 12      | other  |
| 13      | sidewalk  |
| 14      | terrain  |
| 15      | mannade  |
| 16      | vegetation  |

</div>

*Note that we ignore **noise**, and set **empty** as label 0 in the training phase.



# CV Final Project: Inverse Segmentation


## 模型介紹
本作品使用[pix2pix](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix)以及[SinGAN](https://github.com/tamarott/SinGAN)這兩個Model

以下為改自 [SinGAN](https://github.com/tamarott/SinGAN) 參數，分別使用不同的 Dataset_size / 有沒有加 LayerNorm / 在 conv 加入 dropout 層

| Model Name   | type     | datasize | niter | LayerNorm | dropout   |
| ------------ | -------- | -------- | ----- | --------- | --------- |
| SinGAN_typeA | SinGAN_C | 4        | 500   | Yes       | No        |
| SinGAN_typeB | SinGAN_C | 4        | 500   | No        | No        |
| SinGAN_typeC | SinGAN_C | 4        | 500   | Yes       | Yes (0.1) |
| SinGAN_typeD | SinGAN_C | 16       | 500   | Yes       | No        |
| SinGAN_typeE | SinGAN_D | 4        | 500   | N/A       | No        |
| SinGAN_typeF | SinGAN_D | 4        | 500   | N/A       | Yes (0.1) |

## 需要以下的套件

- 建議電腦配備
```
GPU : Geforce RTX2080Ti 11G
OS  : Ubuntu 16.04 LTS, 18.04 LTS
Cuda Version  : 10.1
Cudnn Version : 7.6.5
```

- python 所需要的套件
```
matplotlib
scikit-image
scikit-learn
scipy
numpy
torch==1.3.0
torchvision
Pillow
opencv-python==4.1.1.26
imgaug
dominate>=2.3.1
visdom>=0.1.8.3
```
## Trained Models
[Google Drive](https://drive.google.com/open?id=1H1uDzzwi7uClEY_lJEsyMarji3RX-ckb)
- 對於**pix2pix**
1. 在雲端內進入 `pix2pix/cityUnetmix2` 目錄
2. 選擇 `latest_net_G.pth` 下載
3. 將下載好的model放入主目錄下，並且輸入正確的目錄位址
- 對於**SinGAN**
1. 進入想要下載的SinGAN Type目錄
2. 進入到`TrainedModels/cityscapes/scale_factor=0.750000_seg/`
3. 將所有的`*.pth`下載
4. 對於主目錄，進入與**想要下載的SinGAN Type**同目錄
5. 進入到`TrainedModels/cityscapes/scale_factor=0.750000_seg/`
6. 將所有下載的四個model移至這裡

## Datasets Preprocessing
1. 在主目錄建立 `CV_project/datasets` 資料夾
2. 將**DataSets**放置在主目錄 `CV_project/datasets` 裡面，使用**cityscapes**

## 如何Training
1. 將目前位置移置 **Model Name** 底下 `cd ${your_model_path}`
  - example : `cd SinGAN_C_typeA`
2. 鍵入指令 `python -W ignore seg_train.py` 就可以開始訓練
3. 每次訓練都會把 Model 放置在當前目錄的 `TrainedModels/cityscapes/scale_factor=0.750000_seg/` 底下，
4. 輸出的亂數影像也會在同個目錄。


## 圖片測試
**請使用python3.7執行**
- 對於 **Pix2Pix**
```bash=linux
python running.py --input_picture ${your_seg_image} --pix2pix_path ${pix2pix_model_path} --source_picture ${real_image_of_your_seg_image}
```
> - `${real_image_of_your_seg_image}` 是相對於 `${your_seg_image}` 的真實照片
- 對於 **SinGAN**
```bash=linux
python running.py --input_picture ${your_seg_image} --singan_model_dir ${your_model_name} --singan_model ${your_trained_model_name} --mode B --source_picture ${real_image_of_your_seg_image}
```
> - `${your_trained_model_name}`會放在`./${your_model_name}/TrainedModels/`下
> - `${real_image_of_your_seg_image}` 是相對於 `${your_seg_image}` 的真實照片
- 建議使用類似cityscapes的(segmentation, real image) pair 測試

## Demo
[Demo Video](https://youtu.be/OyJVbbEGA3g)


# Face_detector_repo

# fine tuning Yolov8m to face detector

make new enviroment

```
conda create -n face_detector_repo python=3.10
conda activate face_detector_repo
```

Install requirements libraries

```
pip install torch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 --index-url https://download.pytorch.org/whl/cu118
pip install ultralytics
```

Make repository

```
mkdir face_detector_repo/
cd face_detector_repo/
```

Download train dataset

```
cp -r {PATH_TO_YOUR_DATASET}/wider_face ./face_detector_repo/
```

Fine-tune Yolov8m

```
yolo detect train data='/wider_face/wider_face.yaml' model=yolov8m.pt epochs=300 imgsz=640 device=0
```
Your must have precision: 0.874, recall: 0.655, mAP50: 0.742, mAP50-95: 0.411

Results saved to runs/detect/train

Fine-tune model saved to folder ./runs/detect/train/weights/best.pt

# Testing

Copy test dataset

```
cp -r {PATH_TO_YOUR_DATASET}/test_dataset ./face_detector_repo/
```

Test model

```
yolo val task=detect model=./runs/detect/train/weights/best.pt data=./test_dataset/test_dataset.yaml 
```

Results saved to runs/detect/val

Your must have precision: 0.982, recall: 0.96, mAP50: 0.983, mAP50-95: 0.731

# Inference

Download photo

For example:

```
cp  {PATH_TO_YOUR_PHOTO}/selfie.jpg ./face_detector_repo/
```

Inference

```
yolo predict task=detect model=/root/face_detector_repo/runs/detect/train2/weights/best.pt source='./selfie.jpg'
```

Results saved to runs/detect/predict


Download video

For example:

```
cp  {PATH_TO_YOUR_VIDEO}/MTCNN_video.mp ./face_detector_repo/
```

Inference

```
yolo predict task=detect model=/root/face_detector_repo/runs/detect/train2/weights/best.pt source='./MTCNN_video.mp3
```

Results saved to runs/detect/predict2


An example of code execution is located in this repository




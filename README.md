# Clonar o repositório e instalar dependências
!git clone https://github.com/ultralytics/yolov5
%cd yolov5
!pip install -r requirements.txt

# Montar o Google Drive
from google.colab import drive
drive.mount('/content/drive')

# Treinar com 30 e 60 épocas
!python train.py --img 640 --batch 16 --epochs 30 \
--data /content/drive/MyDrive/YOLO/dataset/dataset.yaml \
--weights yolov5s.pt --project /content/drive/MyDrive/YOLO/runs/train --name exp30

!python train.py --img 640 --batch 16 --epochs 60 \
--data /content/drive/MyDrive/YOLO/dataset/dataset.yaml \
--weights yolov5s.pt --project /content/drive/MyDrive/YOLO/runs/train --name exp60

# Validação dos modelos
!python val.py --weights /content/drive/MyDrive/YOLO/runs/train/exp30/weights/best.pt --data /content/drive/MyDrive/YOLO/dataset/dataset.yaml
!python val.py --weights /content/drive/MyDrive/YOLO/runs/train/exp60/weights/best.pt --data /content/drive/MyDrive/YOLO/dataset/dataset.yaml

# Teste dos modelos com novas imagens
!python detect.py --weights /content/drive/MyDrive/YOLO/runs/train/exp30/weights/best.pt --img 640 --source /content/drive/MyDrive/YOLO/dataset/images/test --project /content/drive/MyDrive/YOLO/runs/detect --name test30
!python detect.py --weights /content/drive/MyDrive/YOLO/runs/train/exp60/weights/best.pt --img 640 --source /content/drive/MyDrive/YOLO/dataset/images/test --project /content/drive/MyDrive/YOLO/runs/detect --name test60

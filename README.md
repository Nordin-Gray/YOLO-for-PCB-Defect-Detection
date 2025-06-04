# YOLO-for-PCB-Defect-Detection
Application of YOLO in Defect Detection of PCB

# 一、项目介绍

数据集：北大戴琳辉数据集
预训练权重：yolo11n.pt
训练参数设置：

``` python
if __name__ == '__main__':
    model = YOLO(model=r'D:\Desktop\YOLOv11\ultralytics\cfg\models\11\yolo11.yaml')
    model.load('yolo11n.pt')  # 加载预训练权重,改进或者做对比实验时候不建议打开，因为用预训练模型整体精度没有很明显的提升
    model.train(data=r'D:\Desktop\YOLOv11\Data.yml',
                imgsz=640,
                epochs=300,
                batch=4,
                workers=0,
                device='',
                optimizer='SGD',
                close_mosaic=10,
                resume=False,
                project='runs/train',
                name='exp',
                single_cls=False,
                cache=False,
                )

"""
参数详解:
    model参数:该参数填入模型配置文件的路径，改进的话建议不需要填预训练模型权重
    data参数:该参数可以填入训练数据集配置文件的路径
    imgsz参数:该参数代表输入图像的尺寸，指定为 640x640 像素
    epochs参数:该参数代表训练的轮数
    batch参数:该参数代表批处理大小，电脑显存越大，就设置越大，根据自己电脑性能设置
    workers参数:该参数代表数据加载的工作线程数，出现显存爆了的话可以设置为0，默认是8
    device参数:该参数代表用哪个显卡训练，留空表示自动选择可用的GPU或CPU
    optimizer参数:该参数代表优化器类型
    close mosaic参数:该参数代表在多少个epoch 后关闭 mosaic 数据增强-次中断的训练状态继续训练。设置为False表示从头开始新的训练。如果设置为True，则会加载上一次训练的模型权重和优化器状态，继续
    resume参数:该参数代表是否从上训练。这在训练被中断或在已有模型的基础上进行进一步训练时非常有用。
    project参数:该参数代表项目文件夹，用于保存训练结果
    name参数:该参数代表命名保存的结果文件夹
    single cls参数:该参数代表是否将所有类别视为一个类别，设置为False表示保留原有类别
    cache参数:该参数代表是否缓存数据，设置为False表示不缓存
"""
```

# 二、模型评估

## 1. Precision  

<img src="https://raw.gitcode.com/NordineGray/PINGO/raw/main/images/20250604232103170.png" style="zoom:50%;" />  

## 2. Recall  

<img src="https://raw.gitcode.com/NordineGray/PINGO/raw/main/images/20250604232138442.png" style="zoom:50%;" />  

## 3. PR  

<img src="https://raw.gitcode.com/NordineGray/PINGO/raw/main/images/20250604232225348.png" style="zoom: 50%;" />  

我应该，用同样的过程，但**不使用预训练权重**，再训练一次，以便于和之后的

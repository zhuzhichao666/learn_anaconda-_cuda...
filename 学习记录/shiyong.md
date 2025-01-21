python detect.py --weights weights/yolov5s.pt --source 0  # 使用 yolov5s.pt

python detect.py --source 0

python detect.py --source ./data/images/ --weights weights/yolov5s.pt --conf 0.4

![image-20250121002846034](C:\Users\wushu\AppData\Roaming\Typora\typora-user-images\image-20250121002846034.png)

你成功运行了 YOLOv5 的目标检测，并且得到了检测结果。根据日志输出，以下是一些信息：

使用了 weights/yolov5s.pt 权重文件。
输入的图片来自 ./data/images/ 目录（包括 bus.jpg 和 zidane.jpg）。
配置了置信度阈值 --conf 0.4，表示只有置信度高于 0.4 的检测结果才会被输出。
结果保存在 runs\detect\exp3 目录中。
输出目录
检测结果保存到了 runs\detect\exp3 目录中。你可以查看该目录，通常会包含以下几种文件和文件夹：

图片结果：检测后的图片通常会被保存为新图片，包含框选出来的目标。
文本文件：如果配置了保存文本结果，会有一个包含检测信息的 .txt 文件（通常按图像名称命名）。
其他输出文件：例如 labels 文件夹，如果你选择保存标签等。



![image-20250121003210425](C:\Users\wushu\AppData\Roaming\Typora\typora-user-images\image-20250121003210425.png)

启动yolov5_env

`cd \.`

`F:`

`cd yolo\yolov5`

`conda activate yolov5_env`




出现了一些问题后

把numpy包安装为

`pip install numpy==1.23.5`
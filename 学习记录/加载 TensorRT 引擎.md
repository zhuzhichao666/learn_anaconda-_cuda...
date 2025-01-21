****

TensorRT构建

cmd

`trtexec --onnx=E:\mx\resnet50-v1-7.onnx --saveEngine=E:\mx\resnet50-v1-7.trt --iterations=100 --warmUp=10 --duration=5`

保存为 `resnet50-v1-7.trt`

**`.trt` 文件** 是通过 **TensorRT** 转换后的优化引擎文件，它包含了一个已经优化和序列化的深度学习模型，专门用于加速推理过程。`.trt` 文件通常用于在 NVIDIA GPU 上进行高效的推理操作。
**推理加速** **减少模型存储和内存消耗**  **跨平台部署** **支持动态批处理** **推理应用**

`.trt` 文件广泛用于各种推理任务，典型应用包括：

- **计算机视觉**：目标检测、图像分类、分割等任务（例如，使用 TensorRT 加速 ResNet、MobileNet、YOLO 等模型）。
- **自然语言处理**：机器翻译、语音识别、文本生成等任务。
- **自动驾驶**：例如，利用 TensorRT 加速自动驾驶中对摄像头图像的实时处理。
- **边缘设备部署**：在移动设备、嵌入式设备上运行深度学习模型，例如 NVIDIA Jetson 系列设备。



例子：

`import tensorrt as trt`
`import numpy as np`
`import cv2`

# `加载 TensorRT 引擎`
`TRT_LOGGER = trt.Logger(trt.Logger.WARNING)`

# `加载 .trt 文件`
`engine_path = "E:/mx/resnet50-v1-7.trt"`
`with open(engine_path, "rb") as f:`
    `engine_data = f.read()`

# `创建 TensorRT runtime`
`runtime = trt.Runtime(TRT_LOGGER)`

# `反序列化引擎`
`engine = runtime.deserialize_cuda_engine(engine_data)`

# `创建执行上下文`
`context = engine.create_execution_context()`

# `加载输入数据（例如图像）`
`input_image_path = "E:/mx/input_image.jpg"`
`image = cv2.imread(input_image_path)`
`image = cv2.resize(image, (224, 224))  # 假设输入是 224x224 图像`
`image = np.transpose(image, (2, 0, 1))  # 转换为 (C, H, W) 格式`
`image = image.astype(np.float32)`
`image = np.expand_dims(image, axis=0)  # 增加 batch 维度`

# `分配内存并将输入数据传递给 GPU`
`input_array = np.asarray(image)`
`output_array = np.empty([1, 1000], dtype=np.float32)  # 假设输出是 1000 类别`

# `获取输入和输出的绑定`
`bindings = []`
`bindings.append(int(input_array.ctypes.data))  # 输入数据指针`
`bindings.append(int(output_array.ctypes.data))  # 输出数据指针`

# `执行推理`
`context.execute_v2(bindings)`

# `输出结果`
`print("Output:", output_array)`

需要安装 TensorRT Python API

`pip install nvidia-pyindex`
`pip install nvidia-tensorrt`


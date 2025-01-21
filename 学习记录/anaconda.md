步骤 1：创建 Anaconda 环境（包含 CUDA 11.7）
由于你需要使用 CUDA 11.7 来支持 GPU 加速，首先你需要创建一个支持 CUDA 11.7 的环境。

创建带有 CUDA 11.7 的 Anaconda 环境（如果你还没有创建环境的话）：

bash
复制代码
`conda create -n yolov5_env python=3.9 cudatoolkit=11.7 -c conda-forge`
这条命令将创建一个新的环境 yolov5_env，并且为其安装支持 CUDA 11.7 的 cudatoolkit。你可以根据需要调整 Python 版本（YOLOv5 推荐使用 Python 3.8 及以上版本）。

激活环境：

bash
复制代码
`conda activate yolov5_env`
这样，你就进入了 yolov5_env 环境。

步骤 2：安装 PyTorch 兼容 CUDA 11.7 版本
YOLOv5 依赖 PyTorch 来进行深度学习训练和推理，而 PyTorch 必须与你的 CUDA 版本兼容。你需要安装适配 CUDA 11.7 的 PyTorch 版本。

安装与 CUDA 11.7 兼容的 PyTorch 版本：

在 Anaconda 环境下，执行以下命令：

bash
复制代码
`conda install pytorch torchvision torchaudio cudatoolkit=11.7 -c pytorch`
这会安装最新版本的 PyTorch、TorchVision、Torchaudio 和与 CUDA 11.7 兼容的工具包。

步骤 3：进入 yolov5 文件夹并安装 YOLOv5 的依赖
进入 yolov5 文件夹（你已经克隆了 YOLOv5，所以直接进入该文件夹）：

bash
复制代码
`cd yolov5`
安装 YOLOv5 所需的 Python 库：

运行以下命令以安装 YOLOv5 所需的依赖项：

bash
复制代码
`pip install -U -r requirements.txt`
这将确保 YOLOv5 的所有必需库（如 opencv, numpy, matplotlib 等）都被正确安装。

步骤 4：验证 GPU 是否正确配置
验证 PyTorch 是否能够检测到 GPU：

你可以通过运行以下命令来确认 PyTorch 是否能正常使用 GPU：

`python`
复制代码
`import torch`
`print(torch.cuda.is_available())  # 如果返回 True，表示 PyTorch 检测到了 GPU`
如果返回 True，说明你的 CUDA 环境和 GPU 设置正确。

![image-20250121172347017](C:\Users\wushu\AppData\Roaming\Typora\typora-user-images\image-20250121172347017.png)

`pip uninstall torch torchvision torchaudio`

or

`conda remove pytorch torchvision torchaudio`

false

`pip install torch==1.13.0+cu117 torchvision==0.14.0+cu117 torchaudio==0.13.0 -f https://download.pytorch.org/whl/torch_stable.html`

测试 YOLOv5 使用 GPU：

你可以尝试运行 YOLOv5 的检测功能，以确保它能正常使用 GPU 进行推理：

bash
复制代码
python detect.py --source 0  # 0 是指默认的摄像头，或者可以替换为图片路径
如果 YOLOv5 成功启动并利用 GPU 进行推理，你会在终端中看到相关的 GPU 使用信息。

总结步骤：
创建并激活带有 CUDA 11.7 的新环境：

bash
复制代码
conda create -n yolov5_env python=3.8 cudatoolkit=11.7
conda activate yolov5_env
安装与 CUDA 11.7 兼容的 PyTorch：

bash
复制代码
conda install pytorch torchvision torchaudio cudatoolkit=11.7 -c pytorch
进入 YOLOv5 文件夹并安装依赖：

bash
复制代码
cd yolov5
pip install -U -r requirements.txt

**这里会出现问题**

你遇到的错误是由于 SSL/TLS 连接问题导致无法通过 HTTPS 连接到 PyPI 获取 Python 包。这种问题通常与网络设置、代理、或者 SSL 证书的验证有关。下面是几个可能的解决方法：

解决方法 1：检查网络连接或代理设置
检查网络连接： 确保你当前的网络连接稳定。如果你在某些网络环境（如公司或学校的网络）中，可能会遇到网络限制，导致 SSL 连接失败。

使用国内镜像源： 如果你在中国大陆，PyPI 访问可能比较慢或不稳定。你可以尝试使用国内的镜像源来安装依赖包，例如使用 清华大学的 PyPI 镜像。

你可以通过以下命令来临时指定 PyPI 镜像源：

bash
复制代码
pip install -U -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
这将使用清华大学的镜像源来下载所需的包，通常能够解决 SSL 连接问题。

解决方法 2：升级 pip 和 setuptools
有时，升级 pip 和 setuptools 可以解决 SSL 证书验证问题。

升级 pip：

bash
复制代码
python -m pip install --upgrade pip
升级 setuptools：

bash
复制代码
pip install --upgrade setuptools
然后再尝试运行 pip install -U -r requirements.txt。

解决方法 3：禁用 SSL 证书验证（不推荐）
虽然不推荐，但在某些情况下，你可以尝试禁用 SSL 证书验证来绕过该问题。可以使用 --trusted-host 参数来临时禁用 SSL 证书验证：

bash
复制代码
pip install -U -r requirements.txt --trusted-host pypi.org --trusted-host pypi.python.org --trusted-host=files.pythonhosted.org
这会强制 pip 忽略 SSL 验证，直接进行包安装。

解决方法 4：手动安装 GitPython
如果问题只出现在 gitpython 包，你可以尝试单独安装该包。

运行以下命令来单独安装 gitpython：

bash
复制代码
pip install gitpython
然后，再运行以下命令安装其它依赖项：

bash
复制代码
pip install -U -r requirements.txt
解决方法 5：检查证书问题
如果你使用的是 Windows 系统，有时可能需要安装额外的 SSL 证书。你可以运行以下命令来安装证书（对于 macOS 用户）：

bash
复制代码
/Applications/Python\ 3.x/Install\ Certificates.command
这通常有助于解决证书问题。

**最后解决办法**

把python版本更换为3.9

`conda create -n yolov5_env python=3.9`

`conda activate yolov5_env`

`pip install -r requirements.txt --trusted-host pypi.mirrors.ustc.edu.cn`
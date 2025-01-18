---
tags:
  - Python
  - Anaconda
  - venv
---

# 1、进入官网

[Anaconda | The Operating System for AI](https://www.anaconda.com/)
下载图形化安装包

# 2、验证安装

```bash
conda --version
```

# 3、初始化设置

为了让Anaconda能够在终端中正常工作，我们需要初始化它，在终端中输入
```bash
conda init zsh  # 如果你使用的是zsh shell
conda init bash  # 如果你使用的是bash shell
```

# 4、创建新环境

以创建paddleOCR虚拟环境为例
```bash
# 创建一个名为paddle_env的新环境，使用Python 3.12.8
conda create -n paddle_env python=3.12.8
```

# 5、激活新创建的环境

```bash
# 激活新创建的环境
conda activate paddle_env
```

# 6、验证环境

在激活环境后，确认一下Python版本

```bash
python --version
```

# 7、常用命令

```bash
# 查看所有环境
conda env list

# 切换环境
conda activate 环境名称

# 退出当前环境
conda deactivate

# 安装包
conda install 包名
```
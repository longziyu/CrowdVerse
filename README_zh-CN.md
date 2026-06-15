# CrowdVerse

<p align="center">
  <a href="README.md">English</a> | <strong>简体中文</strong>
</p>

CrowdVerse 是一个面向多种人群理解任务的大规模数据集与研究平台。本项目将分阶段开放相关数据集、基准代码，以及人群计数、轨迹预测和其他人群分析任务的具体实现。

当前版本主要聚焦于**人群计数**，并提供适配 CrowdVerse 的 APGCC 复现代码。包括轨迹预测代码在内的其他内容将在后续版本中陆续开放。

## 数据集

CrowdVerse 数据集主要包含以下两类视觉数据：

1. **离散图像数据**：由独立采样的人群图像组成，适用于传统的单图像人群计数研究。该部分数据现已开放。
2. **连续帧图像数据**：由时间连续的图像帧序列组成，适用于动态场景下的人群计数和人群分析研究。

### 离散图像数据集下载

离散图像数据集可通过百度网盘下载：

- **下载链接：** [https://pan.baidu.com/s/1b09sZCgSutAMEiaQP74-Sg](https://pan.baidu.com/s/1b09sZCgSutAMEiaQP74-Sg)
- **提取码：** `w2v1`

连续帧数据集及其他研究任务的对应代码将在后续版本中发布。

## 待办事项

- √ 发布离散图像数据集。
- [ ] 发布连续帧图像数据集。
- √ 提供适用于 CrowdVerse 的 APGCC 人群计数复现代码。
- [ ] 发布轨迹预测代码和评测工具。

## 人群计数：APGCC 复现

我们提供了在 CrowdVerse 上复现 APGCC 方法的代码，希望该项目能够支持可复现的实验，并促进人群计数领域的进一步研究。

### 下载

由于 CrowdVerse 数据集及相关代码的体量较大，CrowdVerse 人群计数相关资源和 APGCC 复现代码通过 Google Drive 单独提供：

**[下载 CrowdVerse 人群计数资源包](https://drive.google.com/file/d/1PrgBwJH0S08XLOHs_GiKNYdr8o5zMdFE/view?usp=sharing)**

下载并解压资源包后，请按照以下说明配置运行环境并复现实验结果。

### 环境配置

1. 创建并激活 Conda 环境：

```bash
conda create --name apgcc python=3.8 -y
conda activate apgcc
```

2. 安装项目依赖：

```bash
pip install -r requirements.txt
```

### 推理

使用默认配置在 CrowdVerse 上运行推理：

```bash
cd apgcc
bash test.sh
```

默认情况下，结果将保存至 `./output/`。也可以使用以下命令自定义推理配置：

```bash
python main.py -t -c "${CONFIG}" \
    TEST.WEIGHT "${CHECKPOINT}" \
    OUTPUT_DIR "${OUTPUT_DIR}" \
    TEST.THRESHOLD "${THRESHOLD}"
```

参数说明：

- `CONFIG`：配置文件路径，默认为 `./configs/SHHA_test.yml`。
- `CHECKPOINT`：预训练模型权重路径。
- `OUTPUT_DIR`：推理结果的保存目录。
- `THRESHOLD`：用于过滤预测结果的置信度阈值。

更多配置选项请参见 `./configs/SHHA_test.yml`。

### 训练

在 CrowdVerse 上训练模型：

```bash
cd apgcc
bash train.sh
```

### CrowdVerse 适配说明

为了提高模型对 CrowdVerse 数据集的适应能力，我们主要对以下文件进行了少量调整：

- `main.py`
- `engine.py`
- `configs/` 目录下的配置文件

发布的资源中还包含一些可用于快速复现实验的预处理数据文件。这些文件尚未按照严格的最终分类结构进行整理，但可以直接配合现有脚本使用。

你也可以参考 APGCC 原始实现中的数据预处理流程，使用 `prepare_label.py` 自行预处理数据集。

## 引用

如果 CrowdVerse 对你的研究有所帮助，请引用：

```bibtex
@inproceedings{lai2026crowdverse,
  title={CrowdVerse: A Bidirectional Reality-Calibrated Benchmark for Crowd Understanding and Simulation},
  author={Lai, Pingrui and Zhou, Yanshan and Xie, Zihao and Yang, Hua},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={2197--2207},
  year={2026}
}
```

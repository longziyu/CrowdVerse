# CrowdVerse

CrowdVerse is a large-scale dataset and research platform designed to support crowd understanding across multiple tasks. The project will be released progressively, including datasets, benchmark code, and task-specific implementations for crowd counting, trajectory prediction, and other crowd-analysis tasks.

The current release focuses on **crowd counting** and provides an APGCC reproduction adapted to CrowdVerse. Additional components, including trajectory-prediction code, will be released in future updates.

## Dataset

The CrowdVerse dataset will include two main types of visual data:

1. **Discrete image data**: independently sampled crowd images for conventional image-based crowd counting.
2. **Continuous-frame image data**: temporally continuous frame sequences for studying crowd counting and analysis in dynamic scenes.

These data components will be released progressively alongside the corresponding code for different research tasks.

## To-Do List

- [ ] Release the discrete image dataset.
- [ ] Release the continuous-frame image dataset.
- √ Provide the APGCC crowd-counting reproduction for CrowdVerse.
- [ ] Release trajectory-prediction code and evaluation tools.

## Crowd Counting: APGCC Reproduction

We provide code for reproducing the APGCC method on CrowdVerse. We hope this release will support reproducible experiments and facilitate further research in crowd counting.

### Download

Because the CrowdVerse dataset and associated code are large, the CrowdVerse crowd-counting resources and APGCC reproduction code are provided separately through Google Drive:

**[Download the CrowdVerse crowd-counting package](https://drive.google.com/file/d/1PrgBwJH0S08XLOHs_GiKNYdr8o5zMdFE/view?usp=sharing)**

After downloading and extracting the package, follow the instructions below to set up the environment and reproduce the results.

### Setup

1. Create and activate a Conda environment:

```bash
conda create --name apgcc python=3.8 -y
conda activate apgcc
```

2. Install the required dependencies:

```bash
pip install -r requirements.txt
```

### Inference

To run inference on CrowdVerse using the default settings:

```bash
cd apgcc
bash test.sh
```

By default, the results are saved to `./output/`. You can customize the inference settings with:

```bash
python main.py -t -c "${CONFIG}" \
    TEST.WEIGHT "${CHECKPOINT}" \
    OUTPUT_DIR "${OUTPUT_DIR}" \
    TEST.THRESHOLD "${THRESHOLD}"
```

The arguments are:

- `CONFIG`: path to the configuration file. The default is `./configs/SHHA_test.yml`.
- `CHECKPOINT`: path to the pretrained model checkpoint.
- `OUTPUT_DIR`: directory in which inference results will be saved.
- `THRESHOLD`: confidence threshold used to filter predictions.

For additional configuration options, see `./configs/SHHA_test.yml`.

### Training

To train the model on CrowdVerse:

```bash
cd apgcc
bash train.sh
```

### Adaptation to CrowdVerse

To improve the model's compatibility with CrowdVerse, we made minor adjustments mainly to the following files:

- `main.py`
- `engine.py`
- Configuration files under `configs/`

The released repository also includes several preprocessed dataset files for quick reproduction. These files have not been organized into a strict final classification structure, but they can be used directly with the provided scripts.

Alternatively, you can follow the preprocessing procedure in the original APGCC implementation and use `prepare_label.py` to preprocess the dataset yourself.

## Acknowledgements

This reproduction is based on APGCC. We thank the authors of APGCC for making their work available to the research community.

## Citation

If you find CrowdVerse useful in your research, please cite:

```bibtex
@InProceedings{Lai_2026_CVPR,
  author    = {Lai, Pingrui and Zhou, Yanshan and Xie, Zihao and Yang, Hua},
  title     = {CrowdVerse: A Bidirectional Reality-Calibrated Benchmark for Crowd Understanding and Simulation},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  month     = {June},
  year      = {2026},
  pages     = {2197--2207}
}
```

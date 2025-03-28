# GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing Image Analysis

![GAIA Spatial Coverage](figures/spatial_coverage.png?raw=true)

This repository contains the pre-trained model weights, associated code, and complete dataset of the paper [GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing Image Analysis](https://arxiv.org/abs/2502.09598).

**GAIA** is a large-scale vision-language dataset designed to bridge the gap between remote sensing (RS) imagery and natural language understanding. It provides **205,150 image-text pairs** (41,030 images with 5 synthetic captions each) for advancing RS-specific vision-language models (VLMs). The dataset spans over **25 years** of Earth observations (1998-2024), covering diverse geographic regions, satellite missions, and RS modalities.

If you use this work, please cite our paper:

> Zavras, A., Michail, D., Zhu, X. X., Demir, B., & Papoutsis, I. (2025). [GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing Image Analysis](https://arxiv.org/abs/2502.09598). arXiv preprint arXiv:2502.09598.

```bibtex
@article{zavras2025gaia,
  title={GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing Image Analysis},
  author={Zavras, Angelos and Michail, Dimitrios and Zhu, Xiao Xiang and Demir, Beg{\"u}m and Papoutsis, Ioannis},
  journal={arXiv preprint arXiv:2502.09598},
  year={2025}
}
```

## Dataset Structure 📂
GAIA has been split into **train (70%)**, **test (20%)**, and **validation (10%)** sets, which are spatio-temporally stratified. The dataset splits are provided in JSON files compatible with the img2dataset tool. This approach enables seamless access and reconstruction of the dataset for research purposes. 

Each entry contains a set of web-scraped (i.e. image_src, image_alt, credits) and extracted (i.e. location, tag, resolution, satellite, sensor, modalities) or synthetically-generated data (i.e. lat, lon, captions):
```json
[
  "id", 
  "image_src",
  "image_alt",
  "captions",
  "credits",
  "location",
  "lat",
  "lon",
  "tag",
  "resolution",
  "satellite",
  "sensor",
  "modalities"
]
```

![GAIA Thematic Coverage](figures/categories.png?raw=true)

## Download Instructions ⬇️
To download and reconstruct the GAIA dataset, follow these steps:
- Download the GAIA dataset JSON files from [HuggingFace](https://huggingface.co/datasets/azavras/GAIA).
  ```bash
  huggingface-cli download azavras/GAIA --repo-type dataset --local-dir GAIA
  ```
- Install and use the [img2dataset](https://github.com/rom1504/img2dataset) tool to reconstruct the GAIA dataset.
  ```bash
  img2dataset --url_list "./{split}_data.json" \
              --input_format "json" \
              --url_col "image_src" \
              --caption_col "image_alt" \
              --output_format "webdataset" \
              --save_additional_columns "['id','captions']" \
              --output_folder "./{split}/" \
              --processes_count 4 \
              --thread_count 4 \
              --retries=5 \
              --image_size 512 \
              --encode_format "png" \
              --encode_quality 9 \
              --resize_mode "keep_ratio" \
              --number_sample_per_shard 512 \
              --disallowed_header_directives '[]'
  ```
  ❗ Significantly increasing the **processes_count** and **thread_count** may lead to server overload, potentially causing interruptions and failures in downloads.

  ❗ Some users have reported that **img2dataset** appears to start correctly (with no error messages) but then hangs indefinitely without downloading any samples. We suggest users experiencing this issue to use an **img2dataset** Docker [image](https://hub.docker.com/r/marianna13/spark-img2dataset).

## Pre-trained weights
- Coming soon

## Annotation framework
- Coming soon

## Contributions
We welcome contributions to improve and expand the GAIA dataset. If you have additional RS image-text pair sources or suggestions for enhancing the dataset, please feel free to open an issue.

## Acknowledgements
This work has received funding from the European Union's Horizon Europe research and innovation project ThinkingEarth under grant agreement number 101130544. This work was developed during the research stay of Angelos Zavras at the Remote Sensing Image Analysis (RSiM) Group of the Faculty of Electrical Engineering and Computer Science, Technische Universität Berlin. The research stay grant was awarded by the Short-Term Research Grants program (57693450) of the German Academic Exchange Service (DAAD).

## License
The code in this repository is licensed under the **MIT License**:
```
MIT License

Copyright (c) 2025 Angelos Zavras

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

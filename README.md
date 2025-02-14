# GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing

**GAIA** is a large-scale vision-language dataset designed to bridge the gap between remote sensing (RS) imagery and natural language understanding. It provides **205,150 image-text pairs** (41,030 images with 5 synthetic captions each) for advancing RS-specific vision-language models (VLMs). The dataset spans over **25 years** of Earth observations (1998-2024), covering diverse geographic regions, satellite missions, and RS modalities.

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

## Download Instructions ⬇️
To download and reconstruct the GAIA dataset, follow these steps:
- Download the GAIA dataset JSON files from [HuggingFace](https://huggingface.co/datasets/azavras/GAIA).
- Install and use the [img2dataset](https://github.com/rom1504/img2dataset) tool to reconstruct the GAIA dataset.

For instance, we used the following:
```bash
img2dataset --url_list "./{split}_data.json" \
            --input_format "json" \
            --url_col "image_src" \
            --caption_col "image_alt" \
            --output_format "webdataset" \
            --save_additional_columns "['id','captions']" \
            --output_folder "./{split}/" \
            --processes_count 4 \ # Do NOT increase 
            --thread_count 4 \ # Do NOT increase
            --retries=5 \
            --image_size 512 \
            --encode_format "png" \
            --encode_quality 9 \
            --resize_mode "keep_ratio" \
            --number_sample_per_shard 512 \
            --disallowed_header_directives '[]'
```

## Pre-trained weights
- Coming soon

## Annotation framework
- Coming soon

## Contributions
We welcome contributions to improve and expand the GAIA dataset. If you have additional RS image-text pair sources or suggestions for enhancing the dataset, please feel free to open an issue.

## Citation
If you use the GAIA dataset in your research, please cite our work as follows:
```
@misc{zavras2025gaiaglobalmultimodalmultiscale,
      title={GAIA: A Global, Multi-modal, Multi-scale Vision-Language Dataset for Remote Sensing Image Analysis}, 
      author={Angelos Zavras and Dimitrios Michail and Xiao Xiang Zhu and Begüm Demir and Ioannis Papoutsis},
      year={2025},
      eprint={2502.09598},
      archivePrefix={arXiv},
      primaryClass={cs.CV},
      url={https://arxiv.org/abs/2502.09598}, 
}
```

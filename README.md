# StegaStamp-plus
Improved the original repo, <i>Invisible Hyperlinks in Physical Photographs</i> @tancik, which without datasets and training parameters.

<p align="center">
  <img src="profile.png" alt="Folders in Ubuntu">
</p>

## Features

- Improved training processing;
- Discovered training super-patrameters;
- Provided available training datasets;
- Shell scripts was organized instead of Python;

## Special Acknowledgement

The original author @[tancik](https://github.com/tancik).

## StegaStamp

> ## StegaStamp: Invisible Hyperlinks in Physical Photographs (CVPR 2020) [[Project Page]](http://www.matthewtancik.com/stegastamp)
> **[Matthew Tancik](https://www.matthewtancik.com), [Ben Mildenhall](http://people.eecs.berkeley.edu/~bmild/), [Ren Ng](https://scholar.google.com/citations?hl=en&user=6H0mhLUAAAAJ)**
*University of California, Berkeley*
> ![](https://github.com/tancik/StegaStamp/blob/master/docs/teaser.png)


## Introduction
This repository is a code release for the ArXiv report found [here](https://arxiv.org/abs/1904.05343). The project explores hiding data in images while maintaining perceptual similarity. Our contribution is the ability to extract the data after the encoded image (StegaStamp) has been printed and photographed with a camera (these steps introduce image corruptions). This repository contains the code and pretrained models to replicate the results shown in the paper. Additionally, the repository contains the code necessary to train the encoder and decoder models.

<h2 class="grey-heading">Method</h2>
<h3 class="sub_heading">Deployment</h3>
<div>
	<div class="div-block-5">
	<img src="https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01.png" sizes="(max-width: 767px) 90vw, (max-width: 991px) 728px, 940px" srcset="https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01-p-500.png 500w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01-p-800.png 800w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01-p-1080.png 1080w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01-p-1600.png 1600w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01-p-2000.png 2000w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca3b3c3ca205d53d7e986a1_pipeline-01.png 2407w" alt="" class="stega_pipeline_img"/>
	</div>
	<p class="paragraph-3 stega_text">Our system uses an encoder network to process the input image and hyperlink bitstring into a StegaStamp. The StegaStamp is then printed and captured by a camera. A detection network localizes and rectifies the StegaStamp before passing it to the decoder network. After the bits are recovered and error corrected, the user can follow the hyperlink.</p>
</div>

<h3 class="sub_heading">Training</h3>
<div>
	<div class="div-block-3">
	<img src="https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01.png" sizes="(max-width: 767px) 90vw, (max-width: 991px) 728px, 940px" srcset="https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01-p-500.png 500w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01-p-800.png 800w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01-p-1080.png 1080w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01-p-1600.png 1600w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01-p-2000.png 2000w, https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca400f82e5a6c5707af7189_pipeline_train-01.png 2206w" alt="" class="image-5"/></div><div class="div-block-2"><img src="https://uploads-ssl.webflow.com/51e0d73d83d06baa7a00000f/5ca401582e5a6c3ac8af7332_hidden_4.png" data-w-id="d5da53e4-06cc-85b1-9482-435e4147a949" alt="" class="setga_hidden"/>
	</div>
<p class="paragraph-3 stega_text"> To train the encoder and decoder networks, we simulate the corruptions caused by printing, reimaging, and detecting the StegaStamp with a set of differentiable image augmentations.</p>
</div>

## Citation
If you find our work useful, please consider citing:
```
    @inproceedings{2019stegastamp,
        title={StegaStamp: Invisible Hyperlinks in Physical Photographs},
        author={Tancik, Matthew and Mildenhall, Ben and Ng, Ren},
        booktitle={IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
        year={2020}
    }
```

## Installation
- Clone repo and install submodules
```bash=
git clone --recurse-submodules https://github.com/tancik/StegaStamp.git
cd StegaStamp
```
- Install tensorflow (tested with tf 1.13)
- Python 3 required
- Download dependencies
```bash=
pip install -r requirements.txt
```

## Training
### Encoder / Decoder
- Set dataset path in train.py
```
TRAIN_PATH = DIR_OF_DATASET_IMAGES
```

- Train model
```bash=
bash scripts/base.sh EXP_NAME
```
The training is performed in `train.py`. There are a number of hyperparameters, many corresponding to the augmentation parameters. `scripts/bash.sh` provides a good starting place.

#### Pretrained network
Run the following in the base directory to download the trained network used in paper:
```bash=
wget http://people.eecs.berkeley.edu/~tancik/stegastamp/saved_models.tar.xz
tar -xJf saved_models.tar.xz
rm saved_models.tar.xz
```

### Detector
The training code for the detector model (used to segment StegaStamps) is not included in this repo. The model used in the paper was trained using the BiSeNet model released [here](https://github.com/GeorgeSeif/Semantic-Segmentation-Suite). CROP_WIDTH and CROP_HEIGHT were set to 1024, all other parameters were set to the default. The dataset was generated by randomly placing warped StegaStamps onto larger images.

The exported detector model can be downloaded with the following command:
```bash=
wget http://people.eecs.berkeley.edu/~tancik/stegastamp/detector_models.tar.xz
tar -xJf detector_models.tar.xz
rm detector_models.tar.xz
```

### Tensorboard
To visualize the training run the following command and navigate to http://localhost:6006 in your browser.
```bash=
tensorboard --logdir logs
```

## Encoding a Message
The script `encode_image.py` can be used to encode a message into an image or a directory of images. The default model expects a utf-8 encoded secret that is <= 7 characters (100 bit message -> 56 bits after ECC).

Encode a message into an image:
```bash=
python encode_image.py \
  saved_models/stegastamp_pretrained \
  --image test_im.png  \
  --save_dir out/ \
  --secret Hello
```
This will save both the StegaStamp and the residual that was applied to the original image.

Or run the bash code directly:
```bash=
bash encode_image.sh
```

## Decoding a Message
The script `decode_image.py` can be used to decode a message from a StegaStamp.

Example usage:
```bash=
python decode_image.py \
  saved_models/stegastamp_pretrained \
  --image out/test_hidden.png
```

Samely, or run the bash code directly:
```bash=
bash decode_image.sh
```

## Detecting and Decoding
The script `detector.py` can be used to detect and decode StegaStamps in an image. This is useful in cases where there are multiple StegaStamps are present or the StegaStamp does not fill the frame of the image.

To use the detector, make sure to download the detector model as described in the installation section. The recomended input video resolution is 1920x1080.

```bash=
python detector.py \
  --detector_model detector_models/stegastamp_detector \
  --decoder_model saved_models/stegastamp_pretrained \
  --video test_vid.mp4
```
Add the `--save_video FILENAME` flag to save out the results.

The `--visualize_detector` flag can be used to visualize the output of the detector network. The mask corresponds to the segmentation mask, the colored polygons are fit to this segmentation mask using a set of heuristics. The detector outputs can noisy and are sensitive to size of the stegastamp. Further optimization of the detection network is not explored in this paper.

Samely, or run the bash code directly:
```bash=
bash detector.sh
```

### Detecting and Decoding from Webcam

Just run 

```bash=
bash detector.sh
```

in the terminal.

## Disclaimer

Thanks to the excilent open source work from Matthew Tancik, Ben Mildenhall, et.al !

> Any interest disputes and social consequences arising from using this method have nothing to do with the open source author of this project.

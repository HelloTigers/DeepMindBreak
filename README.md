# DeepMindBreak
*Decensoring Hentai with Deep Neural Networks*

This project applies an implementation of [Globally and Locally Consistent Image Completion](http://hi.cs.waseda.ac.jp/%7Eiizuka/projects/completion/data/completion_sig2017.pdf) to the problem of hentai decensorship. Using a deep fully convolutional neural network, DeepMindBreak can replace censored artwork in hentai with plausible reconstructions. The user needs to only specify the censored regions.

# **THIS PROJECT IS STILL IN DEVELOPMENT. DO NOT BE DISAPPOINTED IF THE RESULTS AREN'T AS GOOD AS YOU EXPECT.**

![Censored, decensored](/readme_images/collage.png)

# Limitations

This project is LIMITED in capability. It is a proof of concept of ongoing research.

The decensorship is intended to ONLY work on color hentai images that have minor bar censorship of the penis or vagina.

It does NOT work with:
- Black and white images
- Monochrome images
- Hentai containing screentones (e.g. printed hentai)
- Real life porn
- Mosaic censorship
- Censorship of nipples
- Censorship of anus
- Animated gifs/videos

In particular, if a vagina or penis is completely censored out, inpainting will be ineffective.

# Dependencies

- Python 2/3
- TensorFlow 1.5
- Pillow
- OpenCV
- tqdm
- scipy
- pyamg
- matplotlib (only for running test.py)

No GPU required! Tested on Ubuntu 16.04 and Windows. (Tensorflow on Windows is compatible with Python 3 and not Python 2.)

Poisson blending is disabled by default since it has little effect on output quality.

Pillow, tqdm, scipy, pyamg, and matplotlib can all be installed using pip.

# Model
Pretrained models can be downloaded from https://drive.google.com/open?id=1KveQ0aaye3tdlB7JR9bFEqMk1Lqp8GyC.

Unzip the contents into the /models/ folder.

# Usage

## I. Decensoring hentai

For each image you want to decensor, using image editing software like Photoshop or GIMP to paint the areas you want to decensor the color (0,255,0), which is a very bright green color.

Save these images in the PNG format to the "decensor_input" directory. Decensor the images by running

```
$ python decensor.py
```

Decensored images will be saved to the "decensor_output" directory.

## II. Train the pretrained model on custom dataset

You must have a GPU for training since training on a CPU will take weeks.

Your custom dataset should be 128 x 128 images of uncensored vaginas and penises cropped from hentai. The more images, the better: I used 70,000 images for training. Censoring these images yourself is unnecessary.

Put your custom dataset for training in the "training_data/images" directory and convert images to npy format.

```
$ cd training_data
$ python to_npy.py
```

To train, run

```
$ python train.py
```

If desired, you can train the pretrained model on your custom dataset by running
```
$ python train.py --continue_training=True
```

Training can be done separately for mosaics with train_mosaic.py, but decensor.py is not yet compatible with mosaic decensorship models.

# To do
- ~~Add Python 3 compatibility~~
- ~~Add random rotations in cropping rectangles~~
- ~~Retrain for arbitrary shape censors~~
- Add a user interface
- Incorporate GAN loss into training
- Update the model to the new version

Contributions are welcome! Special thanks to StartleStars for contributing code for mosaic decensorship and SoftArmpit for greatly simplifying decensoring!

# License

This code is for personal use and research use only.

Example image by dannychoo under [CC BY-NC-SA 2.0 License](https://creativecommons.org/licenses/by-nc-sa/2.0/). The example image is modified from the original, which can be found [here](https://www.flickr.com/photos/dannychoo/16081096643/in/photostream/).

Model is licensed under CC BY-NC-SA 4.0 License.

Code is licensed under CC BY-NC-SA 4.0 License and is modified from tadax's project [Globally and Locally Consistent Image Completion with TensorFlow ](https://github.com/tadax/glcic) and shinseung428's project [https://github.com/shinseung428/GlobalLocalImageCompletion_TF], which are implementations of the paper [Globally and Locally Consistent Image Completion](http://hi.cs.waseda.ac.jp/%7Eiizuka/projects/completion/data/completion_sig2017.pdf). It also has a modified version of parosky's project [poissonblending](https://github.com/parosky/poissonblending).

```
# Copyright (c) 2018, deeppomf. All rights reserved.
#
# This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike
# 4.0 International License. To view a copy of this license, visit
# https://creativecommons.org/licenses/by-nc-sa/4.0/ or send a letter to
# Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.
```

```
# Copyright (c) 2018 tadax, Seung Shin, parosky
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
```

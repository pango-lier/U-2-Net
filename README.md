### Usage for portrait generation
1. Clone this repo to local
```
git clone https://github.com/NathanUA/U-2-Net.git
```

python3.10 -m venv u2net-env
source u2net-env/bin/activate

pip3 install -r requirements.txt

2. Download the u2net_portrait.pth from [**GoogleDrive**](https://drive.google.com/file/d/1IG3HdpcRiDoWNookbncQjeaPN28t90yW/view?usp=sharing) or [**Baidu Pan(提取码：chgd)**](https://pan.baidu.com/s/1BYT5Ts6BxwpB8_l2sAyCkw)model and put it into the directory: ```./saved_models/u2net_portrait/```.

3. Run on the testing set. <br/>
(1) Download the train and test set from [**APDrawingGAN**](https://github.com/yiranran/APDrawingGAN). These images and their ground truth are stitched side-by-side (512x1024). You need to split each of these images into two 512x512 images and put them into ```./test_data/test_portrait_images/portrait_im/```. You can also download the split testing set on [GoogleDrive](https://drive.google.com/file/d/1NkTsDDN8VO-JVik6VxXyV-3l2eo29KCk/view?usp=sharing). <br/>
(2) Running the inference with command ```python u2net_portrait_test.py``` will ouptut the results into ```./test_data/test_portrait_images/portrait_results```. <br/>

4. Run on your own dataset. <br/>
(1) Prepare your images and put them into ```./test_data/test_portrait_images/your_portrait_im/```. [**To obtain enough details of the protrait, human head region in the input image should be close to or larger than 512x512. The head background should be relatively clear.**](https://github.com/NathanUA/U-2-Net) <br/>
(2) Run the prediction by command ```python u2net_portrait_demo.py``` will outputs the results to ```./test_data/test_portrait_images/your_portrait_results/```. <br/>
(3) The difference between ```python u2net_portrait_demo.py``` and ```python u2net_portrait_test.py``` is that we added a simple [**face detection**](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_objdetect/py_face_detection/py_face_detection.html) step before the portrait generation in ```u2net_portrait_demo.py```.  Because the testing set of APDrawingGAN are normalized and cropped to 512x512 for including only heads of humans, while our own dataset may varies with different resolutions and contents. Therefore, the code ```python u2net_portrait_demo.py``` will detect the biggest face from the given image and then crop, pad and resize the ROI to 512x512 for feeding to the network. The following figure shows how to take your own photos for generating high quality portraits.

**(2020-Sep-13)** Our U<sup>2</sup>-Net based model is the **6th** in [**MICCAI 2020 Thyroid Nodule Segmentation Challenge**](https://tn-scui2020.grand-challenge.org/Resultannouncement/).

**(2020-May-18)** The official paper of our **U<sup>2</sup>-Net (U square net)** ([**PDF in elsevier**(free until July 5 2020)](https://www.sciencedirect.com/science/article/pii/S0031320320302077?dgcid=author), [**PDF in arxiv**](http://arxiv.org/abs/2005.09007)) is now available. If you are not able to access that, please feel free to drop me an email.

**(2020-May-16)** We fixed the upsampling issue of the network. Now, the model should be able to handle **arbitrary input size**. (Tips: This modification is to facilitate the retraining of U<sup>2</sup>-Net on your own datasets. When using our pre-trained model on SOD datasets, please keep the input size as 320x320 to guarantee the performance.)

**(2020-May-16)** We highly appreciate **Cyril Diagne** for building this fantastic AR project: [**AR Copy and Paste**](https://github.com/cyrildiagne/ar-cutpaste) using our **U<sup>2</sup>-Net** (Qin *et al*, PR 2020) and [**BASNet**](https://github.com/NathanUA/BASNet)(Qin *et al*, CVPR 2019). The [**demo video**](https://twitter.com/cyrildiagne/status/1256916982764646402) in twitter has achieved over **5M** views, which is phenomenal and shows us more application possibilities of SOD.

## U<sup>2</sup>-Net Results (176.3 MB)

## Required libraries

Python 3.10.12  
numpy 1.15.2  
scikit-image 0.14.0  
python-opencv
PIL 5.2.0  
PyTorch 0.4.0  
torchvision 0.2.1  
glob  

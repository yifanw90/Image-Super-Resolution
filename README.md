# ImageSuperResolution

Implementation of Image Super Resolution CNN in Keras from the paper 
<i><a href="https://arxiv.org/pdf/1501.00092.pdf">Image Super-Resolution Using Deep Convolutional Networks</a></i>

## Model Architecture
![alt tag](https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/SRCNN.png)

This is the simplest model of the ones described in the paper above, consisting of the 9-1-5 model.
Larger architecures can be easily made, but come at the cost of execution time, especially on CPU.

However there are some differences from the original paper:
<br><b>[1]</b> Used the AdaDelta optimizer instead of RMSProp.
<br><b>[2]</b> This model contains some 21,000 parameters, more than the 8,400 of the original paper.

## Usage
The model weights are already provided, therefore simply running :<br>
`python main.py "imgpath"`, where imgpath is a full path to the image.

If the scaling factor needs to be altered then :<br>
`python main.py "imgpath" --scale=s`, where s can be any number. Default s = 2

If the intermediate step (bilinear scaled image) is needed, then:<br>
`python main.py "imgpath" --scale=s --save_intermediate="True"`

If you wish to train the network on your own data set, follow these steps (Performance may drop drasically) :
<br><b>[1]</b> Save all of your input images of any size in the <b>"input_images"</b> folder
<br><b>[2]</b> Open img_utils.py and manually compute the <b>nb_images</b>, located at line 10. 
<br>(nb_images = 400 * number of images in the "input_images" folder)
<br><b>[3]</b> Run img_utils.py function, `transform_images(input_path)`. By default, input_path is input_images path.
<br><b>[4]</b> Open <b>ImageSRModel.py</b> and un-comment the 3 lines at model.fit(...). 
<br><b>Note: It may be usefull to save the original weights in some other location</b>
<br><b>[4]</b> Execute ImageSRModel.py to begin training. GPU is recomended, althoug if small number of images are there then not required.

## Caveats
Very large images may not work with the GPU. Therefore, 
<br>[1] If using Theano, set device="cpu" and cnmem=0.0 in theanorc.txt
<br>[2] If using Tensorflor, set it to cpu mode

## Examples
There are 14 extra images provided in results, 2 of which (Monarch Butterfly and Zebra) have been scaled using both bilinear and SRCNN.

### Monarch Butterfly
Bilinear
<img src="https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/results/monarch_intermediate.bmp" width=25% height=25%> SRCNN
<img src="https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/results/monarch_scaled(2x).bmp" width=25% height=25%>

### Zebra
Bilinear
<img src="https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/results/zebra_intermediate.bmp" width=25% height=25%> SRCNN
<img src="https://raw.githubusercontent.com/titu1994/ImageSuperResolution/master/results/zebra_scaled(2x).bmp" width=25% height=25%>
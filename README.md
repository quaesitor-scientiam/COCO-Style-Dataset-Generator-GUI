# COCO-Style-Dataset-Generator-GUI
This is a simple GUI-based Widget based on matplotlib in Python to facilitate quick and efficient crowd-sourced generation of annotation masks and bounding boxes using a simple interactive User Interface. Optionally, one could choose to use a pretrained Mask RCNN model to come up with initial segmentations. This shifts the work load from painstakingly annotating all the objects in every image to altering wrong predictions made by the system which maybe simpler once an efficient model is learnt.

### REQUIREMENTS:

`Python 3.5+` is required to run the Mask RCNN code. If only the GUI tool is used, `Python2.7` or `Python3.5+` can be used.

#### Installing Dependencies:

Before running the code, install required pre-requisite python packages using pip.

```
pip install -r requirements.txt
```

### RUN THE SEGMENTOR GUI:

Clone the repo.

```
git clone https://github.com/hanskrupakar/COCO-Style-Dataset-Generator-GUI.git
```

#### Running the segmentation GUI without Mask RCNN pretrained predictions:

```
cd COCO-Style-Dataset-Generator-GUI/
python3 segment.py -i images/
```

#### Running the segmentation GUI augmented by initial Mask RCNN pretrained model predictions:

First download the Mask RCNN repo in the same parent directory of COCO-Style-Dataset-Generator-GUI/.

```
git clone https://github.com/hanskrupakar/Mask_RCNN.git
```

To run the particular model for the demo, download the pretrained weights from [HERE!!!](https://drive.google.com/file/d/1S-Wc-tmLDPbtlfje0p9bId20fPHGQNRe/view?usp=sharing). Download and extract pretrained_weights/ into the repository.

```
python3 segment.py -i images -f -p ../Mask_RCNN/ -w pretrained_weights/imagenet_10/mask_rcnn_bags_0006.h5 
```

`USAGE: segment.py [-h] -i IMAGE_DIR [-f] [-p MASKRCNN_DIR] [-w WEIGHTS_PATH]`


##### Optional Arguments 


| Shorthand  | Flag Name | Description |
| ------------- | ------------- | ------------- |
| -h   | --help  | Show this help message and exit |
| -i IMAGE_DIR | --image_dir IMAGE_DIR | Path to the image dir |
| -f | --feedback | Whether or not to include AI feedback |
| -p MASKRCNN_DIR | --maskrcnn_dir MASKRCNN_DIR | Path to Mask RCNN Repo |
| -w WEIGHTS_PATH | --weights_path WEIGHTS_PATH | Path to Mask RCNN checkpoint save file |

### SEGMENTATION GUI CONTROLS:

![deepmagic](https://github.com/hanskrupakar/COCO-Style-Dataset-Generator-GUI/blob/master/gui.png)

In this demo, all the green patches over the objects are the rough masks generated by a pretrained Mask RCNN network. 


  Key-bindings/
    Buttons

   EDIT MODE (when `a` is pressed and polygon is being edited)
   
      'a'       toggle vertex markers on and off.  When vertex markers are on, you can move them, delete them

      'd'       delete the vertex under point

      'i'       insert a vertex at point near the boundary of the polygon.
      
  Left click    click and drag can be used on any point of the polygon to skew the polygon

  REGULAR MODE 
  
    Scroll Up       Zoom into image
    Scroll Down     Zoom out of image
    Right Click     Create a point for a polygon mask around an object
    Left Click      Complete the polygon currently formed by connecting all selected points
  
    SUBMIT          To be clicked after Right click completes polygon! Finalizes current segmentation mask and class label picked. After this, the polygon cannot be edited.
    NEXT            Save all annotations created for current file and move on to next image
    PREV            Goto previous image to re-annotate it. This deletes the annotations created for the file before the current one in order to rewrite the fresh annotations.
    RESET           If when drawing the polygon using points, the polygon doesn't cover the object properly, reset will let you start fresh with the current polygon. This deletes all the points on the image.

The green annotation boxes from the network can be edited by pressing on the Keyboard key `a` when the mouse pointer is on top of a particular such mask. Once you press `a`, the points making up that polygon will show up and you can then edit it using the key bindings specified. Because of the nature of the polygon points being so close to each other, it's easier to delete all the cluttered points at some place of deformation and simply dragging points around to make the image. I suggest not using the insert vertex option `i` as deleting and dragging is just faster. Once you're done editing the polygon, press `a` again to finalize the edits. At this point, it will become possible to submit that particular annotation and move on to the next one.



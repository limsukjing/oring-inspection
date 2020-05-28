# O-ring Inspection

An o-ring is a rubber gasket used in a wide range of ducting and pipework applications, particularly for sealing the junction between two surfaces in liquid or gaseous systems. 

This is a simple Python program designed to inspect images of o-rings for visible defects (e.g. chipped or broken rings) that may have been caused during the manufacturing process. 

![Sample](https://github.com/limsukjing/oring-inspection/blob/master/output.png)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development purposes.

### Prerequisites

If you already have Python 2 or Python 3 installed, you're good to go! If not, install and set up Python 3 on your machine using the packages available [here](https://www.python.org/getit/). Have a look at the following links:

* [Linux/UNIX](https://docs.python.org/3/using/unix.html)
* [macOS](https://docs.python.org/3/using/mac.html)
* [Windows](https://docs.python.org/3/using/windows.html)

### Installing

Use Git from the command line to clone this repo to your local machine:  

```
$ git clone https://github.com/limsukjing/oring-inspection.git
```

To run the main script: 

```
python inspection.py 
```

## Algorithm

1. Read the o-ring images from the `res` folder in a loop. 
2. **Image segmentation:** partition each image into foreground and background using either a histogram-based or a clustering-based thresholding method.
3. **Binary morphology:** perform dilation and erosion to fill interior holes, or generally remove any imperfections in the images.
4. **Connected-component labelling (CCL):** extract the foreground pixels, i.e. pixels belonging to the o-ring and assign unique labels to groups of pixels that are connected. *Use the labels assigned to remove broken pieces.*
5. **Contour detection:** extract contours and generate a bounding box around the labelled o-ring.
6. **Image analysis:** analyze the extracted region to determine whether the o-rings are defective and label them accordingly. 
    - split the o-ring in half vertically and calculate its thickness, i.e. the number of foreground pixels, on each side.
    - in theory, an o-ring should be symmetrical so its thickness on each side must be approximately equal.
    - the o-ring will be classified as failed as long as it's chipped or broken.
7. Add image processing time as an annotation to the output image.

## Built With

* [NumPy](https://numpy.org/) - The fundamental package for scientific computing with Python, which is used to transform images into arrays that can be manipulated.
* [Matplotlib](https://matplotlib.org/) - A comprehensive library for creating static, animated and interactive visualizations in Python.
* [OpenCV](https://opencv.org/) - An open-source Computer Vision library used only for reading `cv2.imread()`, displaying `cv2.imshow()` and annotating `cv2.putText()` the images. *All image processing tasks are done without using OpenCV functions.*

## Author

**Suk Jing Lim** - Please [email](mailto:limsukjing@gmail.com) me if you have any questions.

## Acknowledgement

4th year Computer Vision project supervised by **Dr. Simon McLoughlin**.

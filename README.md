# SIGN_DETECTOR

 The Sign Extractor: Overlapped handwritten signature extraction from scanned documents using OpenCV and scikit-image on python. 

---

**Sample Output**

<p align="center">
  <img src="https://github.com/RechRaj/SIGN_DETECTOR/blob/main/imager.png" | width=750>
</p>

**Explanation:** In this case, the signature extraction algorithm has extracted the signature successfully. Just a very small portion of the signature is lost as this part is not connected with the whole signature line, and hence the algorithm interprets it as a non-signature part.


#### - The pre-version:
<p align="center">
  <img src="https://github.com/RechRaj/SIGN_DETECTOR/blob/main/pre_version.png" | width=450>
</p>

---

**Steps involved:**

- Improvisation of "Outliar Removal" module to boost the signature extraction algorithm.
- Developing CNN based "Signature Recognition" module.
- Developing "Signature Spoofing Detection" algorithm.
- Developing "Signature Detector (bounding box) & Counter" module.
- "Accuracy of detection on [SigSA: On-line Handwritten Signature Database](http://research.sabanciuniv.edu/13568/1/SigDB.pdf)" will be calculated and shared.

---


## Theory

### Main pipe-line

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/47617314-f00c6200-dad6-11e8-8ebf-c45a391b378b.jpg">
</p>

### The logic 
The algorithm extracts the signatures from scanned documents based on "connected component analysis". In image processing, a connected components algorithm finds regions of connected pixels which have the same value.

Thus, the connected components can be found and labelled by a functionality that is provided by scikit-image library. In the scanned documents, if we can get the biggest connected components, we can get the signatures from whole documents. However, since there are undesired lines that also have big connected components, we need a threshold value to get rid of them.

### Calculating the threshold value to get rid of the outliars:

The threshold value to detect the outliars has been calculated (any lines, shapes and texts are not a part of the signatures) via performing many experiments. An equaiton is obtained, which works pretty good for most of the scanned documents which are a4 sized.

**Detect and remove the outliars:**

Here the code parts that start on [rsignextractor.py - line#55](https://github.com/RechRaj/SIGN_DETECTOR/blob/main/rsignextractor.py#L55):

    # experimental-based ratio calculation, modify it for your cases
    # a4_small_size_outliar_constant is used as a threshold value to remove connected outliar connected pixels
    # are smaller than a4_small_size_outliar_constant for A4 size scanned documents
    a4_small_size_outliar_constant = ((average/constant_parameter_1)*constant_parameter_2)+constant_parameter_3
    print("a4_small_size_outliar_constant: " + str(a4_small_size_outliar_constant))

In the equation x stands for scanned document size such as A4 or A0:

- ax_small_size_outliar_constant = ((average/*constant_parameter_1*) * *constant_parameter_2*) + *constant_parameter_3*

It can be modified for other cases and also the for different scanned document size such as A0, A2 and so on. The constants have to be configured to modify:

  - *constant_parameter_1*
  - *constant_parameter_2*
  - *constant_parameter_3*

## Author
Reshma R

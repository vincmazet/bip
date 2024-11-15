# Introduction

A common problem in image processing concerns the detection and localization of certain "objects" in the image.
This corresponds to extracting high-level information that has a meaning for the user, in contrast to low-level information related to pixels.
In the general case, this is a very complicated problem due to the multiplicity of conditions during image acquisition and the variability of the objects themselves:
in such cases, simple methods do not work and (deep) learning methods have to be used.
Conversely, detecting the geometric characteristics (or features) of the objects is easier: for example the contours and corners of the objects or straight lines.
The extreme case is that of an object that is always identically acquired: we then speak of a pattern.
Feature detection is very often a first step for a real application, such as measuring the size of an object,
searching for the presence of a particular object or classifying images.
The detection of patterns, contours, corners, lines or circles is sufficiently well defined to be detected using simple, fast and robust algorithms.
This chapter presents, for these four types of elementary objects, the most effective methods for their detection.
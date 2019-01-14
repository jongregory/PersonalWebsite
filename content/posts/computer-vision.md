---
title: "Azure Computer Vision Services"
date: 2018-08-08T13:54:23Z
draft: false
tags: ["azure","cognitive services","vision"]
---

**Computer Vision**

Computer Vision is a service that provides access to advanced algorithms for image processing via an image upload or an image url. This can enable a website or application to 'understand' images and for them to be integrated into processing or search.


Computer Vision can be accessed via a REST API or a .Net SDK.

The following features are available


- [Image Tagging](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-tagging-images) which returns tags recognised from the image, these tags are set up on the service and not customisable


- [Detecting Objects](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-object-detection) this is similiar to tagging but returns the boundeing box pixel  co-ordinates


- [Categorising Images](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-categorizing-images) this returns a taxonomy of the objects in the image


- [Describing Images](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-describing-images) returns a human readable description of the image along with a tag list of object


- [Detecting Faces](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-detecting-faces) locates a face in an image and returns information on gender, age and emotion.


- [Detecting Image Types](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-detecting-image-types) detects if an image is clip art or a line drawing


- [Domain Specific Content Detection](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-detecting-domain-content) detects domain specific objects, Landmarks and Celebraties are the two current built in domains.


- [Detect Colour Schemes](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-detecting-color-schemes) returns the dominant foreground and background colours, supports twelve accent colours.


- [Generating thumbnails](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-generating-thumbnails) uses smart cropping to generate a thumbnail of the area of interest


- [Extracting text with OCR](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-extracting-text-ocr)  pulls text from an image and supports 25 languages


- [Recognising Text](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-recognizing-text) detects and extracts handwritten or printed text, this is designed to work with different objects and surfaces not just documents


- [Detecting Racy Content](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/concept-detecting-adult-content) detects content in and Image which is either racey or adult.

**Containers**

The text recognition function is available as a docker container which can be deployed in a container with your applications. [https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/computer-vision-how-to-install-containers](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/computer-vision-how-to-install-containers)

**Summary**

As with all azure cognitive services Computer Vision can be used easily via HTTP web service calls or an SDK and quickly added to a website or an application. The benefits can be huge compared to effort expended as images can become an integral part of an application, being categorised or indexed for example to provide a integrated search.


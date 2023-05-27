# DL-2023-VirTex-implementation

Implementation of paper "VirTex: Learning Visual Representations from Textual Annotations" 
https://openaccess.thecvf.com/content/CVPR2021/papers/Desai_VirTex_Learning_Visual_Representations_From_Textual_Annotations_CVPR_2021_paper.pdf

Idea: creation of pretrained ResNet50 model (obtaining high quality image representations) for further usage on different downstream CV tasks 
(such as image classification, object detection, semantic segmentation) - with the pretraining task being image captioning.

The authors claim that such a pretraining task is much more informative than many other pretraining tasks (like image classification used for 
classic ResNet50 pretraining on ImageNet dataset) - because it contains a lot of information about the image - objects, their relations, features, etc.
The claim is that using such a superior pretraining task as image captioning, it is possible to pretrain ResNet on a smaller dataset (like COCO with some 118K images)
so that it will provide a comparable (or even better!) performance on downstream tasks relative to the classic ResNet50 pretrained on ImageNet (14M pictures).

The model trained (named VirTex) has two parts - visual encoder (ResNet50[:-2] architecture, which is actually the target model) and textual classic Transformer decoder.

I implemented this architecture and trained VirTex on two subsets of COCO (10K and 30K images) - with maximum of 20 iterations for 30K images.
And then used the VirTex visual part for image segmentation on CelebA subset. For comparison, I did the same image segmentation with the classic pretrained ResNet50.
The VirTex works very badly in my case - if at all. I guess a lot more iterations are needed - and on a larger dataset. 
The authors trained VirTex on the full COCO (118K images), for some 500K iterations.

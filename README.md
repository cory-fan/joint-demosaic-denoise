# Efficient Joint Demosaicing and Denoising with Downsampled Isotropic Networks

A very simple writeup of the key idea of this project.

A key split in the field of Image Restoration is the existence of two broad macro-architectures: firstly, U-Net (such as Restormer), and second, what I am terming isotropic networks, but include the networks categorized as Residual-in-Residual (such as RCAN or NAFSSR). 

U-Net likely does not need introduction, but isotropic networks here refers to networks that have a uniform resolution among its network body, and do not perform upsampling/downsampling except at the beginning/end of the network. ViT is a famous example of this type of network. In Image Restoration, isotropic networks seek to capture the highly-detailed nature of image restoration tasks and thus tend not to perform *any* downsampling, instead performing calculations only on the full spatial resolution of the input image. This acheives good performance on certain tasks, especially super-resolution.

However, I argue that this is antithetical to many empirical observations about image processing, specifically that images tend to be compressible (especially, I refer to the DeepMAD paper). Specifically, employing DeepMAD's Principle of Maximum Entropy and formula for Normalized Gaussian Entropy Upper Bound (acknowledging its heuristical nature), we can show that in most networks of reasonable size (suppose loosely > 1 GMACs for denoising on 256x256 px image), performing downsampling can actually increase the entropy of the network, implying a greater degree of expressiveness. Thus inspires the design of my networks.

I apply this observation to the task of Joint Demosaicing and Denoising (largely because experiments on denoising-only datasets have a tendency to be prohibitively expensive for my personal budget), specifically the Hard Demosaicing Dataset introduced here (https://arxiv.org/html/2504.07145v1).

![Alt text](hddresults.png?raw=true "Title")

Above is the HDD results. Mine and Mine(S) (the small variant) are my models. Green is best performance, yellow is second best performance. The dashes in some of the FLOPs are because I haven't gotten around to calculating their FLOPs yet.

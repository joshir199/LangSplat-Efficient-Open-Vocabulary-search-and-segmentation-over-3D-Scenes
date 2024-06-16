# LangSplat : An Efficient Open Vocabulary search and segmentation over 3D Scenes
A multi-modal network to do open vocabulary search and semantic segmentation over 3D scenes.
This method requires calibrated single or multi-view images.

Original paper : https://arxiv.org/abs/2312.16084

--------------------
# Architecture 

![](https://github.com/joshir199/LangSplat-Efficient-Open-Vocabulary-search-and-segmentation-over-3D-Scenes/blob/main/images/Langsplat_architecture.png)


--------------
# Previous Models and limitations
LERF use feature distillation from vision-language models like CLIP into 3D scenes.
1. Speed Limitations:
     Computationally expensive rendering speeds.
3. Accuracy Issues:
     Ambiguity in CLIP embeddings which are aligned with images rather than individual pixels.



********************************
# Advantages of using Langsplat

LangSplat aims to address the limitations of current methods (like LeRF) by introducing 3D Language Gaussian Splatting, which incorporates the following innovations:

1. 3D Representation:
        Gaussian Splatting: Instead of using NeRF for 3D representation, LangSplat represents a 3D scene as a collection of 3D Gaussians. This allows for efficient rendering at high resolutions using tile-based 
        splatting.

2. Language Embeddings:
        Each 3D Gaussian is enhanced with a language embedding.
        These embeddings are supervised using CLIP embeddings extracted from image patches captured from multiple training views to ensure multi-view consistency.

3. Memory Efficiency:
        High-dimensional (d = 512) language embeddings are memory-intensive. To mitigate this, LangSplat employs a scene-wise language autoencoder to map CLIP embeddings to a low-dimensional latent space (d = 3).
        This approach reduces memory costs and improves rendering efficiency.

4. Addressing Point Ambiguity:
        LangSplat uses the semantic hierarchy defined by the Segment Anything Model (SAM) to tackle the point ambiguity issue.
        For each 2D image, SAM provides well-segmented maps at three semantic levels. CLIP features are extracted for each segmented mask, and these features are assigned to corresponding points in the 3D 
        scene. This results in precise CLIP embeddings for each point, enhancing model accuracy.

5. Accuracy
        The use of SAM-based masks ensures precise object boundaries in the 3D language field, resulting in higher accuracy and clearer 3D language features.


As per mentioned in the research paper, LangSplat is extremely efficient, achieving a 199 × speedup compared to LERF at the resolution of 1440 × 1080.


![](https://github.com/joshir199/LangSplat-Efficient-Open-Vocabulary-search-and-segmentation-over-3D-Scenes/blob/main/images/langsplat_and_lerf_result_comparison.png)

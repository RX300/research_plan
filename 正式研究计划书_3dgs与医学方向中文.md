# 研究テーマ

本研究的主题是探索一种基于3D高斯溅射（3DGS）技术的新型医疗数据三维可视化方案。该方案旨在利用3DGS技术实现医疗数据的高保真实时渲染，并构建一个支持交互式分割的系统，以精确区分并操作不同的组织结构或病灶区域。

# 研究背景

近年来，3D高斯溅射（3DGS）作为可微分渲染领域的突破性技术，显著提升了渲染的质量与效率。该技术通过与人工智能结合，已在3D内容生成等前沿领域成为关键技术，其高精度、高效率的特性，也为医疗数据可视化带来了巨大的应用潜力。

在临床实践中，对CT、MRI等三维医疗数据的精确可视化至关重要。然而，传统方法难以兼顾渲染细节的保真度与实时交互性能。3DGS技术凭借其照片级的真实感与前所未有的渲染速度，为解决这一长期存在的技术瓶颈提供了新的契机。

然而，将3DGS直接应用于医疗领域仍面临以下挑战：

* **定量准确性** ：标准3DGS侧重于视觉效果，无法保证渲染结果在物理意义上（如CT值）的准确性。
* **实时交互性** ：临床应用需要对数据进行实时的剖切（Clipping）和探索，而原生3DGS缺乏对此类交互的直接支持。
* **语义理解** ：模型仅有几何与外观信息，不足以支持诊断，需要被赋予识别和分割特定组织或病灶（如肿瘤）的能力。

目前，虽已有研究在上述各方向上取得初步成果，但仍缺少一个能将三者有效集成的统一解决方案。因此，本研究旨在提出并实现一个包含了实时交互与智能分割功能的新型医疗数据可视化框架。

# 研究方法

本研究将融合多个前沿方向的技术，构建一个综合性的医疗数据处理框架，并且探索如何更有效率的利用3dgs推进医疗数据可视化。

1. 构建高保真三维高斯表达

   本研究将改进标准3DGS框架，引入基于物理的渲染模型。具体而言，将借鉴R²-Gaussian等工作的思想，在渲染管线中校正积分偏差，确保渲染结果能够忠实地反映CT或MRI数据背后的物理测量值，为定量分析提供坚实基础 [`<sup>`3 `</sup>`](#refer-anchor-3) 。此外，将探索多模态数据融合技术，结合CT与MRI等不同成像方式的信息，提升模型对复杂解剖结构的表达能力 。
2. 实现实时交互式剖切与探索

   为满足临床探索需求，本研究将参考ClipGS等方法的思路，为每个三维高斯体引入可学习的剖切属性 。通过设计一个轻量级的神经网络，使其能够根据用户定义的任意剖切平面，实时判断并调整高斯体的可见性与形态，从而在不牺牲渲染质量的前提下，实现流畅的内部结构观察 。
3. 集成基于语义的交互式分割

   为实现对特定组织的智能识别与分割，本研究将为每个高斯体额外嵌入一个高维的语义特征向量。借鉴SurgTPGS等工作的启发，该特征将通过预训练的视觉语言模型（VLM）或分割模型（SAM）进行监督学习 。在交互阶段，用户仅需通过简单的点击或文本提示，系统即可利用这些语义特征，通过点云分割网络等算法，在三维高斯空间中直接、快速地完成对目标区域的精确分割 。

# 研究計画

修士一年生第一学期：研究方法に記載された内容に基づき、まず分野内の最新の進捗状況を調査し、その後、実験用のコードフレームワークを構築して実験を開始する。

修士一年生第二学期：実験結果に基づき、より良い結果を得るために異なる手法を試行し、実験を行う。並行して論文の執筆を開始する。

修士M2第一学期：学術会議またはジャーナルへの投稿を開始し、フィードバック結果に基づき、論文と実験方法のさらなる改善を行う。

修士M2第二学期：卒業論文の執筆を開始する。

# 参考文献

<div id="refer-anchor-1"></div>
[1] Kerbl, B., Kopanas, G., Leimkühler, T., & Drettakis, G. (2023). 3D Gaussian splatting for real-time radiance field rendering. ACM Trans. Graph., 42(4), 139-1.

<div id="refer-anchor-2"></div>
[2] He, S., Ji, P., Yang, Y., Wang, C., Ji, J., Wang, Y., & Ding, H. (2025). A Survey on 3D Gaussian Splatting Applications: Segmentation, Editing, and Generation. arXiv preprint arXiv:2508.09977.

<div id="refer-anchor-3"></div>
[3] Jiang, Y., Yu, C., Xie, T., Li, X., Feng, Y., Wang, H., ... & Jiang, C. (2024, July). Vr-gs: A physical dynamics-aware interactive gaussian splatting system in virtual reality. In ACM SIGGRAPH 2024 Conference Papers (pp. 1-1).

<div id="refer-anchor-4"></div>
[4] Macklin, M., Müller, M., & Chentanez, N. (2016, October). XPBD: position-based simulation of compliant constrained dynamics. In Proceedings of the 9th International Conference on Motion in Games (pp. 49-54).

<div id="refer-anchor-5"></div>
[5] Tu, X., Radl, L., Steiner, M., Steinberger, M., Kerbl, B., & de la Torre, F. (2025). VRSplat: Fast and Robust Gaussian Splatting for Virtual Reality. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 8(1), 1-22.

<div id="refer-anchor-6"></div>
[6] Wang, S., Leroy, V., Cabon, Y., Chidlovskii, B., & Revaud, J. (2024). Dust3r: Geometric 3d vision made easy. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 20697-20709).

<div id="refer-anchor-7"></div>
[7] Wu, X., Jiang, L., Wang, P. S., Liu, Z., Liu, X., Qiao, Y., ... & Zhao, H. (2024). Point transformer v3: Simpler faster stronger. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 4840-4851).

<div id="refer-anchor-8"></div>
[8] Müller, T., Rousselle, F., Novák, J., & Keller, A. (2021). Real-time neural radiance caching for path tracing. arXiv preprint arXiv:2106.12372.

<div id="refer-anchor-9"></div>
[9] Lee, J. C., Rho, D., Sun, X., Ko, J. H., & Park, E. (2024). Compact 3d gaussian splatting for static and dynamic radiance fields. arXiv preprint arXiv:2408.03822.

<div id="refer-anchor-10"></div>
[10] Papantonakis, P., Kopanas, G., Kerbl, B., Lanvin, A., & Drettakis, G. (2024). Reducing the memory footprint of 3d gaussian splatting. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 7(1), 1-17.

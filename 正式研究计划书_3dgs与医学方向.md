# 研究テーマ

本研究のテーマは「3D Gaussian Splattingに基づく医用データの3次元可視化」です。本手法は、3DGS技術を用いて医用データの高忠実度なリアルタイムレンダリングを実現するとともに、異なる組織構造や病変領域を正確に区別し操作するための、interactive segmentationをサポートするシステムの構築を目的とします。

# 研究背景

近年、 **3D Gaussian Splatting** （3DGS）[`<sup>`1`</sup>`](#refer-anchor-1)は、微分可能レンダリングの分野における画期的な技術として、レンダリングの品質と効率を著しく向上させました。本技術は人工知能との融合により、3Dコンテンツ生成といった最先端分野で基盤技術となっており、その高精度・高効率という特性は、医用データの可視化においても大きな応用ポテンシャルを示しています。

臨床現場において、CTやMRIのような3次元医用データの正確な可視化は極めて重要です[`<sup>`2`</sup>`](#refer-anchor-2)。しかしながら、従来の手法では、レンダリングの忠実度とリアルタイムなインタラクション性能を両立させることは困難でした[`<sup>`3`</sup>`](#refer-anchor-3)。3DGS技術は、そのフォトリアルな品質と未だかつてないレンダリング速度により、この長年の技術的ボトルネックを解決する新たな契機を提供します。

しかし、3DGSを直接医療分野に応用するには、以下の課題が存在します。

* **定量的正確性** ：標準的な3DGSは視覚的な美しさを重視するため、レンダリング結果が物理的な意味（例えばCT値）において正確であるという保証はありません。
* **リアルタイムな インタラクティブ 性** ：臨床応用ではリアルタイムでのData Clippingや探索が求められますが、ネイティブの3DGSはこのようなインタラクションを直接サポートしていません。
* **セマンティック理解** ：幾何情報と外観情報だけでは診断を支援するには不十分であり、モデルに特定の組織や病変（例えば腫瘍）を識別し、セグメンテーションする能力を付与する必要があります。

現在、これらの各方向で初期的な成果を上げた研究は存在するものの、三者を効果的に統合した統一的なソリューションはまだ存在しません。そこで本研究では、リアルタイムなインタラクションとインテリジェントなセグメンテーション機能を備えた、新しい医用データ可視化フレームワークを提案し、実装することを目指します。

# 研究方法

本研究は、複数の最先端分野の技術を融合し、包括的な医用データ処理フレームワークを構築するとともに、3D Gaussian Splatting (3DGS) をより効率的に活用して医用データの可視化を推進する方法を探求します。

1. 高忠実度な3次元画面表現の構築

本研究では、標準的な3DGSフレームワークを改良し、物理ベースのrendering modelを導入します[`<sup>`4`</sup>`](#refer-anchor-4)。具体的には、R²-Gaussian[`<sup>`5`</sup>`](#refer-anchor-5)などの研究に着想を得て、rendering pipelineにおける積分バイアスを補正し、レンダリング結果がCTやMRIデータの背後にある物理的な測定値を忠実に反映できるようにすることで、定量的分析のための強固な基盤を提供します。さらに、multimodal data融合技術を探求し[`<sup>`6`</sup>`](#refer-anchor-6)、CTとMRIといった異なる撮像方式の情報を組み合わせることで、モデルの複雑な解剖学的構造に対する表現能力を向上させます。

2. リアルタイムなclipping と探索の実装

臨床的な探索のニーズに応えるため、本研究ではClipGS[`<sup>`7`</sup>`](#refer-anchor-7)などの手法の着想を参考に、各3Dガウシアンに学習可能な clipping属性を導入します。ユーザーが定義した任意のclipping平面に基づき、ガウスの可視性や形状をリアルタイムに判断・調整する軽量な neural networkを設計することで、レンダリング品質を損なうことなく、内部構造の滑らかな観察を実現します。

3. semantics に基づく interactive segmentation の統合

特定組織のインテリジェントな識別とsegmentationを実現するため、本研究では各ガウシアンに追加で高次元のsemantic feature vectorを埋め込みます。SurgTPGS[`<sup>`8`</sup>`](#refer-anchor-8)などの研究から着想を得て、この特徴は事前学習済みのVision-Language Model (VLM)[`<sup>`9`</sup>`](#refer-anchor-9)や Segmentation Model (SAM)を介した教師あり学習によって獲得されます。interaction段階では、ユーザーが簡単なクリックや text promptを行うだけで、システムはこれらのセマンティック特徴を利用し、point cloud segmentation network[`<sup>`10`</sup>`](#refer-anchor-10)などのアルゴリズムを用いて、3D空間内で直接的かつ高速に対象領域の精密な segmentationを完了させます。

# 研究計画

修士一年生第一学期：研究方法に記載された内容に基づき、まず分野内の最新の進捗状況を調査し、その後、実験用のコードフレームワークを構築して実験を開始する。

修士一年生第二学期：実験結果に基づき、より良い結果を得るために異なる手法を試行し、実験を行う。並行して論文の執筆を開始する。

修士M2第一学期：学術会議またはジャーナルへの投稿を開始し、フィードバック結果に基づき、論文と実験方法のさらなる改善を行う。

修士M2第二学期：卒業論文の執筆を開始する。

# 参考文献

<div id="refer-anchor-1"></div>
[1] Kerbl, B., Kopanas, G., Leimkühler, T., & Drettakis, G. (2023). 3D Gaussian splatting for real-time radiance field rendering. ACM Trans. Graph., 42(4), 139-1.

<div id="refer-anchor-2"></div>
[2] JohnsonChris, R. (2022). A review of three-dimensional medical image visualization. Health Data Science.

<div id="refer-anchor-3"></div>
[3] Papantonakis, P., Kopanas, G., Kerbl, B., Lanvin, A., & Drettakis, G. (2024). Reducing the memory footprint of 3d gaussian splatting. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 7(1), 1-17.

<div id="refer-anchor-4"></div>
[4] Kajiya, J. T. (1986, August). The rendering equation. In Proceedings of the 13th annual conference on Computer graphics and interactive techniques (pp. 143-150).

<div id="refer-anchor-5"></div>
[5] Zha, R., Lin, T. J., Cai, Y., Cao, J., Zhang, Y., & Li, H. (2024). R $^ 2$-Gaussian: Rectifying Radiative Gaussian Splatting for Tomographic Reconstruction. arXiv preprint arXiv:2405.20693.

<div id="refer-anchor-6"></div>
[6] Wei, Z., Lin, J., Liu, Y., Chen, W., Luo, J., Li, G., & Lin, L. (2025). 3DAffordSplat: Efficient Affordance Reasoning with 3D Gaussians. arXiv preprint arXiv:2504.11218.

<div id="refer-anchor-7"></div>
[7] Li, C., Tong, Y., Chen, K., Yang, Z., Li, R., Qiu, S., ... & Dou, Q. (2025, September). ClipGS: Clippable Gaussian Splatting for Interactive Cinematic Visualization of Volumetric Medical Data. In International Conference on Medical Image Computing and Computer-Assisted Intervention (pp. 127-137). Cham: Springer Nature Switzerland.

<div id="refer-anchor-8"></div>
[8] Huang, Y., Bai, L., Cui, B., Yuan, K., Wang, G., Hoque, M. I., ... & Ren, H. (2025, September). SurgTPGS: Semantic 3D Surgical Scene Understanding with Text Promptable Gaussian Splatting. In International Conference on Medical Image Computing and Computer-Assisted Intervention (pp. 584-594). Cham: Springer Nature Switzerland.

<div id="refer-anchor-9"></div>
[9] Shinde, G., Ravi, A., Dey, E., Sakib, S., Rampure, M., & Roy, N. (2025). A Survey on Efficient Vision‐Language Models. Wiley Interdisciplinary Reviews: Data Mining and Knowledge Discovery, 15(3), e70036.

<div id="refer-anchor-10"></div>
[10] Qu, Y., Chen, D., Li, X., Li, X., Zhang, S., Cao, L., & Ji, R. (2025, August). Drag your gaussian: Effective drag-based editing with score distillation for 3d gaussian splatting. In Proceedings of the Special Interest Group on Computer Graphics and Interactive Techniques Conference Conference Papers (pp. 1-12).

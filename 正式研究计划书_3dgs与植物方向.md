# 研究テーマ

本研究は、植物の精細構造における高忠実度な再構成を目的とし、3D Gaussian Splatting（3DGS）技術の最適化を目指す。

研究目標は、標準的な3DGSを植物（微細な葉、葉脈、茎、穂など）に適用する際に生じる、幾何学的なぼけ、エッジの欠損（穴）、および「浮遊物」（floaters）アーティファクトといった問題を専門的に解決することにある。本研究は、植物の表現型解析（フェノタイピング）に適した、ロバストで高精度な3D再構成パイプラインを開発することに専念する。

# 研究背景

3DGS [<sup>1</sup>] は、3D再構成の主流技術となっている。植物科学の分野では、"Splanting" [<sup>2</sup>]や小麦の再構成に関する研究 [<sup>3</sup>] に代表されるように、3DGSが植物の複雑な形態を捉える上でNeRFを顕著に上回る潜在能力を持つことが証明されている。

しかし、植物の表現型解析は、幾何学的な精度に対して極めて高い要求を持つ。既存の3DGS手法を、高周波ディテールと薄い構造（thin structures）を持つ植物のような対象に適用する際、その限界は依然として明らかである。

初期化への依存性： 標準的な3DGSは、初期化を疎なSfM（Structure from Motion）[<sup>4</sup>]点群に依存している。テクスチャが乏しい、あるいは半透明な葉に対しては、SfMは十分な初期点を生成することが難しく、その後の最適化が「根拠なし」に進むことになる。

汎用的なサンプリング戦略： 3DGSの密生化（Densification）戦略は汎用的であるため、葉の縁のような薄い構造部では、誤ってガウス球を複製し「浮遊物」アーティファクトを生成しやすい。同時に、シャープで連続的な幾何学的エッジの再構成も困難であり、しばしばぼけや穴として現れる[<sup>5</sup>]。

したがって、3DGSのサンプリングと最適化プロセスを改善し、植物の精細構造を「知覚」できるようにすることが、本研究が解決すべき核心的な問題である。

# 研究方法

本研究計画は、幾何学的プライア（事前情報）、適応的サンプリング、および幾何学的正則化の3つの側面から、標準的な3DGSパイプラインの最適化を行う。

1. 密な幾何学的プライアに基づく初期化戦略

   MVS（Multi-View Stereo）[<sup>6</sup>]アルゴリズムによって生成された密な点群を、3DGSの幾何学的プライアとして利用する方法を研究する。これらの信頼性の高い密な幾何情報（法線と位置を含む）をガウス球の初期化段階に組み込み[<sup>7</sup>]、精細構造の再構成のためにより質の高い出発点を提供する方法を探求する。
2. エッジ保持のための適応的密生化

   標準的な3DGSの密生化（Densification）および枝刈り（Pruning）戦略を改善する方法を研究する[<sup>8</sup>]。画像領域の高周波情報（ラプラシアンエッジや深度マップの勾配など[<sup>9</sup>]）を利用してガウス球の分裂を誘導し、葉脈や葉の縁などの重要な領域で適応的に密度を高め、同時に何もない領域での無効な分裂を抑制する方法を探求する。
3. 薄い構造のための幾何学的正則化

   ガウス球の幾何学的形態を最適化するために、新しい損失関数または制約項を導入することを研究する。（例えば、葉の表面のガウス球をより「扁平」にすることを奨励したり、透明度の分布を制約したりするなど）「浮遊物」アーティファクトを専門的に抑制し、再構成された葉の表面をより滑らかに、エッジをよりシャープにするための正則化手法[<sup>10</sup>]を探求する。

# 研究計画

修士M1第一学期：研究方法に記載された内容に基づき、まず分野内の最新の進捗状況を調査し、その後、実験用のコードフレームワークを構築して実験を開始する。

修士M1第二学期：実験結果に基づき、より良い結果を得るために異なる手法を試行し、実験を行う。並行して論文の執筆を開始する。

修士M2第一学期：学術会議またはジャーナルへの投稿を開始し、フィードバック結果に基づき、論文と実験方法のさらなる改善を行う。

修士M2第二学期：卒業論文の執筆を開始する。

# 参考文献

<div id="refer-anchor-1"></div>
[1] Kerbl, B., Kopanas, G., Leimkühler, T., & Drettakis, G. (2023). 3D Gaussian splatting for real-time radiance field rendering. ACM Trans. Graph., 42(4), 139-1.

<div id="refer-anchor-2"></div>
[2] Ojo, T., La, T., Morton, A., & Stavness, I. (2024). Splanting: 3d plant capture with gaussian splatting. In SIGGRAPH Asia 2024 Technical Communications (pp. 1-4).

<div id="refer-anchor-3"></div>
[3] Stuart, L. A., Wells, D. M., Atkinson, J. A., Castle-Green, S., Walker, J., & Pound, M. P. (2025). High-fidelity wheat plant reconstruction using 3D Gaussian splatting and neural radiance fields. GigaScience, 14, giaf022.

<div id="refer-anchor-4"></div>
[4] Schonberger, J. L., & Frahm, J. M. (2016). Structure-from-motion revisited. In Proceedings of the IEEE conference on computer vision and pattern recognition (pp. 4104-4113).

<div id="refer-anchor-5"></div>
[5] Li, J., Qi, X., Nabaei, S. H., Liu, M., Chen, D., Zhang, X., ... & Li, Z. (2025). A survey on 3D reconstruction techniques in plant phenotyping: from classical methods to neural radiance fields (NeRF), 3D Gaussian splatting (3DGS), and beyond. arXiv preprint arXiv:2505.00737.

<div id="refer-anchor-6"></div>
[6] Schönberger, J. L., Zheng, E., Frahm, J. M., & Pollefeys, M. (2016, September). Pixelwise view selection for unstructured multi-view stereo. In European conference on computer vision (pp. 501-518). Cham: Springer International Publishing.

<div id="refer-anchor-7"></div>
[7] Liang, Z., Zhang, Q., Feng, Y., Shan, Y., & Jia, K. (2024). Gs-ir: 3d gaussian splatting for inverse rendering. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 21644-21653).

<div id="refer-anchor-8"></div>
[8] Deng, X., Diao, C., Li, M., Yu, R., & Xu, D. (2025). Improving Densification in 3D Gaussian Splatting for High-Fidelity Rendering. arXiv preprint arXiv:2508.12313.

<div id="refer-anchor-9"></div>
[9] Kung, P. C., Isaacson, S., Vasudevan, R., & Skinner, K. A. (2024). Sad-gs: Shape-aligned depth-supervised gaussian splatting. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 2842-2851).

<div id="refer-anchor-10"></div>
[10] Shi, D., Wang, W., Chen, D. Y., Zhang, Z., Bian, J. W., Zhuang, B., & Shen, C. (2025). Revisiting Depth Representations for Feed-Forward 3D Gaussian Splatting. arXiv preprint arXiv:2506.05327.

# 研究テーマ

本研究は、3D Gaussian Splatting (3DGS) とバーチャルリアリティ (VR) 領域を深く統合し、高効率かつ高忠実度なVRシーンの表現とレンダリング手法を探索することで、没入型インタラクション体験の発展を推進することを目的とします。

研究目標は、VRシーンにおける3DGSのリアルタイムレンダリング性能を向上させるだけでなく、点群の編集可能性と動的な相互作用を実現し、ユーザーが仮想環境で三次元オブジェクトを自然に操作・変更できるようにすることを含みます。この方向性の研究を通じて、現在のVRシーンで存在するフリッカー（ちらつき）や高計算コストといったボトルネックを打破し、3DGSの没入型アプリケーションへの大規模な実装を目指します。

# 研究背景

近年、3DGS[<sup>1</sup>](#refer-anchor-1)のような新興技術の発展に伴い、微分可能レンダリグの品質と効率が著しく向上しています。3DGSは、従来のボリュームレンダリングを基盤とし、その微分可能性と勾配降下法を利用してシーンを表現する3Dガウシアン群を最適化することで、 高品質な新視点画像合成を実現します 。同時に、人工知能の急速な進歩も、3DGSとニューラルネットワークの結合を加速させています，その応用を3Dコンテンツ生成、シーンの編集、動的なデジタルヒューマンといった複数[<sup>2</sup>](#refer-anchor-2)の最先端分野へと広げています。深層学習と融合した3DGSは、次世代の3Dコンテンツ制作プラットフォームとして期待されています。

一方、VR技術も急速に発展しており、仮想環境でユーザー中心の三次元インタラクション体験を提供しています。いくつかの研究は、既に3DGSとVRの統合を試みています。例えば、VRGS[<sup>3</sup>](#refer-anchor-3)は、XPBD[<sup>4</sup>](#refer-anchor-4)と3DGSを導入することで、VR内に編集可能で動的な相互作用が可能なレンダリングパイプラインを構築し、ユーザーが仮想空間で3DGSオブジェクトを直接操作および変更することを可能にしました。また、VRSplat[<sup>5</sup>](#refer-anchor-5)などの研究は、VRシーンにおけるリアルタイムレンダリング品質の向上に焦点を当て、VR環境向けに最適化された高品質な3DGSレンダリングソリューションを提案しています。

既存の研究は既に初期的な成果を収めていますが、複雑なシーンでは、現在の⼿法は依然として、 特にカメラ移動時に、ガウシアンの過度な重複や不要な浮遊点群（フローター）が引き起こすフリッカー現象 、そして⾼計算コストといった問題に直⾯しており、これがVR環境における3DGSの⼤規模な応⽤を制限しています。

# 研究方法

本研究では、3DGSと既存のVR技術をいかに融合させるかを探求し、特にリアルタイム性、編集可能性、没入感の三つの方向性でのブレイクスルーを目指します。具体的な実施案は以下の通りです。

1. 編集可能な3DGS-VRパイプラインの構築

   VRGSの考え方を参考に、VR環境でインタラクティブなリアルタイム3DGSレンダリングパイプラインを構築します。まず、近年の研究で注目されているDust3R[<sup>6</sup>](#refer-anchor-6)のような、密な3D点群とセマンティック特徴を同時に出力可能な Pretrained Model を利用します。このモデルを用いて初期点群を生成し、出力された特徴量に基づいて点群の Semantic Segmentation を行います。次に、各点群に学習可能な Embedding を導入し、テクスチャ、マテリアルなどの属性を表現します。さらに、Encoder-Decoderか点群Transformer[<sup>7</sup>](#refer-anchor-7)に基づくネットワークを通じて点群の学習と最適化を行い、編集可能性と動的な相互作用を実現します。
2. 間接照明のモデリング

   3DGSをVR環境に統合するには、間接照明が没入感に与える影響を考慮する必要があります。このため、本研究ではニューラルネットワークに基づく間接照明のモデリング手法を探索し、具体的には、小型のニューラルネットワークを通じて点群に対して間接光の特徴を学習させ[<sup>8</sup>](#refer-anchor-8)、その結果を高速にクエリ可能なネットワークによる近似値としてキャッシュします。レンダリング段階では、このネットワークから直接高品質な間接光の推定値を得ることができ、これによりVRシーン全体の照明品質とリアリズムを向上させます。
3. 高効率な微分可能レンダリングパイプライン

   装着者がVRで快適な体験を得るためには、高いフレームレートを維持する必要があります。本研究では、まずシーン表現自体をコンパクトにするため、学習可能な Maskで不要なガウシアンを除去したり、Vector Quantization によって3DGSの幾何データを圧縮したりする手法[<sup>9</sup>](#refer-anchor-9)を探求します。その上で、グラフィックスにおける階層的詳細度 (Level of Detail, LOD)とカリング・アルゴリズムを組み合わせる[<sup>10</sup>](#refer-anchor-10)戦略を併用し、リアルタイムレンダリングに参加するガウスの数を減らすことで、画質を保証しつつ計算コストを大幅に削減することを目指します。

# 研究計画

修士M1第一学期：研究方法に記載された内容に基づき、まず分野内の最新の進捗状況を調査し、その後、実験用のコードフレームワークを構築して実験を開始する。

修士M1第二学期：実験結果に基づき、より良い結果を得るために異なる手法を試行し、実験を行う。並行して論文の執筆を開始する。

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

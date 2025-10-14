# 研究テーマ

本研究のテーマは「3DGSに基づいたリライティング」です。本研究では、3次元ガウススプラッティング（3D Gaussian Splatting, 3DGS）を3次元リライティングに応用し、その高性能という利点を活かすことで、アルゴリズムの効率性とスケーラビリティを向上させることを目指します。

# 研究背景

近年、3DGS[<sup>1</sup>](#refer-anchor-1)のような新興技術の発展に伴い、微分可能レンダリグの品質と効率が著しく向上しています。3DGSは、従来のボリュームレンダリングを基盤とし、その微分可能性と勾配降下法を利用してシーンを表現する3Dガウシアン群を最適化することで、 高品質な新視点画像合成を実現します 。同時に、人工知能の急速な進歩も、3DGSとニューラルネットワークの結合を加速させています，その応用を3Dコンテンツ生成、シーンの編集、動的なデジタルヒューマンといった複数[<sup>2</sup>](#refer-anchor-2)の最先端分野へと広げています。深層学習と融合した3DGSは、次世代の3Dコンテンツ制作プラットフォームとして期待されています。

一方、Relighting[<sup>3</sup>](#refer-anchor-3)の分野において、従来の3DGSでは照明情報と物体の色や質感（アピアランス）が強く結びついてしまうという課題がありました。この課題に対し、「Relightable 3D Gaussian」[<sup>4</sup>](#refer-anchor-4)は、BRDF分解とRay Tracingを導入して照明情報をガウシアンの属性から分離し、PBRのレンダリング方程式[<sup>5</sup>](#refer-anchor-5)でレンダリング過程をモデル化することで、シーンの照明と材質を個別に学習することを可能にしました。このアプローチは、物理ベースの忠実性とリアルタイム性能を両立させています。また、「RNG（Relightable Neural Gaussians）」[<sup>6</sup>](#refer-anchor-6)のような手法は、3DGSを髪の毛やビロードといった、より複雑な外観を持つオブジェクトへと拡張し、その再現能力を高めています。

これらの手法は顕著な進歩を遂げた一方で、大規模シーンや、強い鏡面反射・サブサーフェススキャタリングといった複雑な条件下では、依然として品質の低下、フリッカー、計算コストの増大といった問題が発生します。これらが、本技術の幅広い実用化を妨げる要因となっています。

# 研究方法

本研究では、3D Gaussian Splatting（3DGS）における物理ベースのリアルタイム・リライティング技術の確立を目指します。この目標を達成するため、材質特性の表現手法、グローバルイルミネーションのモデル化、及び複雑なシーンにおけるレンダリングの安定化に関する先進的なアプローチを探求し、リアリティと堅牢性におけるブレイクスルーを追求します。具体的な実施案は以下の通りです。

1. **物理に基づいたモデリングと属性の分離**

   従来のレンダリングにおけるPBR（物理ベースレンダリング）の手法を3DGSに導入し、レンダリング過程を物理法則に一致する形でモデル化します。これにより、独立した物理属性（アルベド、ラフネス等）を明示的に学習させ、照明とカラー（材質）の分離を実現します。このアプローチによって、照明情報が点群の球面調和関数（Spherical Harmonics）に直接的に学習されてしまう問題を回避します。
2. **グローバルイルミネーションと間接光のモデル化**

   グローバルイルミネーション[<sup>7</sup>](#refer-anchor-7)については、「Relightable 3DGS」を参考に環境光情報を環境マップにエンコードします。間接光については、小型のニューラルネットワークを用いて点群の間接光特徴を学習させることを試みます。さらに、「Neural Radiance Cache」[<sup>8</sup>](#refer-anchor-8)の着想を応用し、間接光を高速にクエリ可能なネットワークによる近似結果としてキャッシュします。これにより、レンダリング時には本ネットワークから直接、高品質な間接光の推定値を取得できます。また、訓練と推論の高速化のため、Instant-NGP[<sup>9</sup>](#refer-anchor-9)で用いられているNVIDIAの高性能MLPフレームワークの活用を計画しています。
3. **複雑なシーンに対応するハイブリッドレンダリング戦略**

   強い鏡面反射、サブサーフェススキャタリング（SSS）[<sup>10</sup>](#refer-anchor-10)が発生するシーンや、大規模シーンといった複雑・特殊な状況に対応するため、path tracingやphoto mappingといった従来のグローバルイルミネーション手法と3DGSを組み合わせたhybrid rendering pipelineの構築を検討します。これにより、リアルタイム性を維持しつつ、リライティングの品質と安定性を一層向上させることを目指します。

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
[3] Zhu, S., Wong, W. K., & Zou, X. (2025). Learning-based Human Relighting: A Survey. ACM Computing Surveys.

<div id="refer-anchor-4"></div>
[4] Gao, J., Gu, C., Lin, Y., Li, Z., Zhu, H., Cao, X., ... & Yao, Y. (2024, September). Relightable 3d gaussians: Realistic point cloud relighting with brdf decomposition and ray tracing. In European Conference on Computer Vision (pp. 73-89). Cham: Springer Nature Switzerland.

<div id="refer-anchor-5"></div>
[5] Kajiya, J. T. (1986, August). The rendering equation. In Proceedings of the 13th annual conference on Computer graphics and interactive techniques (pp. 143-150).

<div id="refer-anchor-6"></div>
[6] Fan, J., Luan, F., Yang, J., Hasan, M., & Wang, B. (2025). Rng: Relightable neural gaussians. In Proceedings of the Computer Vision and Pattern Recognition Conference (pp. 26525-26534).

<div id="refer-anchor-7"></div>
[7] Dutre, P., Bekaert, P., & Bala, K. (2018). Advanced global illumination. AK Peters/CRC Press.

<div id="refer-anchor-8"></div>
[8] Müller, T., Rousselle, F., Novák, J., & Keller, A. (2021). Real-time neural radiance caching for path tracing. arXiv preprint arXiv:2106.12372.

<div id="refer-anchor-9"></div>
[9] Müller, T., Evans, A., Schied, C., & Keller, A. (2022). Instant neural graphics primitives with a multiresolution hash encoding. ACM transactions on graphics (TOG), 41(4), 1-15.

<div id="refer-anchor-10"></div>
[10] Papantonakis, P., Kopanas, G., Kerbl, B., Lanvin, A., & Drettakis, G. (2024). Reducing the memory footprint of 3d gaussian splatting. Proceedings of the ACM on Computer Graphics and Interactive Techniques, 7(1), 1-17.

# 研究テーマ

本研究は、3D Gaussian Splatting（3DGS）でレンダリングされたシーンに対し、従来の3Dコンテンツ制作ワークフローとの親和性を重視しつつ、ユーザーがオブジェクトを精細かつ効率的に操作・変更できる、高度で直感的な編集フレームワークの構築を目指すものです。

# 研究背景

近年、3D Gaussian Splatting（3DGS）[`<sup>`1`</sup>`](#refer-anchor-1)のような新興技術の発展に伴い、微分可能レンダリングの品質と効率は著しく向上しています。3DGSは高品質な新視点画像をリアルタイムで生成可能であり、次世代の3Dコンテンツ制作基盤として大きな期待が寄せられています。しかし、基本的な3DGSで生成されるシーンは静的であり、一度学習が完了するとその後の編集が極めて困難になるという点が、より広範なクリエイティブ領域での応用展開における主な障壁となっています[`<sup>`2`</sup>`](#refer-anchor-2)。

この課題を解決するため、学術界では多方面からの探求が進められています。初期の研究は主にLangSplat[`<sup>`3`</sup>`](#refer-anchor-3)やGaussianEditor[`<sup>`4`</sup>`](#refer-anchor-4)のようなテキスト指示に依存しており、これらはシーンのセマンティックな操作を実現したものの、従来の3Dアーティストが持つ直感的なワークフローとは大きく乖離していました。その後の研究はより基礎的なレベルへと深まり、一方ではSemantic Gaussian Splatting[`<sup>`5`</sup>`](#refer-anchor-5)のようなセマンティック分割技術がオブジェクト単位での直接操作を可能にし、もう一方ではRelightable 3D Gaussians[`<sup>`6`</sup>`](#refer-anchor-6)のような照明と材質の分離（デカップリング）技術が、物理ベースの材質編集への道を開きました。

既存の研究は、言語編集、オブジェクト分割、材質分離といった個別の方向性で顕著な成果を収めているものの、これらの機能は現時点で断片的かつ未統合な状態にあります。依然として、これらの先進的な機能を一つに統合し、従来の3Dソフトウェアのような直感的で包括的な操作体験を提供する編集フレームワークは市場に存在しません。本研究は、この決定的な空白を埋め、3DGSにおけるシーン編集可能性の発展を推進することを目指すものです。

# 研究方法

本研究は、3D Gaussian Splatting（3DGS）で構築されたシーンの編集可能性を高めることを目指します。その実現のため、オブジェクトの幾何情報や材質といった物理プロパティの分離・編集を可能にし、かつ既存の3Dソフトウェアに近い直感的な操作体系を導入する、新たな編集フレームワークの構築を探求します。

1. 効率的な点群分割と基本的な編集

   3DGSによるシーンの初期再構成後、点群に対してセマンティック分割を行い[`<sup>`7 `</sup>`](#refer-anchor-7)、シーンを複数の構成要素に分離した上で、各要素を独立して編集します。同時に、シーンのリアルタイム編集を可能にするため、シーン表現自体の軽量化が求められます。その実現のため、学習可能なマスク（Mask）による不要なガウシアンの除去や、Vector Quantization技術を用いた3DGSの幾何データ圧縮[`<sup>`8 `</sup>`](#refer-anchor-8)といった手法を探求します。
2. オブジェクトの材質編集

   従来のレンダリングにおけるPBR（物理ベースレンダリング）[`<sup>`9 `</sup>`](#refer-anchor-9)手法を3DGSと組み合わせ、レンダリングプロセスに対して物理ベースのモデリングを適用します。これにより、反射率や粗さといったオブジェクト固有の物理プロパティを学習させ、照明と材質の分離（デカップリング）を実現します。照明情報が点群のSH係数に直接エンコードされることを回避し、材質の編集可能性を確立します。
3. 精細的な編集手法の探求

   3DGSベースのシーン編集を既存のワークフローとより容易に連携させるため、テキスト指示ベースの手法とは一線を回避する、より直感的で制御しやすい編集アプローチを探求します[`<sup>`10 `</sup>`](#refer-anchor-10)。具体的には、従来の3Dソフトウェアの操作体系を導入・組み合わせることで、ユーザーが追加の学習コストなしに、3DGSシーンに対して極めて精細な編集を行える環境の実現を目指します。

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
[3] Qin, M., Li, W., Zhou, J., Wang, H., & Pfister, H. (2024). Langsplat: 3d language gaussian splatting. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 20051-20060).

<div id="refer-anchor-4"></div>
[4] Wang, J., Fang, J., Zhang, X., Xie, L., & Tian, Q. (2024). Gaussianeditor: Editing 3d gaussians delicately with text instructions. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 20902-20911).

<div id="refer-anchor-5"></div>
[5] Li, M., Liu, S., Zhou, H., Zhu, G., Cheng, N., Deng, T., & Wang, H. (2024, September). Sgs-slam: Semantic gaussian splatting for neural dense slam. In European Conference on Computer Vision (pp. 163-179). Cham: Springer Nature Switzerland.

<div id="refer-anchor-6"></div>
[6] Gao, J., Gu, C., Lin, Y., Li, Z., Zhu, H., Cao, X., ... & Yao, Y. (2024, September). Relightable 3d gaussians: Realistic point cloud relighting with brdf decomposition and ray tracing. In European Conference on Computer Vision (pp. 73-89). Cham: Springer Nature Switzerland.

<div id="refer-anchor-7"></div>
[7] Wu, X., Jiang, L., Wang, P. S., Liu, Z., Liu, X., Qiao, Y., ... & Zhao, H. (2024). Point transformer v3: Simpler faster stronger. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 4840-4851).

<div id="refer-anchor-8"></div>
[8] Lee, J. C., Rho, D., Sun, X., Ko, J. H., & Park, E. (2024). Compact 3d gaussian splatting for static and dynamic radiance fields. arXiv preprint arXiv:2408.03822.

<div id="refer-anchor-9"></div>
[9] Kajiya, J. T. (1986, August). The rendering equation. In Proceedings of the 13th annual conference on Computer graphics and interactive techniques (pp. 143-150).

<div id="refer-anchor-10"></div>
[10] Qu, Y., Chen, D., Li, X., Li, X., Zhang, S., Cao, L., & Ji, R. (2025, August). Drag your gaussian: Effective drag-based editing with score distillation for 3d gaussian splatting. In Proceedings of the Special Interest Group on Computer Graphics and Interactive Techniques Conference Conference Papers (pp. 1-12).

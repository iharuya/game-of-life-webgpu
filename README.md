# Tutorial

https://codelabs.developers.google.com/your-first-webgpu-app?hl=ja

- 描画Primitiveは点、線分、三角形のみ
- 2D/3Dよらず、GPUが描画するほぼすべてのものは単なるクリップ空間内の三角形
- Spec: https://gpuweb.github.io/gpuweb/
- シェーダーとはGPUメモリデータを使って頂点の処理、行列の計算などを行うプログラムのこと。これはJSより厳格に構造化しなくてはいけないので、WebGPUではWGSLという言語が使われる。
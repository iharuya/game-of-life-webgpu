# Game of Life with WebGPU

WebGPU を使ってライフゲームを描画する

[WebGPU を使えるブラウザ・バージョン一覧](https://developer.mozilla.org/en-US/docs/Web/API/WebGPU_API#browser_compatibility)

Enter キーで全画面トグル

## The Tutorial

https://codelabs.developers.google.com/your-first-webgpu-app?hl=ja

- 描画 Primitive は点、線分、三角形のみ
- 2D/3D よらず、GPU が描画するほぼすべてのものは単なるクリップ空間内の三角形
- Spec: https://gpuweb.github.io/gpuweb/
- シェーダーとは GPU メモリデータを使って頂点の処理、行列の計算などを行うプログラムのこと。これは JS より厳格に構造化しなくてはいけないので、WebGPU では WGSL という言語が使われる。
- ユニフォームバッファとストレージバッファの違い
  - ユニフォームバッファ
    - シェーダー内で読み取り専用。シェーダー内で値を変更することはできない。
    - ストレージバッファよりも高速にアクセスできる。
    - 頻繁に更新が発生する可能性のある小さなサイズのデータがあれば、ユニフォームバッファの使用を検討する
  - ストレージバッファ
    - シェーダー内で読み取り/書き込み可能。シェーダー内で値を変更することができる。
- コンピューティングシェーダー
  - 頂点シェーダーやフラグメントシェーダーと違って、I/O の型は自由自在、呼び出しも自由自在
  - とはいえ、1 兆回の呼び出しを並列処理するわけにはいかないので、ワークグループという単位に分割する
  - WebGPU ではクライアントの物理 GPU の性能が詳しくわからない？ので最適なワークグループサイズはわからないけど、64 ぐらいが安牌
- スウィズリング
  - `cellIndex(cell.xy)`が`cellIndex(vec2(cell.x, cell.y))`と同じ意味
  - `cell.zyx`, `cell.yyyy`とか繰り返すこともできる
  - WGSL でできるってことは Rust でもそうなのかも

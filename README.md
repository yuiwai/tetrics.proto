tetrics.proto
====

tetrics ( https://github.com/yuiwai/tetrics ) とやり取りをするためのprotobuf定義です。

## リクエスト

tetrics側から、現在のゲームの状態が送信されます。  
バージョン文字列については現在は"0.1"で固定です。

## レスポンス

tetrics側に返すアクションのリストです。  
例えば、「右回転」「左移動」「上へドロップ」のように、一連のアクションをまとめて返すことができます。


## フィールド

tetricsでは一般的な10x10のフィールドが全部で5つ存在ます。  
中央は、プレイヤーがブロックを回転させたり移動させたりするためのフィールドで、その周囲4方向にブロックを積み上げるためのフィールドがあります。  

フィールドは上から下に向かって10行分のデータを持っています。  
行は左から右に向かって、10列分のデータを持っています。  
テトリス同様、一行を埋めることでその行を消すことができます。

## ブロック

テトリスで言うところのテトリミノです。これをフィールドに積み上げることでゲームは進行します。  
データ構造的にはフィールドと同様に行と列の2次元配列構造として扱われます。

## プレイサイクル

ゲームが開始されると、中央のフィールドにランダムに選択されたブロックが配置されます。  
このブロックを左右に回転させるか、上下左右に移動させ、4方向のうちのいずれかのフィールドにドロップするまでが1サイクルとなります。  
ドロップ後は再びブロックが抽選され、中央のフィールドに配置されます。

## 座標

左上を原点として、右にxが増加、下にyが増加していく座標系となっています。

## 回転について

回転時のブロックの座標にはルールがあります。  
初期配置時の状態から、右もしくは左に回転することで、内部ステータスが遷移し、一回転（4回の状態遷移）すると元のステータスに戻ります。  
初期ステータスから右に一回転するときは、座標の端数が「切り上げ」「切り上げ」「切り捨て」「切り捨て」の順に処理されます。

# flutterについて


プロジェクトのファイル構成について
___
~~~
- Flutterプロジェクトには多くのフォルダが含まれており、それぞれのプラットフォーム（Android、iOS、Windows、Web など）に関連するファイルが格納される。
- .dart_tool は Dart 言語が自動生成するファイル類を保管するフォルダ。
- lib フォルダには Dart のスクリプトが保存され、test フォルダはユニットテスト関連のファイルを管理する。
- .gitignore や pubspec.yaml などのファイルは、パッケージ管理やコード解析などに使用される重要な設定ファイル。
~~~



## アプリ画面とウィジェットツリー
　  flutterでは画面表示は「ウィジェット」とよばれる部品によって作成されている。

---
---
そもそも「ウィジェット」とは

ボタンの様に目に見えて操作できるものや、他のウィジェットをまとめたり、決まったレイアウトを配置する、見えないものもある。

---
---
flutterの画面は、すべてがこうしたウィジェットの組み合わせによって構成されている。
## アプリ実行の仕組み
　まず、””package:flutter/material.dart””というパッケージを読み込んでいます。
これが、fluuter　のマテリアルデザインによるアプリのUIウィジェットがまとめられているパッケージです。最初にこれをimportする。

　　　アプリのプログラムを実行する処理は、ごく単純にまとめるなら、以下のようになる
~~~
 void main (){
  runApp(ウィジェット);
 }
~~~
**main**➡アプリを起動する際に呼び出される処理

**runApp**という関数を実行している。これがアプリを起動する処理である。

# StatelessWidgetクラス
「**StatelessWidget**」とはステート（状態を表す値）を持たないウィジェットのベースとなるクラスである。ウィジェットのクラスは、このStatelessWidgetと、ステートを持つStatefulWidgetのいずれかを継承して作成される。

「***一度作ったら変わらない画面***」

## Material Appクラス

~~~
return MaterialApp(  
     title: 'Flutter Demo',
     home: Text(
        'Hello,Flutter World!!',
        style: TextStyle(fontSize:32.0),
     ),
  ); 
~~~

**①return MaterialApp(** 

　　↓

flutterアプリを作るための土台を返す、画面を管理する役割を持っている。またアプリ全体の設定をする場所である。

**②title: 'Flutter Demo',**

　　↓　　

アプリのタイトルの設定

**③home: Text(**

↓

最初に表示する画面（home）を決める。

**④   'Hello,Flutter World!!'**

↓

表示するテキストの内容を設定するもの。

**⑤　 style: TextStyle(fontSize:32.0),**

↓

テキストの見た目（スタイル）を設定するもの。


----
・アプリの構造を確認
---
1 アプリケーションは、main関数として定義する。このmain関数では、runAppでウィジェットのインスタンスを実行する。

2 runApp関数ではStatelesswidget継承クラスのインスタンスを引数に指定する。　　これがアプリ本体のUIとなる。

3　Statelesswidgetr継承クラスにはbuildメゾットを用意する。マテリアルデザインのアプリクラスであるMaterialAppインスタンスをreturnする。

4　MaterialAppの引数homeに実際にアプリ内に表示するウィジェットを設定。

flutterアプリは　main関数　statelesswidget materialapp　などが階層的に組み込まれた形になっている。

## Scaffoldについて
一言でいえば「足場、骨組み」みたいなもの。

~~~
{役割}
- appBar → 画面の上に「タイトルバー」をつける
- body → 画面のメイン部分（テキストやボタンなど）を配置する
- floatingActionButton → 画面の端に「丸いボタン」を追加できる　などなど。
~~~


例えば
>Scaffold(  
>  appBar: AppBar(  
>   title: Text('Hello Flutter!'),  
> ),  
>  body: Text(  
>    'Hello Flutter World!!!',  
>    style: TextStyle(fontSize: 32.0),  
>  ),  
>)

上のコードの場合だと
>appBar: AppBar(  
>   title: Text('Hello Flutter!'),  
> ),  

この部分ではアプリケーションバーのウイジェット（appbar）に表示をするテキストをtextインスタンスとして指定することで、アプリケーションバーにText内のものが表示されるようになっている。

>  body: Text(  
>    'Hello Flutter World!!!',  
>    style: TextStyle(fontSize: 32.0),  
>  ),  

この部分では、アプリケーションバーの下の空白エリア全体の表示を担当する「body」にtextインスタンスを組み込むことで、その部分に表示させるようになっている。

イメージ
![イメージ](https://cdn.discordapp.com/attachments/1374623617165557851/1380763267521183815/69_20250607132000.png?ex=68450f80&is=6843be00&hm=26b53e1b1ec79d144f7c4942c2309cf2324fb278e610a1e839fb36f6636d8714&)

赤で線を引いてある部分がアプリケーションバー
その下の空白が「body」によっていじれる部分。

# | Stateクラスの利用
## StatefulWidgetについて
動的に表示するものを作るのに使うのが
***「StatefulWidget」***
 
 ### |StatefulWidgetとState
 ・StatefulWidget　➡　「設計図」　画面の基本的な構造を決めるもの
 ・State         ➡「メモ帳」　変化するデータを記録する。






　　












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

### |StatefulWidgetクラスの基本形
 ~~~
 class ウィジェットクラス extends StatefulWidget{

   @override
   ステートクラス　createState() => ステートクラス();

 }
~~~

### | Stateクラスの基本形

~~~
class ステートクラス　extends State<ウィジェットクラス>{

 ......略......

 @override
 Widget build(BuildContext context){

     ...略...

 }

}

~~~

- StatefulWidgetは、ウィジェット部分（StatefulWidgetクラス）とステート部分（Stateクラス）の２つで構成される。ウィジェットクラスはStatefulWidgetクラスを継承して定義する。

- createState メソッドは、ウィジェットの状態（ステート）を作るために使われる。
- build メソッドは、画面を再描画するために頻繁に呼び出される。
つまり、createState でステートを作り、build でそのステートを使ってUIを更新するという流れになります。

## |ステートを操作する
~~~
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  final title = 'Flutterサンプル';
  final message = 'サンプル・メッセージ。';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MyHomePage(
        title: this.title,
        message: this.message
      ),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;
  final String message;
  const MyHomePage({
    Key? key,
    required this.title,
    required this.message
  }): super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        widget.message,
        style: TextStyle(fontSize:32.0),
      ),
    );
  }
}

~~~

### |StatelessWidgetからStatefulWidget　コードの説明
~~~
final title = 'Flutterサンプル';  
 final message = 'サンプル・メッセージ。';  
~~~
「final」が指定されていることで、値が変更されない。
~~~

 return MaterialApp(  
      title: 'Flutter Demo',  
     home: MyHomePage(  
        title: this.title,  
        message: this.message  
      ),  
    );

~~~
homeのMyHomePageにtitleとmessageという二つの値を用意し、this.titleとthis.messageを指定している。前のフィールドを引数に指定してMyHomePageインスタンスを作っている。

このMyHomePageのクラス側は、以下のようにコンストラクタが用意されている。
~~~
const MyHomePage({
    Key? key,
    required this.title,
    required this.message
  }): super(key: key);
~~~
このクラスでも、title,messageというfinalフィールドが用意されている。引数で渡された値が、そのままthis.titleとthis.messageに代入されていることがわかります。

これでMyAppで用意した値がそのままMyHomePageに渡された。

### |MyHomePageから_MyHomePafeStateについて
   次にMyHomePageに保管したtitleとmessageを使い、ステートクラスである_MyHomePageStateクラスのインスタンスを作成する部分を見てみましょう 

~~~
Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        widget.message,
        style: TextStyle(fontSize:32.0),
      ),
    );
~~~

Text引数に、それぞれWidget.titleとwidget.messageを指定している。このwidgetはStateクラスに用意されるプロパティで、このステートが設定されているウィジェットのインスタンスが代入されています。



## FloatingActionButtonをクリック

~~~
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  final title = 'Flutterサンプル';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MyHomePage(
        title:this.title,
      ),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({required this.title}): super();
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  String _message = 'Hello!';

  void _setMessage() {
    setState(() {
      _message = 'タップしました！';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Text(
        _message,
        style: TextStyle(fontSize:32.0),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _setMessage,
        tooltip: 'set message.',
        child: Icon(Icons.star),
      ),
    );
  }
}
~~~

## |ステート更新とsetState
State継承クラス内にステートの変更のための処理を用意している。

~~~
class _MyHomePageState extends State<MyHomePage> {
  String _message = 'Hello!';

  void _setMessage() {
    setState(() {
      _message = 'タップしました！';
    });
  }
~~~

このメソッドでは、「***setState***」というメソッドを実行しています。
setStateは、ステートの更新をステートクラスに知らせる働きをします。

"String _message = 'Hello!';"　　

_messageという変数を作って、最初の値を"***Hello***"にしています。
この_messageの値を変えることで、画面に表示される言葉を変更できます。

~~~
"void _setMessage() {
    setState(() {
      _message = 'タップしました！';
    });
  }"
~~~

この「_setMessage()」という関数は、ボタンが押されたときに呼ばれる。

その中の「setState()」を使うことで、画面の内容を更新できる。

|具体的に|
|-|

|_messageの内容を"タップしました！"に変更|
|-|

|setState()を使うことで、アプリが「新しいメッセージに変わった」と認識し画面を更新。|
|-|



## |FloatingActionButtonクラスについて
~~~
 floatingActionButton: FloatingActionButton(
        onPressed: _setMessage,
        tooltip: 'set message.',
        child: Icon(Icons.star),
      ),
~~~
_setMessage()はどこで呼び出されているかが次の問題につながります。実はコードの最後の方にある
floatingActionButton「フローティングアクションボタン」と呼ばれる所に呼び出されています。

## 「floatingActionButton」とは？

画面の端に浮かぶように表示される円形のボタン。を表示する関数です。このボタンはアプリの画面に表示されているウィジェットなどと同じような形で組み込まれているわけではないです。他のウィジェットの配置とは関係なく、いつも同じ所に表示されます。

---

それぞれの部分解説

|onPressed:_setMessage|
|-|

　➡　ボタンが押された時の動作の設定。   
                              
  ・ ここでは_setMessagという関数が呼ば れ、***メッセージが変わる***仕組みになっています。        

  |tooltip: 'set message.',|
  |-|

  ➡    ユーザーがボタンを長押ししたときに表示される***テキスト*** 


   |child: Icon(Icons.star),|
   |-|

　➡  FABのアイコンを設定している。
ここでは星（★）マークを使っていますが、他にも  
***Icons.add  (プラスボタン)などが使えます。***

## 複雑な値の利用
~~~
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  final title = 'Flutterサンプル';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: MyHomePage(title: this.title),
    );
  }
}

class MyHomePage extends StatefulWidget {
  final String title;

  const MyHomePage({Key? key, required this.title}) : super(key: key);

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

// データ用クラス
class Data {
  int _price;
  String _name;
  Data(this._name, this._price) : super();

  @override
  String toString() {
    return _name + ':' + _price.toString() + '円';
  }
}

class _MyHomePageState extends State<MyHomePage> {
  // サンプルデータ
  static final _data = [
    Data('Apple', 200),
    Data('Orange', 150),
    Data('Peach', 300),
  ];
  Data _item = _data[0];

  void _setData() {
    setState(() {
      _item = (_data..shuffle()).first;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Set data')),
      body: Text(_item.toString(), style: TextStyle(fontSize: 32.0)),
      floatingActionButton: FloatingActionButton(
        onPressed: _setData,
        tooltip: 'set message.',
        child: Icon(Icons.star),
      ),
    );
  }
}
~~~
まず初めに教科書のコードと実際に表示ができたコードとで違った部分を紹介をします。

***[教科書のclass MyHomePage部分]***
>class MyHomePage extends StatefulWidget {  
>  const MyHomePage({title:'Flutter Demo'}): super();   
>
>  @override  
>  _MyHomePageState createState() => _MyHomePageState();
>}


***[実際に表示が上手くいったclass MyHomePage部分]***
>class MyHomePage extends StatefulWidget {
>  final String title;
>
>  const MyHomePage({Key? key, required this.title}) : super>(key:key);
>
>  @override  
>  _MyHomePageState createState() => _MyHomePageState();
>}

### |エラーになったと考えられる原因をいくつか紹介|

>const MyHomePage({title:'Flutter Demo'}): super();  

1.
|title:'Flutter Demo'| 
|-|
の問題点

・これはtitleに文字列'Flutter Demo'を設定しようとしているけれど、***正しくプロパティを定義していない***ため、エラーが出る。

・titleを***クラスの中でちゃんと宣言***しないと、Flutterはそれを認識することができない。

２.コンストラクタの正しい書き方

・`title`を使いたいなら、クラスの中で　　　　　`final String title;`と***プロパティを明示する必要***がある。

・さらに、値を渡すときは`required`をつけて、***必ず指定する***ようにする。
　　　　　　　　　
<div style="text-align: center;">
<div style="font-size: 150%"> これらに注意して修正することで </div>
</div>

<div style="text-align: center;">
<div style="font-size: 150%"> 
↓
</div> </div>

このコードになる。
>class MyHomePage extends StatefulWidget {
>  final String title;  
>
>  const MyHomePage({Key? key, required this.title}) : super>(key:key);
>
>  @override  
>  _MyHomePageState createState() => _MyHomePageState();
>}

### | Dataについて

１.Dataクラスについて

アプリを作る際に「名前」「年齢」などの関連のある情報をひとまとめにしたい場合がでてきます。そのような複数の情報を１つの箱にまとめ、管理するのがDataクラスです。

>class Data {  
>  int _price;  
>  String _name;  
>  Data(this._name, this._price) : super();
>
>  @override  
>  String toString() {  
>    return _name + ':' + _price.toString() + '円';   
>   }  
>}

このDataクラスでは、_price _nameという二つのプロパティ（そのクラスが持っている情報・データ）を用意してあります。

コンストラクタでは、引数の値をそれぞれのプロパティに設定するようにしてある。（注文された情報を、ちゃんとその人専用のデータに詰めておく作業）

toStringをオーバーライドし、内容をテキストにまとめて出力するようにしてある。

### | Dataインスタンスの設定

ステートクラス側では、Dataインスタンスをまとめたリストを用意しておき、これをランダムに選んで表示する処理を用意している。

まず初めに、データとなるリストと、選んだDataを保管するプロパティを用意しておきます。

>static final _data = [  
>    Data('Apple', 200),  
>    Data('Orange', 150),  
>    Data('Peach', 300),  
>  ];  
>  Data _item = _data[0];

Dataインスタンスを保管する_dataは、static finalにしてある。後でリスト
を改変することがないため。
その後、_dataの最初の項目を _itemに設定している。

>_item = _data[0];
これで、起動時に最初のDataが表示されるようになります。後は、ステートを設定する_setDataで、リストからランダムにDataを取り出す処理を用意するだけになる。

>void _setData() {  
>    setState(() {  
>      _item = (_data..shuffle()).first;  
>    });  
>  }

ここではsetState内で（data..shuffle()).firstという形で値を取り出しています。　　shuffleは、リストの項目をランダムに入れ替えるメソッドで、firstは最初の項目のプロパティ。これにより、_dataからランダムに１つを取り出せます。

## デフォルトのmain.dart

これまでのおさらいもかねて、もともと生成されていたコードがどういったものだったか確認します。

~~~
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key, required this.title}) : super(key: key);
  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ),
    );
  }
}

~~~

### 　|main.dartの内容

#### ◆１.MyAppクラス
ここでは、buildメソッドでMaterialAppを作成し返す処理が用意されている。themeという値は、テーマを指定するためのもの。

#### ◆２.MyHomePageクラス
コンストラクタとcreateStateがあるだけのシンプルなクラス。
>const MyHomePage({Key? key, required this.title}) : super(key: key);

引数の値をthis.titleに設定して、そのほかに、keyという値も渡されている。ウィジェットを識別するためのIDのようなもの。デフォルトでこのkeyを受け取るようになっている。MyAppクラスでこのMyHomePageインスタンスを作成している部分を見ると...

>const MyHomePage(title: 'Flutter Demo Home Page'),

keyの値は用意されない。keyは用意しなくとも自動的に割り当てられる。実際にはこのkeyは特に使われない。

#### ◆３._MyHomePageStateクラス
ステートの処理を行う_MyHomePageStateクラスでは、_counterというフィールドを用意している。setStateでは、この値を１ずつ増やす処理を用意している。また_counterの値をText表示するのに、変わったやり方をしています。

>Text(  
>   '$_counter',  
>....);

Textに表示するテキストに、'$_counter',という値が指定されている。この値は、























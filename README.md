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

Textに表示するテキストに、'$_counter',という値が指定されている。この値は、変数_counterをテキストリテラル内に埋め込んでいるもの。Dartでは、このように「$変数」という形で変数リテラル内に埋め込むことができる。

## 2-3ウィジェットの基本レイアウト
次に、flutterの重要な特徴の1つに「さまざまな画面サイズのデバイスに対応できる」という点があげられる。ここでは画面のレイアウト作成に、flutter studioを活用します。

[flutter studio](https://flutterstudio.app/)

ここに必要なウィジェットをドラッグ＆ドロップして配置し下にある「source vode」タブをクリックして表示を切り替えれば、そのレイアウトのソースコードをコピーすることができます。

### textを配置

ソースコード
>import 'package:flutter/material.dart';
>
>void main() {  
>  runApp(MyApp());  
>}  
>class MyApp extends StatelessWidget {  
>  
>  @override  
>  Widget build(BuildContext context) {  
>    return MaterialApp(  
>      title: 'Generated App',  
>      theme: ThemeData(  
>        primarySwatch: Colors.blue,    
>        primaryColor: const Color(0xff2196f3),  
>        canvasColor: const Color(0xffafafa),  
>      ),  
>      home: MyHomePage(),  
>    );  
>  }  
>}  
>
>class MyHomePage extends StatefulWidget {  
>  MyHomePage({Key? key}) : super(key: key);  
>  @override  
>  _MyHomePageState createState() => _MyHomePageState();  
>}  
>
>class _MyHomePageState extends State<MyHomePage> {  
>    @override  
>    Widget build(BuildContext context) {  
>      return Scaffold(  
>        appBar: AppBar(  
>          title: Text('App Name'),  
>          ),  
>        body:  
>          Text(  
>          "Hello Flutter!",  
>            style: TextStyle(fontSize:32.0,  
>            color: const Color(0xff000000),  
>            fontWeight: FontWeight.w700,  
>            fontFamily: "Roboto"),  
>            ),  
>      );  
>    }  
>}  

#### テキストスタイルについて
　レイアウトに入る前に、テキストの表示に関する機能についてです。
テキストのスタイルは、Textウィジェットを作成する際、styleという値を使って設定する。
この値は「TextStyle」というクラスとして用意されている。

| fontSize | fontWeight | fontFamily |
|-----|-----|-----|
|フォントサイズ。double値で指定|フォントの太さ。|テキスト（String）で指定|

| fontStyle |color |
|-----|-----|
|FontStyle列挙型のnormal,italicという値で指定|colorクラスで指定|

これらの中で必要な項目だけを値として用意すれば、それらを指定するTextStyleが作成されます。省略されたものはデフォルト値です。
参考に先ほどのソースコードを載せます。

---
>"Hello Flutter!",  
>             style: TextStyle(fontSize:32.0,  
>            color: const Color(0xff000000),  
>            fontWeight: FontWeight.w700,  
>            fontFamily: "Roboto"),  
>            ),  
---

### Colorについて
書き方がいくつかあります。
>color: const Color(0xff000000),

引数には、６または８桁の１６進数を指定します。これで、RGB,ARGBの値を指定しています。インスタンス作成事態は、Colorではなく、const Colorとして定数扱いになっている。基本としてColorでは、インスタンス作成する際はconstを使用する。
>Color.fromARGB(アルファ,赤,緑,青)

引数にはARGBの各値を0～255の整数で指定。

#### Colorsクラス
>colors. blue

colorsは、主な色の値をまとめたクラスです。個人的に一番使いやすいと感じました。

### Centerによる中央揃え
また一度例としてコードを載せます。

>class _MyHomePageState extends State<MyHomePage> {  
  @override  
  Widget build(BuildContext context) {  
    return Scaffold(  
      appBar: AppBar(  
        title: Text('App Name'),  
      ),  
      body:  
      Center(  
        child:  
        Text(  
          "Hello Flutter!",  
          style: TextStyle(fontSize:32.0,  
              color: const Color(0xff000000),   
              fontWeight: FontWeight.w700,  
              fontFamily: "Roboto"),  
        ),  
      ),  
    );  
  }  
>}  

Centerクラスの基本形は

>Center(  
>   child:....ウイジェット....  
>)

childという値が用意されている。ここに配置するウイジェットを用意します。

## Containerクラスについて
Centerは、中央にウイジェットを配置するだけですが、場合によっては右側に寄せたり、あるいは画面の下に配置したりしたいときもある。

このような細かな配置の設定を行えるのが「Container」というクラス。これは文字通り、コンテナのもっとも基本的なクラス。

| Color | Alignment | Sized | Padding |
| ---- | ----- | ---- | ---- |
| 色の指定。通常時は、MaterialAppで設定されたテーマに沿った色で背景などが設定されるが、Onにすると、コンテナ独自の背景色を設定できる。| 配置場所の指定。これは上下左右を9ヶ所に分け、そのどれかを選択。　| 表示サイズを最大化するためのもの　| 余白幅の設定。　上下左右の余白を整数で指定　|

### |Containerクラスの基本形

>Container(  
     child: ...ウィジェット...,  
     padding:<<EdgeInsets>>,  
     alignment<<Alignment>>,  
>)

Centerと同様、中に組み込むウィジェットのインスタンスをchildに指定。その他に、paddiing、alignmentが用意されている。これらで余白と位置を決める。

#### |Edgelnsetsについて
周辺の余白は、paddingという値を使う。これは「Edgelnsets」というクラスを使って設定している。

EdgeInsetsクラスは、上下左右の余白幅を設定するためのやつ。

◆　全方向を設定
>EngeInsets.all(<<double>>)

allは引数で指定した値に上下左右すべての余白幅を設定するものです。

◆　個別に設定
>EdgeInsets.fromLTRB(左,上,右,下)

fromLTRBは、左・上・右・下の順に余白幅を数値で指定します。全部で四つの引数を用意する必要がある。

> const EdgeIndets.only(left:左,top:上,right:右,botom:下,)

  onlyは、上下左右のうち、必要な項目だけを指定するもの。

  省略したものはすべてゼロが指定されます。

◆シンメトリック
>const EdgeInsets.symmetric(横,縦)

縦横で値を指名する。

### |Alignmentについて

配置場所を示すalignmentは、Alignmentクラスを使い指定する。

| topLeft | topCenter | topRight | centerLeft | center | centerRight | bottomLeft | bottomCenter | bottomRight |
| ------- | --------- | -------- | ----------- | ------ | ----------- | ---------- | ------------- | -------- |
|左上|中央上|右上|左中央|中央|右中央|左下|中央下|右下|

これら以外にも、全体の位置を-1.0~1.0の範囲で指定するやり方もある。

例えば...
>alignment: const Alignment(0.5,-0,5),

のような感じ。

## 2-4複数ウィジェットの配置

## Columnを使う
ここまで使ったコンテナ型のウィジェットは、すべて「１つのウィジェットだけ」を組み込めるようになっていた。しかし、実際のデザインでは、一つの画面内に複数のUI部品が配置されます。

これには、複数のウィジェットを組み込めるコンテナを利用する必要がある。こうしたコンテナは、レイアウトの方式に応じて何種類か用意されている。

最初に取り上げるのが***Colum***というウィジェットです。

簡単に説明すると、複数のウィジェットを「**縦**」に並べて配置するもの。

### |Columnの基本形

>Column(  
    mainAxisAlignment: [MainAxisAlignment],  
    mainAxisSize: [MainAxisSize],  
    crossAxisAlignment: [CrossAxisAlignment],  
    children: <Widget>[...リスト...]  
>)  

色んな値が用意されています。

childrenというのが、Columnに組み込まれるウィジェットを用意するところです。これはウィジェットのインスタンスをリストにまとめたものを指定します。Columnは、このchildrenのリストから順にウィジェットを表示していきます。リストの並び順が変われば、表示されるウィジェットの順番も変わります。


## Rowを使う

Rowは複数のウィジェットを「**横**」に並べるものです。

### Rowの基本形

~~~
Row(　　　　　　
  mainAxisAlignment: [MainAxisAlignment],
  mainAxisSize: [MainAxisSize],
  crossAxisAlignment: [CrossAxisAlignment],　　　　
  children: <Widget>[...リスト...]　　　　　　　　　　　
)
~~~

見ての通りColumnとほぼ一緒です。なのでセットで覚えるといいらしい。

### Main AXisとCross Axis

| Main Axis | Cross Axis |
| ---------- | ------- |
| ウィジェットが順に並ぶ方向。Columnは縦、Rowは横　| 並んだウイジェットと交差する方向。　Columnなら横方向、Rowなら縦方向。 |

このように、ColumnやRowでは、方向を「縦・横」ではなく、「ウィジェットが並ぶ方向、それに交差する方向」として考える。こうすることで、ColumnやRowのように、並ぶ向きが異なるものでも同じ考え方でレイアウトを作成できるようになっています。

# 3－1　ボタン・ウィジェット

## TextButtonについて

「TextButton」は特にUIの外観なども持たない、平面のボタンです。基本形は次のようになります。

>TextButton(key:null,  
>   onPressed: 関数,  
>   child: ウィジェット  
>)

onPressedとは、このTextButtonをクリックした際に実行される処理を指定するためのもの。ここは直接関数を記述することも可能です。

childは内部に組み込むウィジェットです。TextButtonは、デフォルトでは何も表示されません。なのでchild内で、Textを組み込むことでその言葉を表示することで、ボタンらしくなります。

### アイコンの表示

ではchildのウイジェット部分にText以外に何を入れればボタンらしくなるか、アイコンなどを試しに入れてみます。

>TextButton(  
>  onPressed:buttonPressed,  
>  child: Padding(  
>    padding: EdgeInsets.all(10.0),  
>    child:Icon (  
>      Icons.android,  
>      size: 50.0,  
>    )  
>  )  
>)  

このコードによって実行すると、ボタンの部分に言葉Textではなく、androidのアイコンが表示されるようになりました。ここでは、TextButton内にPaddingを組み込み、さらにその中にIconインスタンスを組み込んでいます。

### buttonPressed メソッドについて
クリックしたときの処理については次のような例があります。

>void buttonPressed(){  
>   setState((){  
>       _message = (_janken..shuffle()).first;  
>    });  
>}

これは教科書で、ボタンを押したら_messageに表示されているものが、_jankenの中のいくつかの単語に変わるというものを例で挙げています。まだ試せてはいませんが、buttonPressedを使うことで、他にも色んな事ができそうだと感じました。

## Padding
Paddingとは**余白**を作成する、表示させるためのコンテナです。
基本余白の機能がないウィジェットで余白設定したいときに使います。

## ElevatedButton・IconButton について
つぎにTextButtonと同じ働きをし、表示方法が少し違うものを軽く書いておきます。

***- Elebatedbutton***

「ボタンが**立体的**に表示されます。」

***- IconButton***

「その名の通りアイコンをクリックできるよう表示されます。」

## FloatingActionButtonについて
アイコン表示するボタンは、すでに「FloatingActionButton」を利用していた。これは基本的に画面の右下にあります。ですが普通のボタンとしてウィジェットを組み込んで使うこともできます。
~~~
FloatingActionButton(
  child: Icon(Icons.android),
  onPressed: buttonPressed
),
~~~
こうすることで普通のボタンとしても機能しますが、やはり右下にある方が一番利用しやすいことがわかりました。

## RawMaterialButtonについて
サンプルソースコード
~~~
RawMaterialButton(
  fillColor: Colors.white,
  elevation: 10.0,
  padding: EdgeInsets.all(10.0),
  child: Text(
      "Push me!",
      style: TextStyle(fontSize:32.0,
      color: const Color(0xff000000),
      fontWeight: FontWeight.w400,
      fontFamily: "Roboto"),
    ),
  onPressed: buttonPressed
),

~~~
実行すると横長の白いボタンが表示されます。これがRawMaterialButtonです。クリックすればちゃんとbuttonPressedメソッドの処理が実行される。

ここでは、fillColorとelevation:という値が用意されています。RawMaterialButtonには他にもひょうじに関する値が用意されています。

| fillcolor | highlightcolor | splashcolor | elevation | highlightElevation 
| --- | --- | --- | --- | --- |
背景色　| クリックしてハイライトした時の色　| クリックされたことをあらわす効果として使われる色　|　ボタンの高さ（影の幅） | クリックしたときのボタンの高さ　|

これらを個別に設定することで、独自のボタンを作成できます。

# 3-2 入力のためのUI

## Text Field について
「Text Field」は、テキストを入力するUIウィジェットです。例えを上げるとすると、ネット上での自由記入欄的なものを作れるものです。初めに例のコードををclass MyhomePageStateから

例
~~~
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static final _controller = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(10.0),
              child: TextField(
                controller: _controller,
                style: TextStyle(
                  fontSize: 28.0,
                  color: const Color(0xffFF0000),
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
            ElevatedButton(
                child: Text(
                  "Push me!",
                  style: TextStyle(
                    fontSize: 32.0,
                    color: const Color(0xff000000),
                    fontWeight: FontWeight.w400,
                    fontFamily: "Roboto"),
                ),
                onPressed: buttonPressed),
          ],
        ),
      ),
    );
  }

  void buttonPressed() {
    setState(() {
      _message = 'you said: ' + _controller.text;
    });
  }
}

~~~

このコードを実行をすると、テキストを入力できる部分とボタンが表示されます。

## TextField Controllerについて
では、TextFieldの作成部分を見てみます。ここではColumnの中にTextやElevatedButtonとともにTextFieldを追加している。
~~~
TextField(
    controller:<<TextEditingController>>,
    style:<<TextStyle>>
 )   
 ~~~

 styleはテキストスタイル設定と前の段階で学んだのでわかります。問題は「Controller」という値。これは「Controller(コントローラー)」と呼ばれるものを設定するためのものです。

 ### controller は値を管理するクラス
 Controllerはウイジェットの値を管理するための専用のクラスです。TextFieldのような入力を行うウィジェットは、自身の中に値を保管するプロパティのようなものを持っているわけではないのです。値を管理するための「Controller」というクラスを組み込み、これで値を管理します。

  Controllerは、 _controllerというフィールドとして用意します。TextFieldでは、TextEditingControllerというクラスが用意されており、このインスタンスをcontrollerに組み込む。

  ~~~
static final _controller = TextEditingController();
  ~~~
TextEditingControllerは、引数なしでインスタンスを作成します。このTextEditingControllerには「text」というプロパティが用意されており、これがウィジェットに入力されたテキストとなります。このtextプロパティの値を読み書きすることで、textEditingControllerを組み込んだウィジェットのテキストを扱うことができます。

buttonPressedメソッドのsetStateでは、以下のような値を利用する。
~~~
_message = 'you said:' + _controller.text;
~~~
 _controller.textで、入力したテキストを取り出し、それを利用して_messageにテキストを設定しているわけである。UIウィジェットを使うには、そのControllerを利用する、というのが基本的考え方。


 ### onChanged イベントの利用
 ここでは、ボタンをクリックしたときのonPressedイベントによる処理でテキストを表示しました。
 「onChanged」これは、テキストが修正されると発生するイベントです。これを利用することで、テキストを編集している間、リアルタイムに入力値を利用した処理を行わせることもできます。

 #### | onChangedメソッドの定義
  TextFieldインスタンスを作成している部分を見てみると、以下のようにしてonChangedイベントの設定がされているのかがわかります。

  > onChanged: textChanged,

  ここでは、textChangedというメソッドが指定されています。このメソッドの定義は、クラス定義の一番最後に以下のように用意されています。

  ~~~
void textChanged(String val){
  setState((){
        _message = val.toUpperCase();
});
  ~~~

  引数にString値が用意されています。
これが、変更されたウィジェットのテキストになります。その中では、  onPressedの場合と同様に、setStateが用意されています。StatefulWidgetのステートを操作する場合は、常にsetStateを使います。これはイベントの種類や操作するウィジェットが変わっても同じです。ここでは、toUpperCaseメソッドで引数valのテキストをすべて大文字にしてメッセージに設定してあります。

#### |Checkboxについて
ON OFFといった二者択一の値を入力するのに用いられるが「チェックボックス」です。これは「Checkbox」というクラスとして用意されています。

#### Checkboxの利用例
~~~
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _checked = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(10.0),
              child: Row(
                  mainAxisAlignment: MainAxisAlignment.start,
                  mainAxisSize: MainAxisSize.max,
                  crossAxisAlignment: CrossAxisAlignment.end,
                  children: <Widget>[
                    Checkbox(
                      value:_checked,
                      onChanged: checkChanged,
                    ),
                    Text(
                      "Checkbox",
                      style: TextStyle(fontSize:28.0,
                          fontWeight: FontWeight.w400,
                          fontFamily: "Roboto"),
                    )
                  ]
              )
            ),
          ],
        ),
      ),
    );
  }

  void checkChanged(bool? value){
    setState(() {
      _checked = value!;
      _message = value ? 'checked!' : 'not checked...';
    });
  }

}


~~~

このコードを実行すると、チェックボックスが１つだけ表示されます。このチェックボックス部分をクリックするとチェックがON/OFFされます。同時に、チェックボックスの上に「checked!」「notchecked...」といったテキストが表示されます。
##### |Checkboxの基本
では、checkboxインスタンスを作成している部分を見てみましょう。
~~~
Checkbox(
   value:<<bool>>,
  onChanged: 関数,
),
~~~

 valueは、チェックの状態を示すもので、bool値で指定をします。trueならばON,falseならばOFFになります。onChangedは、チェック状態が変更された際に発生するイベントの処理を指定するためのものです。ここにメソッドを指定すれば、チェックボックスを操作した際に処理を自動的に呼び出すことができる。

 ~~~
void checkChanged(bool? value){
   setState(() {
     _checked = value!;
     _message = value ? 'checked!' : 'not checked...';
   } );
}
 ~~~

 引数にはbool値が１つ渡されています。これは、現在のチェックの状態を表す値です。その中では、setStateで_checkedと_messageの値を変更している。これで、checkboxのチェック状態とTextのメッセージ変更される。
 　_checkedの変更が一番重要です。ここではCheckboxを作る際、value:_checkedというようにvalueに_checkedを代入している。それにより、setStateを変更すれば、valueの値が変わり、チェック状態も変更される。

 ## Switchについて
 このウィジェットもCheckbox同様、ON OFFをクリックで決めるものです。基本はCheckboxと同じで、自分ではあまりつかわないと判断したので利用例は省きます。

 ## Radio　Radioの利用例　について
 複数の項目から１つを選ぶものです。

 ・Radioの利用例
 ~~~
class _MyHomePageState extends State<MyHomePage> {
  static var _message = 'ok.';
  static var _selected = 'A';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('App Name'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Padding(
              padding: EdgeInsets.all(20.0),
              child: Text(
                _message,
                style: TextStyle(
                  fontSize: 32.0,
                  fontWeight: FontWeight.w400,
                  fontFamily: "Roboto"),
              ),
            ),

            Padding(
              padding: EdgeInsets.all(10.0),
            ),

            Row(
                mainAxisAlignment: MainAxisAlignment.start,
                mainAxisSize: MainAxisSize.max,
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[

                  Radio<String>(
                    value: 'A',
                    groupValue: _selected,
                    onChanged: checkChanged,
                  ),
                  Text(
                    "radio A",
                    style: TextStyle(fontSize:28.0,
                      fontWeight: FontWeight.w400,
                      fontFamily: "Roboto"),
                  )
                ]
            ),

            Row(
                mainAxisAlignment: MainAxisAlignment.start,
                mainAxisSize: MainAxisSize.max,
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[

                  Radio<String>(
                    value: 'B',
                    groupValue: _selected,
                    onChanged: checkChanged,
                  ),
                  Text(
                    "radio B",
                    style: TextStyle(fontSize:28.0,
                      fontWeight: FontWeight.w400,
                      fontFamily: "Roboto"),
                  )
                ]
            ),
          ],
        ),
      ),
    );
  }

  void checkChanged(String? value){
    setState(() {
      _selected = value ?? 'nodata';
      _message = 'select: $_selected';
    });
  }
}


 ~~~

 このコードを実行すると、２つのラジオボタンが表示されます。ボタンをクリックすると、そのボタンが選択され、上に「select:○○」と選択したボタン名が表示される。

 ### |Radioの仕組み

 ~~~
Radio<型>(
   value: 値,
   groupValue: 値,
  onChanged:...メソッド...,
)
 ~~~

Radioで重要となるのは**型**です。Radioを、使う時最初に考えるものが「どんな値を、各ボタンの値として利用するか」。

Radioにはvalueプロパティがあり、これで各Radio固有の値を設定される。この値はどんなものでも入れられます。ただし、「これを使う」となったら、そのRadioを含むグループのすべてのRadioで同じ型をvalueとして使わなければいけない。

例えば、ここではStringの値をvalueとして使っています。Radio作成部分をみるとこんな感じです。
~~~
Radio<String>(
    value:'A',
    groupValue: _selected,
    onChanged: checkChanged,
),
~~~
Stringを値として利用するため、 Radio<String>(...)という形でインスタンスを作成しています。valueには、各Radioごとに固有の値を設定しておく。

### |gourpValueとは？
　　
その後の「***groupValue***」は、グループで選択された値を示します。例えば、ここではvalue:'A'と、value:'B'のRadioが用意されています。value:'A'のRadioが選択されていたなら、groupValueの値は'A'となります。そしてvalue:'B'のRadioが選択されたなら、groupValueは'B'。

　ここでは、_selectedというString型のフィールドを用意し、これをgroupValueに設定しています。これで、Radioをクリックして選択したとき、_selectedの値をクリックしたRadioのvalueに変更すれば、そのRadioが選択された状態に変わる、というわけです。

選択状態が変更されると、onChangedイベントが発生します。ここでは、onChanged:cehckChangedとしてcheckChangedメソッドが設定されています。このメソッドの処理はいかのようになっている。
~~~
void checkChanged(String? value){
    setState(() {
      _selected = value ?? 'nodata';
      _message = 'select $_selected';
  });
}
~~~
 引数にはString値が渡されている。これが、選択されたRadioのvalueです。この値を、groupValueに設定してある_selectedに代入することで、そのRadioが選択された状態と認識される。

 ## DropdownButtonについて
 　ラジオボタンのように複数の項目から一つ選ぶようなUIと同じです。このボタンはクリックするとメニューが現れ、そこから項目を選ぶとそれが表示される、というものです。

 ### | DropdownButtonの基本形
まずは基本形を整理します
~~~
DropdownButton<型>(
    onChanged: 関数,
    value:　値,
    style:<<TextStyle>>,
    items:[<<DropdownMwnuItem>>,...]
)
~~~
onChangedは、値が変更されたときのイベント処理。valueは、選択された値です。そしてitemsには、表示する項目の情報をまとめておく。

このDrokpdownButtonも、先ほどのRadioと同様に「どんな型を値として利用するか」を考えて設計する必要があります。インスタンスは、DropdownButton<型>(...)というように、型を指定して作成します。valueはこの型の値になる。

itemsに用意するメニュー項目の情報も、この型が重要になります。メニュー項目は、「***DropdownMenultem***」というクラスのインスタンスとして作成します。このインスタンスの配列を作成し、itemsに設定する。
~~~
DropdownMenuItem<型>(value:　値, child: ウィジェット)
~~~


引数には、valueでそのDropdownMenuItemの値を指定します。これは<型>で指定された型の値でなければならない。childには、このメニュー項目内に組み込まれるウィジェットを指定します。通常はTextを使い、メニュー項目に表示されるテキストを指定する。

onChangedの部分は基本変わりません。

## PopupMenuButton
 DropdownButtonと似たようなもの「PopupMenuButton」というものもある。これはポップアップメニューを呼び出すための専用ボタンです。どんなものかというと、一般のアプリでは画面の右上あたりにある３つの点のやつです。

 利用例
 ~~~
Align(alignment: Alignment.centerRight,
  child: PopupMenuButton(
    onSelected: (String value)=> popupSelected(value),
    itemBuilder: (BuildContext context) =>
    <PopupMenuEntry<String>>[
      const PopupMenuItem( child: const Text("One"), value: "One",),
      const PopupMenuItem( child: const Text("Two"), value: "Two",),
      const PopupMenuItem( child: const Text("Three"), value: "Three",),
    ],
  ),
),
 ~~~

実行すると、画面上部のテキストの右下あたりに「３つの点」マークが表示されます。これをクリックすると、メニューがポップアップして現れます。ここからメニュー項目を選ぶと、選んだメニューの値がメッセージとして表示されます。

ここではonSelectedに先のサンプルと全く同じでpopupSelectedメソッドを割り当てています。メソッドはそのままで変更していないのでDropdownButtonがそのままPopupMenuButtonに置き換わっただけで、同じ処理を実行しています。
 
 ### |PopupMenuEntryとPopupMenultem
 ここでは、「itemBuilder」というものにメニュー項目の情報がまとめられている。いかのようになっている。
 ~~~
itemBuilder:(BuildContext context) =><PopupMenuEntry<型>>[...]
 ~~~

 ***BuildContext***というクラスのインスタンスを引数として渡す形で、***PopupMenuEntry***のリストを用意しています。BuildContextはウィジェット類のベースとなっているクラスである。このリストでは、PopupMenuEntryにはPopupMenultemというPopupMenuEntryのサブクラスを使っている。
 ~~~
const PopupMenuItem( child: ウィジェット, value: 値,),
 ~~~
 このように、valiueにこのPopuMenuItemの値を、そしてChildにはメニュー項目内に表示するウィジェット（通常はText）を用意します。このあたりの使い方は、DropdownMenuItemとほとんど同じです。クラス名が異なるだけです。

 ## Slider
 数値をアナログ的に入力するのに用いられるものです。ドラックして動かすノブがあり、それを左右にスライドして値を決めるものです。

 ###  |　Sliderの基本形
 Sliderは多くのプロパティを持っています。しかし、一般的に利用されるプロパティはそう多くはないです。整理すると以下のようになります。
 ~~~
Slider(
   onChanged:関数,
   min:<<double>>,
   max:<<double>>,
   divisions:<<int>>,
   value:<<double>>,
   ),
 ~~~

| onChanged | min | max | divisions | value 
| --- | --- | --- | --- | --- |
変更時のイベント処理。ドラッグ中、値が変わるたびに呼び出される。　| 最小値　| 最大値　|　分割数。例えばmin:0 max:10　でdivisions:10ならば、１ずつ値が選択される。省略される場合実数のままなめらかに値が変更する。 | 現在選択されている値　|

divisionsは、実数で値を取り出し利用する場合は必要ない。

# 3-3 アラートとダイアログ
## showDialog関数について
UIというのは、最初から画面に表示されているものばかりではない。必要に応じて画面に現れるものもある。アラートやダイアログと呼ばれるものです。

　アラートなどを画面に表示するには「***showDialog***」という関数を利用します。この関数は以下のような形をしている。
~~~
showDialog(
   context:<<BuildContext>>,
    builder:<<WidgetBuilder>>
)
~~~
contextには、***BuildContext***インスタンスを指定します。このBuildContext、前にも一度登場しています。なので利用例はあげず、基本に移ります。

### showDialogの基本
まずはコードの確認。ここでは、ボタンをクリックしたときに呼び出されるbuttonPressedメソッドの中でshowDialogを呼び出している。
~~~
showDialog(
   context: context,
    builder: (BuildContext context) => AlertDialog(...),
)
~~~
contextは、contextをそのまま指定しています。これはStateクラスに用意されているプロパティです。Stateクラスはウィジェットの状態を扱うためのものなので、これ単体で存在することはないです。必ず、何らかのウィジェットに関連付けられる。

　関連付けられたウィジェット（BuildContext = ウィジェットツリーにおけるウィジェットのハンドル）を保管しているのがcontextプロパティです。このStateにあるcontextをそのままshowDialogのcontextに代入すれば、このウィジェット上にアラートを表示することができます。

### AlertDialogについて
もう１つのbuilderには、「AlertDialog」というクラスを用意している。これは以下のような形でインスタンスを作成します。
~~~
AlertDialog(
   title: ウィジェット,
    content: ウィジェット
)
~~~
タイトルとコンテンツとして表示するウィジェットをそれぞれtitleとcontentに指定する。これをshowDialogで表示させればいいのです。

## アラートにボタンを追加する
　アラートは、単にメッセージを表示するだけでなく、さまざまな働きを用意することができます。一番一般的なのは「ボタン」になります。いくつかのボタンを表示し、クリックしたボタンに応じて処理を行う、という処理はよく用いられる。例えば「OK」「Cancel」といったボタンを用意し、どちらをクリックしたかで処理を変えるというものです。
 

AlertDialogには「actions」というプロパティが用意されている。これは以下のようになる。
~~~
actions:<Widget>[...ウィジェットのリスト...]
~~~

actionsにはウィジェットのリストを用意します。通常、これはボタン関係のインスタンスが用いられます。それぞれのボタンをクリックしたときの処理を用意することで、さらにアラートが閉じたあとの処理を用意することで、選択したボタンに応じた処理を作ることができます。

　また、いくつかのボタンを表示させる場合は、アラートを閉じた後の処理も必要となります。これは、ボタンのonPressedなどとは別に、showDialog後に記述します。
~~~
showDialog(...).then<void>(...処理...)
~~~

このように、showDialogのあとに「then」というメソッドを用意し、そこに実行する処理を用意する。「then」は、showDialogのコールバック関数を指定するものです。showDialogは非同期に実行されるメソッドになる。このためアラートダイアログを閉じた後の処理はコールバック関数として用意しなければいけない。

**「then」はそれをシンプルに実装できるメソッドになります。**

### アラートのボタンを利用する

~~~
void buttonPressed(){
  showDialog(
    context: context,
    builder: (BuildContext context) => AlertDialog(
      title: Text("Hello!"),
      content: const Text("This is sample."),
      actions: <Widget>[
        TextButton(
            child: const Text('Cancel'),
            onPressed: () => Navigator.pop<String>(context, 'Cancel')
        ),
        TextButton(
            child: const Text('OK'),
            onPressed: () => Navigator.pop<String>(context, 'OK')
        )
      ],
    ),
  ).then<void>((value) => resultAlert(value));
}

void resultAlert(String value) {
  setState((){
    _message = 'selected: $value';
  });
}

~~~
このコードをshowDialogと合わせると、アプリのボタンをクリックすると、画面にアラートが表示される。そしてメッセージの下に「Cancel」「OK」という２つのボタンが表示されます。これらのボタンを押すとアラートは消え、「selected:○○」と選択したボタンがメッセージとして表示されます。

#### |actionsのボタンについて

showDialogのactionsにWidgetリストを用意し、その赤にTextButtonを２つ用意しています。これが、ボタンとして表示されたものになります。それぞれのTextButtonで、クリックした際の処理を以下のように用意している。
~~~
onPressed:　( ) => Navigator.pop<String>(context,'Cancel')
~~~

Navigator.popは、表示されているアラートダイアログを消す働きがあります。これはContextと、アラートを閉じる際に送られる値を引数に指定しています。この値は、どんなものでもいいですが、あらかじめ「どういう型の値か」を決めてコーディングする必要がある。
　　
### thenによるアラート後の処理
では、アラートが閉じたあとの処理はどうしているか？これは、thenメソッドの中で行っている。ここでは以下のように処理を描いています。
~~~
then<void>((value) => resultAlert(value));
~~~
　
これにより、resultAlertメソッドがコールバックとして呼び出されるようになります。このとき、valueという引数が渡されますが、これは、Navigator.popの第二引数に指定された値が格納される。

## SimpleDialogとは？
ダイアログは、アラートのようにメッセージを表示するだけでなく、ユーザーに何らかの入力をしてもらうものもある。複数の項目から１つを選ぶような入力は「**SimpleDialog**」というクラスがある。

　これはAlertDialogと同じくDialogというクラスを継承して作られたものになります。このクラスは以下のようにしてインスタンスを作成します。
~~~
SimpleDialog(
   title:ウィジェット,
    children:[ウィジェットのリスト],
)
~~~
 titleとchildrenという2つの値を用意します。titleには、タイトルのテキストなどを設定します。通常はTextを指定するのですが、childrenには、選択肢として表示する項目のリストを用意します。これは通常「**SimpleDialogOption**」というクラスのインスタンスを指定する。

 ###  |SimpleDialogOptionについて
 このクラスはSimpleDialogの選択肢の項目として使う専用のクラスです。
 ~~~
SimpleDialogOption(
  child:ウィンドウ,
  onPressed:...処理...,
)
 ~~~

 childには、項目内に表示するウィジェットを指定します。テキストを表示するだけなら、Textだけでも大丈夫です。onPressedには、その項目をクリックしたときの処理を用意します。これはダイアログを閉じた後の処理ではありません。ダイアログを閉じるなど、項目を選択したときの基本的な処理を用意します。


 # 複雑な構造のUIウィジェット

 





















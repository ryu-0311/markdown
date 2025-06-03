# flutterについて
<<<<<<< HEAD

プロジェクトのファイル構成について
- Flutterプロジェクトには多くのフォルダが含まれており、それぞれのプラットフォーム（Android、iOS、Windows、Web など）に関連するファイルが格納される。
- .dart_tool は Dart 言語が自動生成するファイル類を保管するフォルダ。
- lib フォルダには Dart のスクリプトが保存され、test フォルダはユニットテスト関連のファイルを管理する。
- .gitignore や pubspec.yaml などのファイルは、パッケージ管理やコード解析などに使用される重要な設定ファイル。
=======
>>>>>>> d851d9f30695161d8367d5ee150c4b28d0b9ab97



import 'package:flutter/material.dart';

void main() {
  runApp(new MyApp());
}
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Generated App',
      theme: new ThemeData(
        primarySwatch: Colors.blue,
        primaryColor: const Color(0xFF2196f3),
        accentColor: const Color(0xFF2196f3),
        canvasColor: const Color(0xFFfafafa),
      ),
      home: new MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key}) : super(key: key);
  @override
  _MyHomePageState createState() => new _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
    @override
    Widget build(BuildContext context) {
      return new Scaffold(
        appBar: new AppBar(
          title: new Text('App Name'),
          ),
      );
    }

    
















































}
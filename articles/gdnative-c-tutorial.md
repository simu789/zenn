---
title: "GDNative C　チュートリアル　詰まった所メモ"
emoji: "😽"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["godot","GDNative"]
published: true
---
Godot Documentの記事[GDNative Cの例](https://docs.godotengine.org/en/stable/tutorials/scripting/gdnative/gdnative_c_example.html#doc-gdnative-c-example)で詰まったところを記します。
## 手順
1. 指定されたgitファイルを用意
2. コンパイル
3. Godot Engine 上での設定

### 1.指定されたgitファイルを用意
まずは適当なプロジェクト用のフォルダを用意（今回はGDNative_test1にした）。
```cd GDNative_test1```
で移動したら
```git clone https://github.com/godotengine/godot-headers.git```
でリポジトリを引っ張ってくるのですが、そのままではmasterブランチなのでコンパイルする際に**gdnative_api_struct.gen.h**がないのでエラーとなります。

なので、
```git checkout godot-3.4.5-stable```
このコマンドで使用しているGodotEngineのバージョンへとcheckoutしてブランチを切り替える必要があります。

切り替えると例のヘッダーファイルが作成されるので、コンパイルが可能になります。
### 2.コンパイル
srcフォルダにcdコマンドで移動したら各OSに対応したコンパイルコマンドを打ち込みます。

その際、2行目のコマンドにおいて指定するディレクトリが
```../simple/bin/libsimple.so```
なのですが、1番上で先に[GDNative-demos repository](https://github.com/godotengine/gdnative-demos/tree/master/c/simple)というgitファイルを導入している場合、フォルダ名がsimpleではなくprojectになっているので、フォルダを見つけられずエラーとなるので、こちらもブランチを切り替えるかフォルダ名を変更しておきます。これで他に問題がなければ通ると思います。
### 3.Godot Engine 上での設定
あとはsimpleフォルダからgodotプロジェクトを立ち上げ、任意のディレクトリに「GDNativeLibrary」リソースを作成し、手順通り各コンパイラから生成したファイルを設定します。

そして手順通り保存すれば、最後にNativeScriptを作成するのですが、ファイルシステムタブから作成すると設定で手間取るので、libsimple.gdnlibを選択した状態で、インスペクタータブから新規ファイル作成ボタンを押し「NativeScript」リソースを作成します。

あとは手順通りに設定して、プロジェクトを起動してボタンを押すと文字が表示されて一応の完成となるはずです。

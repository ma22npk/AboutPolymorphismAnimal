# AboutPolymorphismAnimal
【Java】ポリモーフィズムの学習で用いた動物の鳴き声を出力するプログラム
<!-- タイトル -->
# ポリモーフィズム
「中に入るものによって同じ[メソッド]でも違う処理を行える」というプログラミング言語自体の特徴のこと。

<!-- 説明 「なにをするものか」-->
## 【説明】

<!-- ポリモーフィズムとは -->
結論、ポリモーフィズムは「 *呼び出す関数が呼び出し元に適した振る舞いをすること* 」。

[Wikipedia「ポリモーフィズム」]には以下のように書かれていました。

> 「プログラミング言語の型システムの性質を表すもので、プログラミング言語の各要素（定数、変数、式、オブジェクト、関数、メソッドなど）についてそれらが複数の型に属することを許すという性質を指す。」

正直、自分には難解でしたが、つまりは「*大量の同じ処理を一つの[メソッド]でまとめて処理する」ようにすることで、短いコードで管理がしやすく、修正に強いコードにすること*」が「 **ポリモーフィズム** 」であると思いました。

ポリモーフィズム(和訳: 多相性)は、[オブジェクト指向]三大要素([継承], [カプセル化], ポリモーフィズム)の1つで、そのなかでも一番理解が難しいとされます。
「ポリモーフィズム的」な考え方の目的についてのまとめが以下です。

- 親[クラス]生成時に子[クラス]に渡すメッセージを共通にする
- [インターフェース]を使って(Javaの場合)メッセージを共通にする
- コードの重複を排除して汎用性の高い部品をつくる


<!-- メリット「使うことのメリット」 -->
## 【メリット】
ポリモーフィズムを利用しない場合とプログラムと比較して、このようなメリットがあります。

- 記述量が減ることで、修正が加えやすくなる
- コードがきれいにまとまる
- 変更に強い柔軟性があり修正やテストにかかるコストが少ない

<!-- ここから 各キャプチャー△▽△▽△▽△▽△▽△▽△▽△▽△ -->

<!-- ここから サンプルコード ★☆★☆★☆★☆★ -->
<!-- サンプルコードタイトル -->
## 【サンプルコード】 ポリモーフィズムを使ってコードの重複を減らす

以下のプログラムは *親[クラス]に「Animal」,子[クラス]に「Cat」や「Dog」などのそれぞれ複数の動物クラスを作成し、「鳴き声を表示する[メソッド]」をそれぞれで出力する* ものです。
つまり、以下のような実行結果をするということです。

### 【Animal.java】親クラス

```java
package about_polymorphism;

abstract class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    // 食べ物の味を出力。
    public void letsHear() {
        System.out.println(name + "は" + call() + "と鳴く");
    }

    // 「抽象メソッドの呼び出し」ため、abstract修飾子を使用。
    // 具象クラスからのみアクセスするため、protected修飾とする
    abstract protected String call();
}
```
### 【各種子クラス】

```java
//【Dog.java】
package about_polymorphism;

public class Dog extends Animal {
    public Dog() {
        super("犬");
    }

    protected String call() {
        return "バウバウ";

    }
}
//【Cat.java】
package about_polymorphism;
// 抽象クラスの Animalを　継承
public class Cat extends Animal{
    public Cat() {
        super("ネコ");
    }

    protected String call() {
        return "にゃーん";

    }
}

//【Cow.java】
package about_polymorphism;

public class Cow extends Animal {
    public Cow() {
        super("牛");
    }

    protected String call() {
        return "ブルルルルル";

    }
}
//【Horse.java】
package about_polymorphism;

public class Horse extends Animal {
    public Horse() {
        super("馬");
    }
    protected String call() {
        return "ヒヒーン";

    }
}

```

<!-- 実行結果 -->
### 【実行結果】

```
ネコはにゃーんと鳴く
犬はバウバウと鳴く
牛はブルルルルルと鳴く
馬はヒヒーンと鳴く
```

## ポリモーフィズムを使わない場合

ポリモーフィズムな書き方をしないと、以下のように 「行数が多く、同じことを何度も記述」しているコードになっている点に注目です。

### 【Main.java】

```java
package about_polymorphism;

public class Main {

    public static void main(String[] args) {
        // ネコクラスの インスタンス 生成
        Cat cat = new Cat();
        // 鳴き声を表示する メソッドの呼び出し
        cat.letsHear();

        // 犬クラスの インスタンス 生成
        Dog dog = new Dog();
        // 鳴き声を表示する メソッドの呼び出し
        dog.letsHear();

        // 牛クラスの インスタンス 生成
        Cow cow = new Cow();
        // 鳴き声を表示する メソッドの呼び出し
        cow.letsHear();

        // 馬クラスの インスタンス 生成
        Horse horse = new Horse();
        // 鳴き声を表示する メソッドの呼び出し
        horse.letsHear();
    }
}
```

## ポリモーフィズムな書き方の場合
上記のコードを下記のようなポリモーフィズム的な書き方で スッキリさせることができます。

```
親クラス 配列 = {new 子クラス(),new 子クラス(),new 子クラス(),new 子クラス()..};
for (親クラス 変数 :配列) {
  変数.メソッド();
}
```

### 【Main.java】 ポリモーフィズム化

- インスタンス化を一気にまとめて行い配列に格納
- 「定義した子クラス全部で、それぞれメソッドを呼び出す」を拡張for文（for文でも）を用いて行う。



<!-- サンプルコード -->
```java
public class Main {

    public static void main(String[] args) {
      //それぞれのオブジェクトのポインタを格納する配列を用意
        // 子クラスのインスタンス化を 配列内に入れてひとくくりに行う
      Animal[] animals = { new Cat(), new Dog(), new Cow(),new Horse()};
      
      // 「定義した子クラス全部で、それぞれメソッドを呼び出す」を拡張for文（for文でも）を用いて行う。
        for (Animal a : animals) {
            a.letsHear();
        }
    }
}
```
<!-- サンプルコード説明があればここに記述 -->
行数が一気にスッキリしました。
このコードの良いところはスッキリしているだけでなく、「**修正に強い**」というのも強みです。仮にここに新しく子クラスを追加することになったとしても

- 動物クラスの配列に追加分のインスタンスを書くだけなので行数自体は増えない
- 中心的なソースをいじることなく修正することなく修正が可能

コードがきれいにまとまり、修正が加えやすく、変更に強い柔軟性があり、修正やテストにかかるコストが少ないという、いわゆる<font color="Blue">「**良いコード**」</font>を実現しました。



<!-- ここまで サンプルコード ★☆★☆★☆★☆★ -->

<!-- ここまで 各キャプチャー△▽△▽△▽△▽△▽△▽△▽△▽△ -->

<!-- まとめ -->
## 【まとめ】
ポリモーフィズムなプログラムというのは、結果的に *DRYの原則(同じことを二度書かない*)に従ったプログラムとも言えるかもしれません。

## 参考文献・記事

- [Wikipedia「ポリモーフィズム」]
- [Javaのポリモーフィズムについて現役エンジニアが解説【初心者向け】](https://techacademy.jp/magazine/40258)
- [ポリモーフィズムとはなにか？超わかりやすく解説します！](https://jpazamu.com/polymorphism/)


<!-- 以下リンク -->
[Wikipedia「ポリモーフィズム」]:https://ja.wikipedia.org/wiki/%E3%83%9D%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%95%E3%82%A3%E3%82%BA%E3%83%A0
[Progate]:https://prog-8.com/
[ドットインストール]:https://dotinstall.com/
[Progate]:https://prog-8.com/
[ドットインストール]:https://dotinstall.com/
[abstract修飾子]:https://qiita.com/takahirocook/items/9fa0e1cbb8a4dd4e1ff4
[abstract]:https://qiita.com/takahirocook/items/9fa0e1cbb8a4dd4e1ff4
[import]:https://qiita.com/takahirocook/items/59a8a09cab6a98d3bca2
[this]:https://qiita.com/takahirocook/items/d251ec4693c68f6b9538
[super]:https://qiita.com/takahirocook/items/75a07131e7e791c8442c
[final]:https://qiita.com/takahirocook/items/5e0916d9bf28bcf68d0c
[final修飾子]:https://qiita.com/takahirocook/items/5e0916d9bf28bcf68d0c
[List]:https://qiita.com/takahirocook/items/4d622fc6f271569783b5
[list]:https://qiita.com/takahirocook/items/4d622fc6f271569783b5
[Map]:https://qiita.com/takahirocook/items/49f46151ecb5e332db32
[map]:https://qiita.com/takahirocook/items/49f46151ecb5e332db32
[set]:https://qiita.com/takahirocook/items/d498329cd26e1500f476
[Set]:https://qiita.com/takahirocook/items/d498329cd26e1500f476
[Date]:https://qiita.com/takahirocook/items/a760e20ef2d9aa5c08fc
[SimpleDateFormat]:https://qiita.com/takahirocook/items/aa857c8f2153193095e4
[Time]:https://qiita.com/takahirocook/items/9caef0bb2409caedba55
[Calendar]:https://qiita.com/takahirocook/items/204dd7331db777eb6f3b
[mainメソッド]:https://qiita.com/takahirocook/items/f4635915337303de338c
[printf()メソッド]:https://qiita.com/takahirocook/items/06d525be63eccd99ed49
[printf()関数]:https://qiita.com/takahirocook/items/06d525be63eccd99ed49
[this]:https://qiita.com/takahirocook/items/d251ec4693c68f6b9538
[getter・setter]:https://qiita.com/takahirocook/items/27828bc8477735612021
[setter]:https://qiita.com/takahirocook/items/27828bc8477735612021
[getter]:https://qiita.com/takahirocook/items/27828bc8477735612021
[new演算子]:https://qiita.com/takahirocook/items/00f9f97592bf50831d39
[new]:https://qiita.com/takahirocook/items/00f9f97592bf50831d39
[static修飾子]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[static]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
<!-- あ行 -->
[オブジェクト指向]:https://qiita.com/takahirocook/items/041ba7a096b71ab8ffd4
[継承]:https://qiita.com/takahirocook/items/6c84ea66a6e2ad536a37
[オーバーライド]:https://qiita.com/takahirocook/items/09dd8e5f56d6617ce45a
[オーバーロード]:https://qiita.com/takahirocook/items/b937c3c07126fe7e02a4
[インスタンス]:https://qiita.com/takahirocook/items/ec01cdcbb440cf0d1cc4
[インスタンス化]:https://qiita.com/takahirocook/items/ec01cdcbb440cf0d1cc4
[アクセス修飾子]:https://qiita.com/takahirocook/items/e51b0b9d37d95ad587fe
[インスタンス化]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[インスタンス変数]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[インターフェイス]:https://qiita.com/takahirocook/items/ca84be8dfef664b19194
[インターフェース]:https://qiita.com/takahirocook/items/ca84be8dfef664b19194
[インポート]:https://qiita.com/takahirocook/items/59a8a09cab6a98d3bca2
<!-- か行 -->
[拡張for文]:https://qiita.com/takahirocook/items/470b2858de1a4f99b334
[クラスメソッド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[クラスフィールド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[クラス変数]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[カプセル化]:https://qiita.com/takahirocook/items/e469a7c0539a0012868e
[クラス]:https://qiita.com/takahirocook/items/50cbbdca8e21539170e9
[コンストラクタ]:https://qiita.com/takahirocook/items/fa1822f2f22c3786593e
<!-- さ行 -->
[書式指定子]:https://qiita.com/takahirocook/items/06d525be63eccd99ed49
[静的メソッド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[静的変数]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[静的メソッド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
[スーパークラス]:https://qiita.com/takahirocook/items/75a07131e7e791c8442c
<!-- た行 -->
[定数]:https://qiita.com/takahirocook/items/5e0916d9bf28bcf68d0c
[抽象クラス]:https://qiita.com/takahirocook/items/9fa0e1cbb8a4dd4e1ff4
[抽象メソッド]:https://qiita.com/takahirocook/items/9fa0e1cbb8a4dd4e1ff4
[動的メソッド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
<!-- な行 -->
[日時の文字列操作]:https://qiita.com/takahirocook/items/aa857c8f2153193095e4
<!-- は行 -->
[パッケージ]:https://qiita.com/takahirocook/items/39b58d17abcb159ef5c1
[引数]:https://qiita.com/takahirocook/items/5e5b0ba79e869f4a592e
[配列]:https://qiita.com/takahirocook/items/16a123fb73b30869053b
[配列操作]:https://qiita.com/takahirocook/items/16a123fb73b30869053b
[日付操作]:https://qiita.com/takahirocook/items/9caef0bb2409caedba55
[フィールド]:https://qiita.com/takahirocook/items/28df75a133049a74ece1
[フィールド変数]:https://qiita.com/takahirocook/items/28df75a133049a74ece1
[インスタンスフィールド]:https://qiita.com/takahirocook/items/cf527f85d17a5af86735
<!-- ま行 -->
[戻り値]:https://qiita.com/takahirocook/items/3b6fa670a1d6dd4a9386
[メソッド]:https://qiita.com/takahirocook/items/5bfe43576d87a2a4006c
[メソッドの呼び出し]:https://qiita.com/takahirocook/items/f4635915337303de338c
<!-- や行 -->
<!-- ら行 -->
<!-- わ行 -->



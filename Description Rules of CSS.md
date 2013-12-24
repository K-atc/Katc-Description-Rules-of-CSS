K_atcなりのCSSの記述ルール
=====================

HTMLの構造をどう設計するか？
----------------------
基本的に「BEM記法」に則り，これにアレンジを加えています。

スタイル適用はHTMLタグとclassに対して行い，idはJavascript(JS)でDOM操作を行うために使うこととします。したがって，属性にidが指定されるということはclassも同時に指定されるということになります。

オーソドックスにヘッダー・サイドバー・メイン・フッターの3ブロックに分けておき，クラスを指定します。次にその下に付くグループをパネルと呼び，そのパネルににエレメントを入れていきます。これが終わると，各エレメントは階層的な従属となります。


classの命名規則
-------------
### 順番
classは以下の順番に従って付加していきます。

1. 所属するパネル名

	`article, sidebar`

2. エレメント名

	`article__tags, sidebar__items`

3. 状態

	`article__tags--null, sidebar__items--externalLink`

ただし，3が２の前に来ることや，1,2,3が繰り返す場合もあります
	
`sidebar__items--selected__sidebar__sub-items`

### ハイフンとアンダーバーの使い方

* \- （ハイフン1つ）

    スペースは使えないので単語どうしをつなげるのに使います。例えば，sub-items。

* _ （アンダーバー1つ）

	使いません。

* -- （ハイフン2つ）

	そのエレメントの状態を補足するのに使います。サイドバーでリストの中にリストがあるような場合，sidebar\_\_items--selected\_\_sidebar\_\_sub-itemsのような長く続ける書き方もありだと思います。しかしながら，これをcssファイル上で組んでいくのも大変ですからSASS（v3.3以降）を利用することをおすすめします。

* __ （アンダーバー2つ）

	エレメントとその親のグループの関係を示すのに使います。寿司で言えば「ハマチ寿司」は「寿司__ハマチ」と等価です。

### なぜこの書き方がよいのか
このようにclass名を付けることで，全体を把握セずともスタイルの適用範囲を知ることができ，引き継ぎのコストが低いことが最大のメリットとなります。

### 付け足し
* class名が階層的になるため，セレクタを使って`.sidebar > ul`のような指定は非推奨となります。


スタイルをどう適用させるか
-----------------
itemのように独立し，他のエレメントでスタイルを使いまわすことができそうでない場合を除き，`class="panel panel__1"`のように共有のスタイルと特化したスタイルを同時に指定することでスタイルの重複指定が少なくなるようにします。


CSSタグの並べ方
-----------
基本的によく使うものを上に，同類は隣接するようにします。次のリストは上にあるものがCSSまたはSASSで上に書かれるべきという意味です。

* margin [Group A]
* padding [A]
* width [A]
* Height [A]
* position [A]
* top [A]
* left [A]
* font-family [Group B]
* font-weight [B]
* color [B]
* display [Group C]
* visibility [C]
* background(url) [Group D]
* background-color [D]
* background(gradient) [D]
* border [D]
* border-radius [D]
* box-shadow [D]
* line-height [Group B']
* text-align [B']
* vertical-align [B']
* cursor [Group E]
* zoom [E]

Group B'はBに近いですが重要度が低いのでDの次に書きます。 


各CSSタグで推奨する単位
------------------
* 余白系はpx, %
* 文字系はpt, %, em
	line-heightはemが良い？
* 色はHEX値



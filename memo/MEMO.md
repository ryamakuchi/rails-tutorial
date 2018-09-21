Ruby on Rails チュートリアル


## 演習デモ

1. Ruby on Railsで使うRuby gemはどのWebサイトにありますか？
* https://rubygems.org/

2. 現時点でのRailsの最新バージョンはいくつですか？
* 5.2.1 (2018/09/08 現在)
* https://rubygems.org/gems/rails

3. Ruby on Railsはこれまでに何回ダウンロードされたでしょうか？調べてみてください。
* 142,669,111 (2018/09/08 現在)
* https://rubygems.org/gems/rails


## 1.3.2 rails server

1. デフォルトのRailsページに表示されているものと比べて、今の自分のコンピュータにあるRubyのバージョンはいくつになっていますか? コマンドラインでruby -vを実行することで簡単に確認できます。
* `ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-linux]`

2. 同様にして、Railsのバージョンも調べてみましょう。調べたバージョンはリスト 1.1でインストールしたバージョンと一致しているでしょうか?
* `Rails 5.1.6`


## 1.3.4 Hello, world!

1. リスト 1.7のhelloアクションを書き換え、「hello, world!」の代わりに「hola, mundo!」と表示されるようにしてみましょう。
* OK

2. Railsでは「非ASCII文字」もサポートされています。「¡Hola, mundo!」にはスペイン語特有の逆さ感嘆符「¡」が含まれています
* OK

3. リスト 1.7のhelloアクションを参考にして、２つ目のアクションgoodbyeを追加しましょう。このアクションは、「goodbye, world!」というテキストを表示します。リスト 1.9のルーティングを編集して、ルートルーティングの割り当て先をhelloアクションからgoodbyeアクションに変更します
* OK


## 1.5.3 Herokuにデプロイする (2)

1. 1.3.4.1と同じ変更を行い、本番アプリでも「hola, mundo!」を表示できるようにしてください。
* OK

2. 1.3.4.1と同様、ルートへのルーティングを変更してgoodbyeアクションの結果が表示されるようにしてください。またデプロイ時には、Git pushのmasterをあえて省略し、git push herokuでデプロイできることを確認してみてください。
* OK


## 2.2.1 ユーザーページを探検する

1. CSSを知っている読者へ: 新しいユーザーを作成し、ブラウ���のHTMLインスペクター機能を使って「User was successfully created.」の箇所を調べてみてください。ブラウザをリロードすると、その箇所はどうなるでしょうか?
* 要素の中の文字だけ消える(Rubyの変数が出力されている?)

2. emailを���力せず、名前だけを入力しようとした場合、どうなるでしょうか?「@example.com」のような間違ったメールアドレスを入力して更新しようとした場合、どうなるでしょうか?
* 更新されてしまう

3. 上記の演習で作成したユーザーを削除してみてください。ユーザーを削除したとき、Railsはどんなメッセージを表示するでしょうか?
* `User was successfully destroyed.`


## 2.2.2 MVCの挙動

1. 図 2.11を参考にしながら、/users/1/edit というURLにアクセスしたときの振る舞いについて図を書いてみてください。
![MVCの振る舞い](./images/618D1198F83F25F058242FC0E900C889.png)

2. 図示した振る舞いを見ながら、Scaffoldで生成されたコードの中でデータベースからユーザー情報を取得しているコードを探してみてください。
```
# app/controllers/users_controller.rb
# Never trust parameters from the scary internet, only allow the white list through.
    def user_params
      params.require(:user).permit(:name, :email)
    end
```

ユーザーの情報を編集するページのファイル名は何でしょうか?
* edit.html.erb


## 2.3.1 マイクロポストを探検する

1. CSSを知っている読者へ: 新しいマイクロポストを作成し、ブラウザのHTMLインスペクター機能を使って「Micropost was successfully created.」の箇所を調べてみてください。ブラウザをリロードすると、その箇所はどうなるでしょうか?
* `<p id="notice">Micropost was successfully created.</p>`となっている。多分変数。リロードすると消える。

2. マイクロポストの作成画面で、ContentもUserも空にして作成しようとするどうなるでしょうか?
* `Micropost was successfully created.` 空のまま作られる。

3. 141文字以上の文字列をContentに入力した状態で、マイクロポストを作成しようとするとどうなるでしょうか? (ヒント: WikipediaのRubyの記事にある１段落目がちょうど150文字程度ですが、どうなりますか?)
* 141文字以上のデータが登録される

4. 上記の演習で作成したマイクロポストを削除してみましょう。
* OK


## 2.3.2 マイクロポストをマイクロにする

1. 先ほど2.3.1.1の演習でやったように、もう一度Contentに141文字以上を入力してみましょう。どのように振る舞いが変わったでしょうか?
* バリデーションエラーになった

2. CSSを知っている読者へ: ブラウザのHTMLインスペクター機能を使って、表示されたエラーメッセージを調べてみてください。
```
<div id="error_explanation">
  <h2>1 error prohibited this micropost from being saved:</h2>

  <ul>
    <li>Content is too long (maximum is 140 characters)</li>
  </ul>
</div>
```
これが表示されていて、これもリロードすると消えた。


## 2.3.3 ユーザーはたくさんマイクロポストを持っている

1. ユーザーのshowページを編集し、ユーザーの最初のマイクロポストを表示してみましょう。同ファイル内の他のコードから文法を推測してみてください (コラム 1.1で紹介した技術の出番です)。うまく表示できたかどうか、/users/1 にアクセスして確認してみましょう。
```
<p>
  <strong>first micropost:</strong>
  <%= @user.microposts.first.content %>
</p>
```

2. リスト 2.16は、マイクロポストのContentが存在しているかどうかを検証するバリデーションです。マイクロポストが空でないことを検証できているかどうか、実際に試してみましょう (図 2.16のようになっていると成功です)。
![OK](./images/2D81DB7796FC0448889C8ECF01057062.png)

3. リスト 2.17のFILL_INとなっている箇所を書き換えて、Userモデルのnameとemailが存在していることを検証してみてください (図 2.17)。
![OK](./images/A9AA8612F9303F76F24CB744D94E349F.png)


## 2.3.4 継承の階層

1. Applicationコントローラのファイルを開き、ApplicationControllerがActionController::Baseを継承している部分のコードを探してみてください。
```
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
```

2. ApplicationRecordがActiveRecord::Baseを継承しているコードはどこにあるでしょうか? 先ほどの演習を参考に、探してみてください。ヒント: コントローラと本質的には同じ仕組みなので、app/modelsディレクトリ内にあるファイルを調べてみると...?)
```
# app/models/application_record.rb
class ApplicationRecord < ActiveRecord::Base
  self.abstract_class = true
end
```


## 2.3.5 アプリケーションをデプロイする

1. 本番環境で２〜３人のユーザーを作成してみましょう。
![OK](./images/B3CC33503C0D0F08FA3A849DBE54C007.png)

2. 本番環境で最初のユーザーのマイクロポストを作ってみましょう
![OK](./images/A915F67BE8B06A57C591565A7F1E85E3.png)

3. マイクロポストのContentに141文字以上を入力した状態で、マイクロポストを作成してみましょう。リスト 2.13で加えたバリデーションが本番環境でもうまく動くかどうか、確認してみてください。
![OK](./images/18913B9EDB55A9966BF2729B5143033B.png)


## 3.1 セットアップ

1. BitbucketがMarkdown記法のREADME (リスト 3.3) をHTMLとして正しく描画しているか、確認してみてください。
* Githubで確認した

2. 本番環境 (Heroku) のルートURLにアクセスして、デプロイが成功したかどうか確かめてみてください。
* できてた


## 3.2.1 静的なページの生成

1. Fooというコントローラを生成し、その中にbarとbazアクションを追加してみてください。
* `rails generate controller Foo bar baz`

2. コラム 3.1で紹介したテクニックを駆使して、Fooコントローラとそれに関連するアクションを削除してみてください。
* `rails destroy controller Foo bar baz`


## 3.4.2 タイトルを追加する (Green)

1. StaticPagesコントローラのテスト (リスト 3.24) には、いくつか繰り返しがあったことにお気づきでしょうか? 特に「Ruby on Rails Tutorial Sample App」という基本タイトルは、各テストで毎回同じ内容を書いてしまっています。そこで、setupという特別なメソッド (各テストが実行される直前で実行されるメソッド) を使って、この問題を解決したいと思います。まずは、リスト 3.30のテストが green になることを確認してみてください (リスト 3.30では、2.2.2で少し触れたインスタンス変数や文字列の式展開というテクニックを使っています。それぞれ4.4.5と4.2.2で詳しく解説するので、今はわからなくても問題ありません)。
* GREENになった
* 3 runs, 6 assertions, 0 failures, 0 errors, 0 skips


## 3.4.3 レイアウトと埋め込みRuby (Refactor)

1. サンプルアプリケーションにContact (問い合わせ先) ページを作成してください16 (ヒント: まずはリスト 3.15を参考にして、/static_pages/contactというURLのページに「Contact | Ruby on Rails Tutorial Sample App」というタイトルが存在するかどうかを確認するテストを最初に作成しましょう。次に、3.3.3でAboutページを作ったときのと同じように、Contactページにもリスト 3.40のコンテンツを表示してみましょう。)。
![OK](./images/5AE16398FBDD39C3C85E932B1ED531BD.png)


## 3.4.4 ルーティングの設定

1. リスト 3.41にrootルーティングを追加したことで、root_urlというRailsヘルパーが使えるようになりました (以前、static_pages_home_urlが使えるようになったときと同じです)。リスト 3.42のFILL_INと記された部分を置き換えて、rootルーティングのテストを書いてみてください。
```
  test "should get root" do
    get root_url
    assert_response :success
    assert_select "title", "Home | #{@base_title}"
  end
```

2. 実はリスト 3.41のコードを書いていたので、先ほどの課題のテストは既に green になっているはずです。このような場合、テストを変更する前から成功していたのか、変更した後に成功するようになったのか、判断が難しいです。リスト 3.41のコードがテスト結果に影響を与えていることを確認するため、リスト 3.43のようにrootルーティングをコメントアウトして見て、 red になるかどうか確かめてみましょう (なおRubyのコメント機能については4.2.1で説明します)。最後に、コメントアウトした箇所を元に戻し (すなわちリスト 3.41に戻し)、テストが green になることを確認してみましょう。

* OK, なった!!!
![LGTM](./images/BpVjA7wCMAAfmum.png)


## 4.2.2 文字列
1. city変数に適当な市区町村を、prefecture変数に適当な都道府県を代入してください。
```
?> city = "江東区"
=> "江東区"
>> prefecture = "東京"
=> "東京
```

2. 先ほど作った変数と式展開を使って、「東京都 新宿区」のような住所の文字列を作ってみましょう。出力にはputsを使ってください。
```
?> "#{prefecture} #{city}"                                                                                                     
=> "東京 江東区"
```

3. 上記の文字列の間にある半角スペースをタブに置き換えてみてください。(ヒント: 改行文字と同じで、タブも特殊文字です)
```
>> print "#{prefecture}\t#{city}"
東京    江東区=> nil
```

4. タブに置き換えた文字列を、ダブルクォートからシングルクォートに置き換えてみるとどうなるでしょうか?
```
?> print '#{prefecture}\t#{city}'
#{prefecture}\t#{city}=> nil
```


## 4.2.3 オブジェクトとメッセージ受け渡し
1. "racecar" の文字列の長さはいくつですか? lengthメソッドを使って調べてみてください。
```
>> "racecar".length
=> 7
```

2. reverseメソッドを使って、"racecar"の文字列を逆から読むとどうなるか調べてみてください。
```
>> "racecar".reverse
=> "racecar"
```

3. 変数sに "racecar" を代入してください。その後、比較演算子 (==) を使って変数sとs.reverseの値が同じであるかどうか、調べてみてください。
```
>> puts "true" if s == s.reverse
true
=> nil
```

4. リスト 4.9を実行すると、どんな結果になるでしょうか? 変数sに "onomatopoeia" という文字列を代入するとどうなるでしょうか?
ヒント: 上矢印 (またはCtrl-Pコマンド) を使って以前に使ったコマンドを再利用すると一からコマンドを全部打ち込む必要がなくて便利ですよ。)
```
>> s = "onomatopoeia"
=> "onomatopoeia"
>> puts "It's a palindrome!" if s == s.reverse
=> nil
```


## 4.2.4 メソッドの定義
1. リスト 4.10のFILL_INの部分を適切なコードに置き換え、回文かどうかをチェックするメソッドを定義してみてください。
ヒント: リスト 4.9の比較方法を参考にしてください。
```
def palindrome_tester(s)
   if s == s.reverse
     puts "It's a palindrome!"
   else
     puts "It's not a palindrome."
   end
end
```

2. 上で定義したメソッドを使って “racecar” と “onomatopoeia” が回文かどうかを確かめてみてください。１つ目は回文である、２つ目は回文でない、という結果になれば成功です。
```
>> puts palindrome_tester("racecar")
It's a palindrome!

>> puts palindrome_tester("onomatopoeia")
It's not a palindrome.
```

3. palindrome_tester("racecar")に対してnil?メソッドを呼び出し、戻り値がnilであるかどうかを確認してみてください (つまりnil?を呼び出した結果がtrueであることを確認してください)。
このメソッドチェーンは、nil?メソッドがリスト 4.10の戻り値を受け取り、その結果を返しているという意味になります。
```
?> palindrome_tester("racecar").nil?
It's a palindrome!
=> true
```


## 4.3.1 配列と範囲演算子
1. 文字列 “A man, a plan, a canal, Panama” を ", " で分割して配列にし、変数aに代入してみてください。
```
>> a = "A man, a plan, a canal, Panama".split(',')
=> ["A man", " a plan", " a canal", " Panama"]
```

2. 今度は、変数aの要素を連結した結果 (文字列) を、変数sに代入してみてください。
```
>> s = a.join
=> "A man a plan a canal Panama"
```

3. 変数sを半角スペースで分割した後、もう一度連結して文字列にして��ださい
(ヒント: メソッドチェーンを使うと１行でもできます)。
リスト 4.10で使った回文をチェックするメソッドを使って、
(現状ではまだ) 変数sが回文ではないことを確認してください。
downcaseメソッドを使って、s.downcaseは回文であることを確認してください。
```
?> s.split(',').join
=> "A man a plan a canal Panama"

?> palindrome_tester(s.split(',').join)
It's not a palindrome.
=> nil
```

4. aからzまでの範囲オブジェクトを作成し、7番目の要素を取り出してみてください。
同様にして、後ろから７番目の要素を取り出してみてください。
(ヒント: 範囲オブジェクトを配列に変換するのを忘れないでください)
```
>> ('a'..'z').to_a[6]
=> "g"

>> ('a'..'z').to_a[-7]
=> "t"
```


## 4.3.2 ブロック
1. 範囲オブジェクト0..16を使って、各要素の２乗を出力してください。
```
>> (1..16).map { |i| i**2 }                                                                                                    
=> [1, 4, 9, 16, 25, 36, 49, 64, 81, 100, 121, 144, 169, 196, 225, 256]
```

2. yeller (大声で叫ぶ) というメソッドを定義してください。
このメソッドは、文字列の要素で構成された配列を受け取り、各要素を連結した後、大文字にして結果を返します。
例えばyeller([’o’, ’l’, ’d’])と実行したとき、"OLD"という結果が返ってくれば成功です。
ヒント: mapとupcaseとjoinメソッドを使ってみましょう。
```
def yeller(l = '')
  l.map(&:upcase).join
end

?> yeller(["o", "l", "d"])
=> "OLD"
```

3. random_subdomainというメソッドを定義してください。
このメソッドはランダムな8文字を生成し、文字列として返します。
ヒント: サブドメインを作るときに使ったRubyコードをメソッド化したものです。
```
>> def random_subdomain
>>   ('a'..'z').to_a.shuffle[0..7].join
>> end
=> :random_subdomain
>> 
?> random_subdomain
=> "lzndeosp"
>> random_subdomain
=> "vgxtjahf"
>> random_subdomain
=> "vohygitx"
```

4. リスト 4.12の「?」の部分を、それぞれ適切なメソッドに置き換えてみてください。
ヒント:split、shuffle、joinメソッドを組み合わせると、
メソッドに渡された文字列 (引数) をシャッフルさせることができます。
```
?> def string_shuffle(s)
>>  s.split('').shuffle.join
>> end
=> :string_shuffle
?> string_shuffle("foobar")
=> "orofab"
```

## 4.3.3 ハッシュとシンボル
1. キーが’one’、’two’、’three’となっていて、それぞれの値が’uno’、’dos��、’tres’となっているハッシュを作ってみてください。
その後、ハッシュの各要素をみて、それぞれのキーと値を"’#{key}’のスペイン語は’#{value}’"といった形で出力してみてください。
```
>> num = {}
>> num = { one: "uno", two: "dos", three: "tres" }
>> num.each do |key,value|
?> puts "’#{key}’のスペイン語は’#{value}’"
>> end

’one’のスペイン語は’uno’
’two’のスペイン語は’dos’
’three’のスペイン語は’tres’
=> {:one=>"uno", :two=>"dos", :three=>"tres"}
```

2. person1、person2、person3という３つのハッシュを作成し、それぞれのハッシュに:firstと:lastキーを追加し、
適当な値 (名前など) を入力してください。その後、次のようなparamsというハッシュのハッシュを作ってみてください。
1). キーparams[:father]の値にperson1を代入、
2). キーparams[:mother]の値にperson2を代入、
3). キーparams[:child]の値にperson3を代入。
最後に、ハッシュのハッシュを調べていき、正しい値になっているか確かめてみてください。
(例えばparams[:father][:first]がperson1[:first]と一致しているか確かめてみてください)
```
?> person1 = { first: "masu", last: "suzuki" }                                                                                 
=> {:first=>"masu", :last=>"suzuki"}
>> person2 = { first: "rio", last: "yamakuchi" }                                                                               
=> {:first=>"rio", :last=>"yamakuchi"}

>> params[:father] = person1                                                                                                   
=> {:first=>"masu", :last=>"suzuki"}
>> params[:mother] = person2
=> {:first=>"rio", :last=>"yamakuchi"}

?> params[:father][:first]
=> "masu"

>> params
=> {:father=>{:first=>"masu", :last=>"suzuki"}, :mother=>{:first=>"rio", :last=>"yamakuchi"}}
```

3. userというハッシュを定義してみてください。このハッシュは３つのキー:name、:email、:password_digestを持っていて、
それぞれの値にあなたの名前、あなたのメールアドレス、そして16文字からなるランダムな文字列が代入されています。
```
?> user = { name: "ryamakuchi", email: "r.yamakuchi@gmail.com", password_digest: ('a'..'z').to_a.shuffle[0..15].join }         
=> {:name=>"ryamakuchi", :email=>"r.yamakuchi@gmail.com", :password_digest=>"orkjlfmzhstbgqea"}
```

4. Ruby API (訳注: もしくはるりまサーチ) を使って、Hashクラスのmergeメソッドについて調べてみてください。
次のコードを実行せずに、どのような結果が返ってくるか推測できますか? 
推測できたら、実際にコードを実行して推測があっていたか確認してみましょう。
`{ "a" => 100, "b" => 200 }.merge({ "b" => 300 })`
> selfとotherのハッシュの内容をマージ(統合)した結果を返します。デフォルト値はselfの設定のままです。
> https://docs.ruby-lang.org/ja/search/query:.merge/
{ "a" => 100, "b" => 300 }
>> hash = { "a" => 100, "b" => 200 }.merge({ "b" => 300 })
=> {"a"=>100, "b"=>300}

## 4.4.1 コンストラクタ
1. 1から10の範囲オブジェクトを生成するリテラルコンストラクタは何でしたか? (復習です)
a = (1..10)

2. 今度はRangeクラスとnewメソッドを使って、1から10の範囲オブジェクトを作ってみてください。ヒント: newメソッドに2つの引数を渡す必要があります
b = Range.new(1, 10)

3. 比較演算子==を使って、上記２つの課題で作ったそれぞれのオブジェクトが同じであることを確認してみてください。
```
>> a = (1..10)
=> 1..10
>> b = Range.new(1, 10)
=> 1..10
>> a == b
=> true
```

## 4.4.2 クラス継承
1. Rangeクラスの継承階層を調べてみてください。同様にして、HashとSymbolクラスの継承階層も調べてみてください。
Range > Class > Module > Oblect > BasicObject
Hash > Integer > Numeric > Oblect > BasicObject
Symbol > Class > Module > Oblect > BasicObject

2. リスト 4.15にあるself.reverseのselfを省略し、reverseと書いてもうまく動くことを確認してみてください。
```
?> class Word < String
>> def palindrome?
>> self == reverse
>> end
>> end
=> :palindrome?
>> s = Word.new("level")
=> "level"
>> s.palindrome?  
=> true
```


## 4.4.3 組み込みクラスの変更
1. palindrome?メソッドを使って、“racecar”が回文であり、“onomatopoeia”が回文でないことを確認してみてください。
2. 南インドの言葉「Malayalam」は回文でしょうか? ヒント: downcaseメソッドで小文字にすることを忘れないで。
```
?> s = Word.new("racecar")
=> "racecar"
>> s.palindrome?
=> true
>> s = Word.new("onomatopoeia")
=> "onomatopoeia"
>> s.palindrome?
=> false
>> m = "Malayalam".downcase                                                                                                    
=> "malayalam"
>> s = Word.new(m)
=> "malayalam"
>> s.palindrome?
=> true
```

2. リスト 4.16を参考に、Stringクラスにshuffleメソッドを追加してみてください。ヒント: リスト 4.12も参考になります。
```
?> class String
>> def shuffle
>> self.split('').shuffle.join
>> end
>> end
=> :shuffle
>> "foobar".shuffle
=> "robfao"
```

3. リスト 4.16のコードにおいて、self.を削除してもうまく動くことを確認してください。
```
>> class String
>> def shuffle
>> split('').shuffle.join
>> end
>> end
=> :shuffle
>> "foobar".shuffle
=> "rfooba"
```


## 4.4.4 コントローラクラス
1. 第2章で作ったToyアプリケーションのディレクトリでRailsコンソールを開き、
User.newと実行することでuserオブジェクトが生成できることを確認してみましょう。
```
>> u = User.new
=> #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>
```

2. 生成したuserオブジェクトのクラスの継承階層を調べてみてください。
User > ApplicationRecord(abstract) > ActiveRecord::Base > Object > BasicObject


## 4.4.5 ユーザークラス
1. Userクラスで定義されているname属性を修正して、first_name属性とlast_name属性に分割してみましょう。
また、それらの属性を使って "Michael Hartl" といった文字列を返すfull_nameメソッドを定義してみてください。
最後に、formatted_emailメソッドのnameの部分を、full_nameに置き換えてみましょう (元々の結果と同じになっていれば成功です)
```
>> require './example_user'
=> true
>> user = User.new(first_name: "Michael", last_name: "Hartl", email: "mhartl@example.com")
=> #<User:0x00000003e60610 @first_name="Michael", @last_name="Hartl", @email="mhartl@example.com">
>> user.full_name
=> "Michael Hartl"
>> user.formatted_email
=> "Michael Hartl <mhartl@example.com>"
```

2. "Hartl, Michael" といったフォーマット (苗字と名前がカンマ+半角スペースで区切られている文字列) 
で返すalphabetical_nameメソッドを定義してみましょう。
```
>> user = User.new(first_name: "Michael", last_name: "Hartl", email: "mhartl@example.com")
=> #<User:0x00000004b18150 @first_name="Michael", @last_name="Hartl", @email="mhartl@example.com">
>> user.alphabetical_name
=> "Michael, Hartl"
>> user.formatted_email_al
=> "Michael, Hartl <mhartl@example.com>"
```

3. full_name.splitとalphabetical_name.split(’, ’).reverseの結果を比較し、同じ結果になるかどうか確認してみましょう。
```
>> user.full_name.split
=> ["MichaelHartl"]
>> user.alphabetical_name.split(', ').reverse
=> ["Hartl", "Michael"]
>> user.formatted_email_full
=> "MichaelHartl <mhartl@example.com>"
>> user.formatted_email_al
=> "Michael, Hartl <mhartl@example.com>"
```


## 5章

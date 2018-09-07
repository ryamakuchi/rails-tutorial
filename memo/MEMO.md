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

1. CSSを知っている読者へ: 新しいユーザーを作成し、ブラウザのHTMLインスペクター機能を使って「User was successfully created.」の箇所を調べてみてください。ブラウザをリロードすると、その箇所はどうなるでしょうか?
* 要素の中の文字だけ消える(Rubyの変数が出力されている?)

2. emailを入力せず、名前だけを入力しようとした場合、どうなるでしょうか?「@example.com」のような間違ったメールアドレスを入力して更新しようとした場合、どうなるでしょうか?
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
ApplicationRecordがActiveRecord::Baseを継承しているコードはどこにあるでしょうか? 先ほどの演習を参考に、探してみてください。ヒント: コントローラと本質的には同じ仕組みなので、app/modelsディレクトリ内にあるファイルを調べてみると...?)
# app/models/application_record.rb
class ApplicationRecord < ActiveRecord::Base
  self.abstract_class = true
end
```

## 2.3.5 アプリケーションをデプロイする

1. 本番環境で２〜３人のユーザーを作成してみましょう。
![OK](./images/B3CC33503C0D0F08FA3A849DBE54C007.png)

2. 本番環境で最初のユーザーのマイクロポストを作ってみましょう
![OK](,.images/A915F67BE8B06A57C591565A7F1E85E3.png)

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



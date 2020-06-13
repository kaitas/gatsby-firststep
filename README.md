# Gatsby公式チュートリアルで学ぶ React の基礎

# Gatsbyを使ってみる

GatsbyはReactベースの静的サイトジェネレーターです。
生成される静的サイトはシングルページアプリケーション(SPA)であるため、単なる静的HTMLに比べて優れたUXをユーザーに提供できます。

GithubがGithub Pagesで提供しているJekyllなどもありますが、こちらもこなれてはいますが、だいぶ古い仕組みになってきたので最近の状況を勉強したくなりましたので、とりあえず Gatbsy が何なのか理解したかったので、公式の[Quick-Start](https://www.gatsbyjs.org/docs/quick-start/)からやってみました。

## 準備
1. Visual Studio Code (当方はWindows10環境）
2. npmが使える状態
3. 適当にフォルダを作る
4. 右クリックして「Codeで開く」
5. `Ctrl-@` でコマンドラインを開く

## 公式ドキュメントに従ったQuick-Startの手順

1. インストール ` npm i -g gatsby-cli`
1. 新しいWordpressプロジェクト[gatsby-site]の作成 `gatsby new gatsby-site`
1. `cd gatsby-site` `gatsby develop` ローカルでの確認コマンド
1. `http://localhost:8000` に結果が表示される。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/a087d46c-4f8b-2e44-269d-41a5ef29662c.png)
1. `using-typescript.tsx` についても学んでみる。ちょっと間違えるだけでエラーになるので初心者にはお勧めしないので本稿では次のステップで翻訳を加えておきます。
1. プロダクションビルドを作る。Ctrl-Cでコンソールを一度止めて、 `gatsby build`すると `/public/` 静的サイトが生成される
1. `gatsby serve` すると `http://localhost:9000` でローカルサーバを立ち上げて確認できる。 
2. ねんのため、`/public/index.html` をダブルクリックして開くとこんな感じ
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/a64c919a-3169-d0cb-5a64-cbbe6e5cc071.png)
画像については `data:image/png` でプレビューがエンコードされているようだ。これでファイルリクエスト減らしてキャッシュさせているのね…。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/163e770a-b0cd-f854-833c-87978b775916.png)
レスポンシブ対応もできている。

## TypeScriptのほうは翻訳してみるとこんな感じ
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/6c5bbaad-185b-9b78-68fe-660505e7e45b.png)

一部引用

```tsx:using-typescript.tsx
const UsingTypescript: React.FC<PageProps<DataProps>> = ({ data, path }) => (
  <Layout>
    <SEO title="Using TypeScript" />
    <h1>GatsbyはデフォルトでTypeScriptをサポートしています。</h1>
    <p>これは、ページやコンポーネントなどに<em>.ts/.tsx</em>ファイルを作成して書き込むことができることを意味します。</p>
    <p>Please note that the <em>gatsby-*.js</em> files (like gatsby-node.js) currently don't support TypeScript yet.</p>
    <p>gatsby-*.jsファイル(gatsby-node.jsのようなもの)は現在のところTypeScriptをサポートしていないことに注意してください。</p>
    <p>For type checking you'll want to install <em>typescript</em> via npm and run <em>tsc --init</em> to create a <em>.tsconfig</em> file.</p>
    <p>あなたは現在 "{path}"にいます、{data.site.buildTime}にビルドされました。</p>
    <p>To learn more, head over to our <a href="https://www.gatsbyjs.org/docs/typescript/">documentation about TypeScript</a>.</p>
    <Link to="/">Go back to the homepage</Link>
  </Layout>
)
export default UsingTypescript
export const query = graphql`
  {
    site {
      buildTime(formatString: "YYYY-MM-DD hh:mm a z")
    }
  }
`
```

# Gatsbyでできることを知る

公式ドキュメントの次のステップとしては[プラグイン](https://www.gatsbyjs.org/plugins/)だそうです。
どうかんがえてもドキュメントの海に放り出されるのでお勧めしませんので、個人的な興味でピックアップしておきます。

## Gatsbyプラグインライブラリへようこそ
> SEOは必要ですか？
 そのためのプラグインがあります。

> 検索バーを使って、あなたの爆速サイトをさらに素晴らしいものにしてくれるプラグインを見つけてください。あなた自身のプラグインを作成したい場合は、ドキュメントのプラグインオーサリングページを参照してください! Gatsbyプラグインの詳細については、プラグインのドキュメントページをご覧ください。

実際に興味があるのは Wordpress からのソースプラグイン、それから Google Spredsheet からのソースプラグインあたり。

## Wordpressからデータを取り込んでSPA化する 
`gatsby-source-wordpress` というWordpressをソースにしてGatsbyのSPAにしてしまう。詳細はこちら
[Recipes: Sourcing Data](https://www.gatsbyjs.org/docs/recipes/sourcing-data/#sourcing-from-wordpress)
これはWordpressの[HTTP REST API](https://ja.wp-api.org/)を使ってGraphQLにデータを取り込んでしまう方法。

## Google DocsやSpreadsheetをソースにするプラグイン
https://www.gatsbyjs.org/packages/gatsby-source-google-docs-sheets/
https://github.com/rishabh09/gatsby-source-google-docs

## A/Bテストするレシピ
ボタンの色を変えてNetlifyにデプロイしてGoogle Analyticsでデータ取る…といったシナリオの利用方法の紹介などもある。
https://www.gatsbyjs.org/docs/ab-testing-with-google-analytics-and-netlify/


## サイトショーケース
https://www.gatsbyjs.org/showcase/


## 豊富なスターターライブラリ
https://www.gatsbyjs.org/starters/?v=2

右上に検索窓がありますので「wordpress」や「markdown」など打ってみましょう。

### Wordpres2020
https://www.gatsbyjs.org/starters/henrikwirth/gatsby-starter-wordpress-twenty-twenty/
Wordpressの最新テーマ ``twenty-twenty`` があります。これってつまりWordpressをREST API経由で使うということで、本家を隠蔽しながら移行していくにはちょうどいい気もする。

### greg lobinskiさんのgatsby-starter-personal-blog
[このサイト](https://gatsby-starter-personal-blog.greglobinski.com/)素敵！！
と思いましたので紹介します。

- [gatsby-starter-personal-blog](https://www.gatsbyjs.org/starters/greglobinski/gatsby-starter-personal-blog/)


- カスタマイズできる
- 投稿、ページ、パーツにおいてMarkdownファイルで簡単に編集可能
- テーマオブジェクトを使って簡単にリスタイル
- JSSでスタイリング
- Facebookでコメント
- 投稿カテゴリー
- 投稿リストのフィルタリング
- 全文検索(Algolia)
- お問い合わせフォーム(Netlify form handling)
- Material UI (@next)
- RSS feed
- フルスクリーンモード
- ユーザーが調整可能な記事本文コピーのフォントサイズ
- SNS連携(Twitter, Facebook, Google, LinkedIn)
- PWA（Progressive Web Apps） (manifest.json, offline support, favicons)
- Google Analytics
- Favicons生成 (node script)
- AsyncComponent でのコンポーネントの遅延読み込み (social sharing, info box)
- ESLint (google config)
- Prettier コードスタイリング
- Custom webpack CommonsChunkPlugin settings
- Webpack BundleAnalyzerPlugin

ほんとに盛りだくさんですね！これだけやれればWordpressは止められそう。
（実際にはインストールでエラーが出てしまいましたので、今度また挑戦して紹介します）
このかっこいいサイトを Netilify でデプロイすることもできるようです。

# Gatsbyの基礎知識

## ビルディングブロックについての基礎知識

さて、公式チュートリアルより、つづいて基本を学びます。

- [Get to know Gatsby building blocks](https://www.gatsbyjs.org/tutorial/part-one/)

Gatsbyの新規プロジェクト作成は以下の書式になります
`` gatsby new [SITE_DIRECTORY_NAME] [URL_OF_STARTER_GITHUB_REPO]``

`Hello-World` プロジェクトを使って基礎を勉強しておきましょう。
``gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world``

最後のURLを省略すると、Gatsbyは自動的にデフォルトのスターターに基づいてサイトを生成します。

`cd hello-world` `gatsby develop` を使って Gatsbyのページ構成を学んでいきます。

``http://localhost:8000/``にアクセスすると「Hello world!!」が表示されています。
``src/pages/index.js``を見ていきましょう。これはReactのJSXで書かれています。
ReactのJSXについて詳しくない方のために補足しておきますが、1つの `div`要素とHTML風テキストを含むことができます（HTMLに似ていますが、JSXのコードです）。このようにしてReactのコンポーネントを1つ作成します。

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return <div>Hello world!</div>
}
```

Gatsbyはホットリロードを採用していますので、基本的にGatsby develop サーバーを実行しているとき、Gatsbyサイトのファイルはバックグラウンドで「監視」されています。つまりファイルを保存すると、いつでも、変更はすぐにブラウザに反映されます。ページを更新したり、開発サーバーを再起動したりする必要はありません！

変更した内容をもう少し見やすくするために、``src/pages/index.js`` のコードを以下のコードに置き換えて、もう一度保存してみてください。テキストの色が紫色になり、フォントサイズが大きくなります。

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
}
```

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/31e6e488-86e8-e5eb-af03-aa5159263929.png)

### Gatsbyのページ構成についての基礎知識

（React と JSX に慣れている方は読み飛ばしてください）React フレームワークを使ったことがない人は、JavaScript の関数の中で HTML が何をしているのか疑問に思うかもしれません。なぜ最初の行で react をインポートしているのに、どこにも使っていないように見えるのでしょうか。このハイブリッドな「HTML-in-JS」は、実際にはJSXと呼ばれるReact用のJavaScriptの構文拡張です。React の経験がなくても、このチュートリアルに沿って進むことができますが、興味がある方は、ここで簡単な入門編をご紹介します。



フォントサイズのスタイリングを削除し、"Hello Gatsby!" テキストをレベル 1 のヘッダーに変更し、ヘッダーの下にパラグラフを追加します。

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>なんて世界だ</p>
    </div>
  );
}
```
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/da188eaf-61c9-aef1-c98a-eecd82c8b03f.png)

画像を追加してみましょう。
今回は [Unsplash](https://unsplash.com/) からランダムで画像を持ってきます。

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <h1>Hello Gatsby!</h1>
      <p>Unsplashからのランダム画像</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/084847e8-2d6f-f6f5-c42d-143dc4126554.png)

先ほど使用したこちらの構文ですが、

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return <div>Hello world!</div>
}
```

純粋な JavaScript で表現すると以下のようになります。

```jsx:src/pages/index.js
import React from "react"

export default function Home() {
  return React.createElement("div", null, "Hello world!")
}
```

これで、`import` した 'react' が使われるようになりました。それにしても純粋なHTMLやJavaScriptではなくJSXを書いていますが、閲覧者のブラウザはどうやってそれを解釈するのでしょうか？簡単に言うと、そのような動作ではありません。Gatsbyサイトでは、ソースコードをブラウザが解釈できるものに変換するためのツールがすでにセットアップされています。

### コンポーネントを使用したビルドとは

先ほど編集していたホームページは、「ページコンポーネント」を定義して作成したものです。では「コンポーネント」とは何でしょうか？
広く定義すると、コンポーネントはサイトの構成要素であり、UI（ユーザーインターフェース）の一部を記述する自己完結型のコードです。
GatsbyはReact上に構築されています。コンポーネントの使用と定義について話すとき、実際には「Reactコンポーネント」のことです。

コンポーネントを使ってビルドを始めるようになると、CSS、HTML、JavaScriptが密接に結合され、同じファイル内に存在させることが多いということになります。これは一見単純な変化に見えますが、これはウェブサイトの構築についての考え方に大きな影響を与えます。

カスタムボタンの作成を例に考えてみましょう。以前は、カスタム スタイルを持つ CSS クラス (たとえば .primary-button) を作成し、それらのスタイルを適用させたい対象に ``class`` を使って設定していました。例えば、以下のように…

```<button class="primary-button">Click me</button>```

コンポーネントの世界では、代わりにボタンスタイルを持つ ```PrimaryButton``` コンポーネントを作成し、それをサイト全体で使用します。

```<PrimaryButton>Click me</PrimaryButton>```

コンポーネントは、サイトの基本的な「ビルディングブロック」になります。ブラウザが提供するビルディングブロック、例えば  ``<button />`` などに制限されることなく、プロジェクトのニーズをエレガントに満たす新しいビルディングブロックを簡単に作成することができます。

### ページコンポーネントの使用
``src/pages/*.js`` で定義されているReactコンポーネントは自動的にページになります。これを実際に見てみましょう。
``Hello World`` のスターターに含まれている ``src/pages/index.js`` ファイルを参考に ``about`` ページを作ってみましょう。

``src/pages/about.js`` に新規ファイルを作成し、以下のコードをコピーして保存します。

```jsx:src/pages/about.js
import React from "react"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <h1>About Gatsby</h1>
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

保存したら ``http://localhost:8000/about/`` に行ってみてください。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/d943f92f-f3c5-bc80-7e3e-d22bbdf960c1.png)

``src/pages/about.js`` ファイルにReactコンポーネントを入れるだけで、``/about`` にアクセスできるページができました。


#### サブコンポーネントの使用

このあと、ホームページや `about` ページも色々と書き換えてかなり大きくなってしまったとしましょう。「サブコンポーネント」を使ってUIを再利用可能な部分に分割することができます。両方のページには ``<h1>`` ヘッダがありますので、これを利用してヘッダを記述するコンポーネントを作成します。

``src/components`` に新しいディレクトリを作成し、その中に ``header.js`` というファイルを作成します。
新しい ``src/components/header.js`` ファイルに以下のコードを追加します。

```jsx:src/components/header.js
import React from "react"

export default function Header() {
  return <h1>This is a header.</h1>
}
```

``about.js`` ファイルを修正して、``Header`` コンポーネントを `import` します。``<h1>``要素のマークアップを ``<Header />`` に置き換えます。

```jsx:src/pages/about.js
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/c6042b35-bf44-ca0f-d84e-3bc743646fcb.png)

ブラウザでは "About Gatsby" のヘッダーテキストは "This is a header" に置き換えられるはずです。しかしこれは "About"ページなので 「This is a header」ではなく、「Gatsbyについて」と書き換えてみます。
``src/components/header.js`` に戻って、以下の変更を行います。

```jsx:src/components/header.js
import React from "react"

export default function Header(props) {
  return <h1>{props.headerText}</h1>
}
```
``props`` とは Reactにおける変数のようなものと理解しておいてください。引数として何も引き渡しされていないので、
``src/pages/about.js`` に戻って、以下の変更を行います。

```jsx:src/pages/about.js
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

これで「About Gatsby」のヘッダーテキストが再び表示されるはずです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/1350c9a5-6bc5-98be-8add-50b49e6252b4.png)

#### ``props`` とは何なのか

先ほど、React コンポーネントを UI を記述する再利用可能なコードの一部と定義しました。これらの再利用可能な部分を動的にするためには、異なるデータを提供できる必要があります。これを行うには、「props」と呼ばれる入力を使用します。``props`` (プロップ) はReactコンポーネントに供給される（適切なかつ十分な）プロパティ(``property``)です。

``about.js`` では、``import`` された ``Header`` サブコンポーネントに ``"About Gatsby"`` という値を持つ ``headerText`` プロップを渡しています。

``<Header headerText="About Gatsby" /> ``

``header.js``では、``header`` コンポーネントは ``headerText`` プロップを受け取ることを期待しています(期待するように書いてあるので)。そのため、``header.js`` 内では以下のようにアクセスすることができます。

``<h1>{props.headerText}</h1>``

JSXでは、JavaScriptの式を ```{...}``` でラップすることで、任意の式を埋め込むことができます。このようにして、``props`` オブジェクトから ``headerText`` プロパティにアクセスできます。
例えば ``<Header />`` コンポーネントに別のプロップを渡したいときは、

``<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />``

とすれば ``{props.arbitraryPhrase}`` で ``arbitraryPhrase`` プロップにもアクセスできます。

さて、コンポーネントが再利用可能であることを理解するために、``about`` ページに追加の ``<Header />`` コンポーネントを``src/pages/about.js`` ファイルに追加して保存してみましょう。

```jsx:src/pages/about.js
import React from "react"
import Header from "../components/header"

export default function About() {
  return (
    <div style={{ color: `teal` }}>
      <Header headerText="About Gatsby" />
      <Header headerText="It's pretty cool" />
      <p>Such wow. Very React.</p>
    </div>
  )
}
```

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/5f37e9c2-1f3f-1291-b84e-27b9307e245c.png)

プロップを使用して異なるデータを渡すことで、コードを書き換えることなく、2つ目のヘッダーを作成できました。

#### レイアウトコンポーネントを使う
レイアウトコンポーネントは、複数のページで共有したいサイトのセクションのためのものです。例えば、Gatsbyサイトでは、一般的にヘッダーとフッターを共有するレイアウトコンポーネントがあります。レイアウトに追加する他の一般的なものには、サイドバーやナビゲーションメニューがあります。

レイアウトコンポーネントについては、パート3で説明します。

### ページ間のリンク
ページ間をリンクしたいと思うことはよくあるでしょう。Gatsbyサイトにおけるルーティング(``routing``)を学びましょう。

#### ``<Link />`` コンポーネントを使う

インデックスページのコンポーネント( ``src/pages/index.js`` )を開き、Gatsbyから ``<Link />`` コンポーネントを `import` し、`Header` の上に ``<Link />`` コンポーネントを追加し、パス名に ``"/contact/"`` の値を持つ ``to`` プロパティを与えます。

```jsx:src/pages/index.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Home() {
  return (
    <div style={{ color: `purple` }}>
      <Link to="/contact/">Contact</Link>
      <Header headerText="Hello Gatsby!" />
      <p>What a world.</p>
      <img src="https://source.unsplash.com/random/400x200" alt="" />
    </div>
  )
}
```

「Contact」というお問い合わせフォームっぽいリンクが表示されましたが！

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/84834cee-48a5-8dbc-e3ba-d376018b2d88.png)

しかしリンクをクリックすると…
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/387571b8-196a-8159-c38c-6bccb274c288.png)

...404エラーです。まだ存在しないページにリンクしようとしているからですね。
では ``src/pages/contact.js`` に新しい ``Contact ページ用のページコンポーネント`` を作成して、ホームページにリンクさせましょう。

```jsx:src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default function Contact() {
  return (
    <div style={{ color: `teal` }}>
      <Link to="/">Home</Link>
      <Header headerText="Contact" />
      <p>Send us a message!</p>
    </div>
  )
}
```

ファイルを保存すると、``Contacts`` のページが表示され、ホームページへのリンクをたどることができるはずです。

Gatsbyでの ``<Link />`` コンポーネントは、サイト内のページ間をリンクするためのものです。Gatsbyサイトで処理されないページへの外部リンクには、通常のHTML ``<a>`` タグ を使用してください。

### Gatsby サイトのデプロイ

Gatsbyは最新のサイトジェネレーターであり、サーバーをセットアップしたり、複雑なデータベースをデプロイしたりする必要はありません。その代わりに、``Gatsby build`` コマンドは静的なHTMLとJavaScriptファイルのディレクトリを生成し、静的サイトホスティングサービスにデプロイすることができます。

最初のGatsbyウェブサイトのデプロイに [Surge](https://surge.sh/) を使ってみましょう。Surgeは、Gatsbyサイトをデプロイすることを可能にする多くの「静的サイトホスト」の一つです。

``Gatsby Cloud`` は、Gatsbyの背後にあるチームによって構築されたもう一つのデプロイメントオプションです。次のセクションでは、Gatsby Cloudへのデプロイ方法を説明します。

まだ ``Surge`` をインストールして設定していない場合は、新しいターミナルウィンドウを開き、コマンドラインツールをインストールしてください。

```shell
$ npm install --global surge
$ surge login
```
このコマンドで新規アカウントを作成できます。メールとパスワードを入力してください。

次に、サイトのルートにあるターミナルで以下のコマンドを実行してサイトを構築します。
このコマンドをサイトのルートで実行していることを確認してください。この場合、hello-world フォルダの中です。
Visual Studioのコマンドラインで ``gatsby build``を実行中であれば、``Ctrl-C``で一度停止します。

```shell
$ gatsby build
```

ビルドには15～30秒ほどかかるはずです。ビルドが完了したら、```gatsby build`` コマンドがデプロイの準備をしたファイルを見てみるのも面白いでしょう。
以下のターミナルコマンドをサイトのルートに入力して、``/public`` に生成されたファイルのリストを見てみましょう。

```shell
$ ls public
```

では最後に、生成されたファイルを [surge.sh](https://surge.sh/) という、コマンドラインからサイトをデプロイできるカナダのバンクーバーにある ``Chloi Inc.`` が運営するCDNに公開してサイトをデプロイしましょう。
さきほど新しく作成した Surgeアカウントを有効にするため、サイトを公開する前にメールで確認する必要があります。
``Welcome to Surge!`` というメールが来ているはずですので ``Verify your email`` というリンクを踏んで有効にしてください。

```shell
$ surge public/
```

コマンドラインインターフェースに ``domain: some-name.surge.sh`` という情報が表示されたら、エンターキーを押す必要があることに注意してください。

この実行が終了すると、ターミナルに以下のような表示が出るはずです。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/2f45e721-176f-9e00-d36b-ab052dc32a6b.png)

今回は
[seemly-grandfather.surge.sh](https://seemly-grandfather.surge.sh/)
というサイトにデプロイされました！

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/72103276-0cd6-2982-4b50-e183f1f803bc.png)

さて、これで、あなたのサイトが完成しました。

### 別の選択肢： ``Gatsby Cloud`` へのデプロイ
``Gatsby Cloud`` はGatsbyサイトのために特別に構築されたプラットフォームで、リアルタイムプレビュー、高速ビルド、他の多くのツールとの統合などの機能を備えています。Gatsbyで構築されたサイトを構築してデプロイするには最適な場所であり、個人的なプロジェクトでは無料で ``Gatsby Cloud`` を使用することができます。

サイトを ``Gatsby Cloud`` にデプロイするには、GitHubにアカウントを作成してください。GitHubを使うと、バージョン管理にGitを使ってコードプロジェクトをホストし、共同作業をすることができます。

まずGitHubで新しいリポジトリを作成してきてください。
ここでは ``gatsby-firststep`` というリポジトリを作ってきます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/3dfe013a-b316-15c1-ea58-b1e21a2d6c55.png)


既存のプロジェクトをインポートするので、完全に空のものが必要になるので、READMEや.gitignoreファイルで初期化しないようにしましょう。GitリポジトリのURLをコピーします。

リモート(つまり自分のコンピュータ上ではない)のリポジトリがどこにあるかをGitに伝えるには、次のようにします。

```shell
$ git remote add origin [GITHUB_REPOSITORY_URL]
$ git push -u origin master
```

今回の場合は以下のようになります。

```shell
$ git remote add origin https://github.com/kaitas/gatsby-firststep.git
$ git remote -v
origin  https://github.com/kaitas/gatsby-firststep.git (fetch)
origin  https://github.com/kaitas/gatsby-firststep.git (push)
$ git push -u origin master
```

スターターで新しい Gatsby プロジェクトを作成すると、自動的に最初の git コミット、つまり変更のセットが作成されます。これで、変更内容を新しいリモートリポジトリにプッシュできました。

さてGithubのほうを見てみます
https://github.com/kaitas/gatsby-firststep
READMEも整備されており、[Netlify](https://app.netlify.com/start/deploy?repository=https://github.com/gatsbyjs/gatsby-starter-hello-world)や[Vercel](https://vercel.com/import/project?template=https://github.com/gatsbyjs/gatsby-starter-hello-world)へのデプロイボタンもついています…さすが。

#### Gatsby Cloud へのデプロイ
さてこれで、このGitHubリポジトリをGatsby Cloudに直接リンクする準備が整いました。
ここから先は [Gatsby Cloud へのデプロイに関するリファレンスガイド](https://www.gatsbyjs.org/docs/deploying-to-gatsby-cloud/#set-up-an-existing-gatsby-site) をベースにすすめます。

まず、Gatsby Cloudにアクセスし、GitHubアカウントでサインアップ/サインインしてください。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/8abf2ef0-bcce-d675-52de-a29c19ab3e77.png)

すでにGatsbyサイトを持っていますので、「I already have a Gatsby site」オプションを選択します。

このあと、Githubとの連携に合意します。
GitHub の設定で Gatsby Cloud アプリのインストールを設定します。
リポジトリへのアクセスを全体にするか、個々のリポジトリにするか設定できます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/9419d63b-8bdc-e3a0-652c-2b58290ed64f.png)

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/ee184edc-2221-d756-9dc8-7969f02b86fe.png)

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/89f147f2-405e-ee06-ef8e-962cb7408661.png)



ステップ1 で、オプションのリストから Gatsby サイトを含むリポジトリを選択します。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/9deeef71-accc-e0b0-23c6-4fcdced6078a.png)

サイトの構築とデプロイに使用する ``Production Branch`` と ``Base Directory`` を変更することができます。

（monorepoを設定している場合は、Base DirectoryをGatsbyプロジェクトを含むディレクトリに設定する必要があります。Gatsby Cloud は npm、yarn、yarn workspaces または npm で lerna をサポートしています）

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/1b8b45ee-f198-9bc0-4a28-1a0304cbf610.png)

ステップ2では、Gatsby Cloudプレビューインスタンスにデータを提供するCMSを接続するための自動統合プロバイダを選択することができます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/9f8e5fc0-92c2-c7f7-220e-2d0d2ca92b17.png)

今回は「Skip this Step」→「Create site」とします。

必要な統合を接続したら、[Site Settings]をクリックします。タブ3で、プレビューとビルドに設定したい環境変数を設定できます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/e4bfdf7a-5cfc-0b8d-112b-5e8a7a2c269e.png)

早速ビルドがはじまります。
サイトのダッシュボードページが表示され、「Production」タブの下に、ビルドがトリガーされて進行中であることが表示されます。
ビルドが完了すると、サイトのライブビルドを表示するための URL が表示されます。
「Preview」 タブでは、サイトのプレビュー URL を見つけることができます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/d5fb4e86-de16-800a-cf32-13b53884e690.png)

このプレビュー URL を使用すると、チームは CMS に変更を加えたり、再構築することなくリアルタイムでサイトの更新を自動的に表示することができます。

ビルドに失敗した場合は、[詳細を表示] をクリックして、警告、エラー、およびビルドの生ログを表示することができます。

さて、こちらのサイトですが、``Hello World`` プロジェクトを持ってきた初期の状態になっていますね！

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/a8058dde-2d24-f1ae-fa70-3720065a6388.png)

さっそくこれまでの修正点を``my first commit`` としてコミットして、ライブビルドを見てみましょう！

Visual Studio Codeのソース管理機能（左端の(4)となっているアイコンです）で、コミット名を「my first commit」として、``CHANGES`` の「+」から、今回作成した4つのJSファイルを ``Stage All Changes`` します。


![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/de4c14cf-362e-40cb-9804-12a0f48843b9.png)

続いて、「✓ (Commit)」します。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/cf39c162-fde1-afe1-3e5f-f19782b22581.png)

無事にコミット出来たら「Push」します。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/0c0d2172-09dd-37a1-b3ca-3faf5a3b2658.png)

すぐに ``Gatsby Cloud`` のほうにも検出され、ビルドが始まります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/8e4ccac4-cc73-da63-79b2-c58cbdcc9ae0.png)

無事にプレビューできました！

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/191291/77b5da23-f1f5-7a4b-c692-e1ee7c635152.png)

これでコミット、プッシュ、リポジトリからビルド、テスト、デプロイといった CI（Continuous Integration）、つまり継続的インテグレーションの見通しも立ちましたね。


# 今回はここで終わります！

このドキュメントでは以下のことを学びました。

- Gatsby について
- Gatsby の可用性について
- Gatsby スターターについて
- 新しいプロジェクトを作成する方法について
- JSXの構文
- React コンポーネントについて
- Gatsby のページのコンポーネントとサブコンポーネントについて
- Reactの Propsについて
- React コンポーネントの再利用について
- ``surge.sh`` へのデプロイについて
- ``Gatsby Cloud`` への自動デプロイとCIの入り口

長くなりましたのでこれで終わりますが、公式チュートリアルでは次はパート2「[スタイルを追加する](https://www.gatsbyjs.org/tutorial/part-two/)」が続きます。

# Appendix

- [Qiitaへの投稿](https://qiita.com/o_ob/items/11c787fa267873aab622)
- [このリポジトリ](https://github.com/kaitas/gatsby-firststep)


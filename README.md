# sass-express

##　gulpとexpressの導入方法

1. 適当にフォルダを作成
2. expressをインストール
```
npm install -g express-generator
npm install -g nodemon
express --view=ejs
npm install
```

3. gulpをインストール
```
npm install gulp -g
npm install gulp-sass --save-dev
npm install sass
```

4. gulpfile.jsを追加

ツリー
```
css
├─sass
  └─style.scss
gulpfile.js
```
gulpfile.js
```
// Gulpを初期化する
const { src, dest, watch, series } = require('gulp');

// Gulpプラグインの読み込み
const sass = require('gulp-sass')(require('sass'));

// Sassのコンパイル処理
const sass_compile = function () {
  return src('css/sass/style.scss')
    .pipe(sass({ outputStyle: 'expanded' }))
    .pipe(dest('public/stylesheets'))
}

// タスクを実行する
exports.default = series(sass_compile);

exports.watch = function () {
  watch('css/sass/style.scss', sass_compile);
}
```

5. 実行コマンド
```
//　一度だけコンパイルを実行
gulp 

// style.scssを監視して変更があったらコンパイルを実行
gulp watch

// サーバー起動&expressのソースを監視して変更があったら反映させる
nodemon

// gulpの監視とexpressのソースの監視を同時に行う
gulp watch & nodemon
```


# 声明

> 该项目并非原创，更多内容请访问作者github地址： [ustbhuangyi](https://github.com/ustbhuangyi)

## 项目运行
```bash
npm install
npm run dev
```
## 依赖的第三方库
```bash
  # css 
    stylus stylus-loader
  # ajax
    axios
  # click
    fastclick
  # scroll
    better-scroll
  # lazyload
    vue-lazyload
  # jsonp
    jsonp
  # babel
    babel-runtime
    babel-polyfill
```

## 项目结构
```bash
  [root]
    ├── build
    │     ├── build.js
    │     ├── check-versions.js
    │     ├── dev-client.js
    │     ├── dev-server.js
    │     ├── utils.js
    │     ├── vue-loader.conf.js
    │     ├── webpack.base.conf.js
    │     ├── webpack.dev.conf.js
    │     └── webpack.prod.conf.js
    ├── config
    │     ├── dev.env.js
    │     ├── index.js
    │     └── prod.env.js
    ├── node_modules
    ├── src
    │     ├── api
    │     │   ├── config.js
    │     │   ├── rank.js
    │     │   ├── recommend.js
    │     │   ├── search.js
    │     │   ├── singer.js
    │     │   └── song.js
    │     ├── base
    │     │   ├── confirm
    │     │   │     └── confirm.vue
    │     │   ├── listview
    │     │   │     └── listview.vue
    │     │   ├── loading
    │     │   │     ├── loading.gif
    │     │   │     └── loading.vue
    │     │   ├── no-result
    │     │   │     ├── no-result.vue
    │     │   │     ├── no-result@2x.png
    │     │   │     └── no-result@3x.png
    │     │   ├── progress-bar
    │     │   │     └── progress-bar.vue
    │     │   ├── progress-circle
    │     │   │     └── progress-circle.vue
    │     │   ├── scroll
    │     │   │     └── scroll.vue
    │     │   ├── search-box
    │     │   │     └── search-box.vue
    │     │   ├── search-list
    │     │   │     └── search-list.vue
    │     │   ├── slider
    │     │   │     └── slider.vue
    │     │   ├── song-list
    │     │   │     ├── first@2x.png
    │     │   │     ├── first@3x.png
    │     │   │     ├── second@2x.png
    │     │   │     ├── second@3x.png
    │     │   │     ├── song-list.vue
    │     │   │     ├── third@2x.png
    │     │   │     └── third@3x.png
    │     │   ├── switches
    │     │   │     └── switches.vue
    │     │   └── top-tip
    │     │         └── top-tip.vue
    │     ├── common
    │     │     ├── fonts
    │     │     │     ├── music-icon.eot
    │     │     │   ├── music-icon.svg
    │     │     │   ├── music-icon.ttf
    │     │     │   └── music-icon.woff
    │     │     ├── image
    │     │     │   └── default.png
    │     │     ├── js
    │     │     │   ├── cache.js
    │     │     │   ├── config.js
    │     │     │   ├── dom.js
    │     │     │   ├── jsonp.js
    │     │     │   ├── mixin.js
    │     │     │   ├── singer.js
    │     │     │   ├── song.js
    │     │     │   └── util.js
    │     │     └── stylus
    │     │         ├── base.styl
    │     │         ├── icon.styl
    │     │         ├── index.styl
    │     │         ├── mixin.styl
    │     │         ├── reset.styl
    │     │         └── variable.styl
    │     ├── components
    │     │   ├── add-song
    │     │   │     └── add-song.vue
    │     │   ├── disc
    │     │   │     └── disc.vue
    │     │   ├── m-header
    │     │   │     ├── logo@2x.png
    │     │   │     ├── logo@3x.png
    │     │   │     └── m-header.vue
    │     │   ├── music-list
    │     │   │     └── music-list.vue
    │     │   ├── player
    │     │   │     └── player.vue
    │     │   ├── playlist
    │     │   │     └── playlist.vue
    │     │   ├── rank
    │     │   │     └── rank.vue
    │     │   ├── recommend
    │     │   │     └── recommend.vue
    │     │   ├── search
    │     │   │     └── search.vue
    │     │   ├── singer
    │     │   │     └── singer.vue
    │     │   ├── singer-detail
    │     │   │     └── singer-detail.vue
    │     │   ├── suggest
    │     │   │     └── suggest.vue
    │     │   ├── tab
    │     │   │     └── tab.vue
    │     │   ├── top-list
    │     │   │     └── top-list.vue
    │     │   └── user-center
    │     │         └── user-center.vue
    │     ├── router
    │     │     └── index.js
    │     ├── store
    │     │     ├── actions.js
    │     │     ├── getters.js
    │     │     ├── index.js
    │     │     ├── mutation-types.js
    │     │     ├── mutations.js
    │     │     └── state.js
    │     ├── App.vue
    │     └── main.js
    ├── static
    │     └── .gitkeep
    ├── .babelrc
    ├── .editorconfig
    ├── .eslintignore
    ├── .eslintrc.js
    ├── .gitignore
    ├── .postcssrc.js
    ├── index.html
    ├── package.json
    ├── prod.server.js
    └── README.md
```

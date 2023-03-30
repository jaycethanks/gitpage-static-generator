# gitpage-static-generator

一个根据 Markdown 专门用于生成 demo 项目列表静态页面的 node “脚本程序” 。

[Demo](https://jaycethanks.github.io/)

## 项目目录说明

```bash
# indexPageBuilder
.
├── dist # 文件最终的生成目录
├── src
│   ├── index.ts #入口文件
│   ├── base #模板文件，图标资源目录
│   │   ├── icon.svg #svg 图标，可以是任何支持的 favicon, 网站图标需要在 index.html文件中自己手动引入
│   │   └── index.html #模板 html 文件
│   ├── lib #一些逻辑相关的处理函数
│   ├── templates #模板 markdown
│   │   ├── About.md # 文档头部区域内容
│   │   ├── Footer.md # 文档尾部区域内容
│   │   └── Title.md # 生成文档的头部一级标题
│   └── theme # 样式文件
│       ├── basic.css # 基础的页面样式
│       └── haru.css # Markdown 主题文件
├── .env # 环境变量文件
├── .gitignore
├── .prettierrc
├── package.json
├── pnpm-lock.yaml
└── tsconfig.json
```

要顺利生成，有几个规则一定需要注意, 最终生成的页面，是一个二级标题的列表页面。分别是 **类目名称** - **demo 名称**

在本脚本中， demos/XXXX 将会被解析为 类目名称， 你必须指定一个 `demos/XXXX/index.md` 文件， 这样才能够被正常解析。

其内容应该是一个 等级标题， 例如： "demos/CssTrick/index.md" 的内容可以是：

```bash
#### 一些 CSS DEMO 示例
```

同样的， 你应该指定 `demos/XXXX/xxxx/index.md` , 它们将会被解析为具体的 demo 名称。其文件内容应该是一个纯文本内容,例如: "demos/CssTrick/DuangDuang/index.md" 的文件内容可以是：

```bash
DuangDuang弹弹弹~
```

最后，要保证，你的 demo 页面能够正常访问， 你必须指定一个 dist 目录，例如 "demos/CssTrick/DuangDuang/dist"

该目录中，应该有一个 `index.html` 文件才行。

下面是一个示例的目录结构：

```bash
# demos
.
├── CssTrick
│   ├── index.md
│   ├── DuangDuang
│   │   ├── dist
│   │   └── index.md
│   ├── HappyNewYear2022
│   │   ├── dist
│   │   └── index.md
│   ├── hover-board
│   │   ├── dist
│   │   └── index.md
│   └── theme-clock
│       ├── dist
│       └── index.md
├── DemoPages
│   ├── index.md
│   └── iphone14pro-text
│       ├── dist
│       ├── index.md
│       ├──
│       ├──
│       └──
├── GenerateArts
│   ├── index.md
│   └── plum-effect
│       ├── dist
│       ├── index.md
│       ├──
│       ├──
│       └──
└── READE.md
```

## 环境变量

indexPageBuilder/.env

```bash
GITHUB_URL="https://jaycethanks.github.io"
ENTRY_DIR="demos"
SITE_TITLE="Jayce's Git Page Index"
```

这些环境变量值在页面生成时都会被访问， 他们都是必须的。 这些变量分别是：

- GITHUB_URL : 你的 git page 地址
- ENTRY_DIR= : demos 的入口目录，如果你修改了这个值， 那么要保证根目录 的 demo 目录需要同名
- SITE_TITLE : 最后生成的页面的 title

## 如何使用？

```bash
npm i
npm run exec
```

`npm run exec` 执行之后， 在根目录会生成静态页面

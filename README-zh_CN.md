## 贡献指南

<div>
  <a href="./README.md">🧾English Docs</a>
</div>
<br>

哈喽！我们真的很高兴你有兴趣贡献。这是大多数`LeoStar`项目的通用贡献指南。在提交您的PR之前，请务必花点时间阅读以下指南:

## 👨‍💻 仓库配置

我们在大多数项目中使用[`pnpm`](https://pnpm.io/)，也许有一些使用[`yarn`](https://classic.yarnpkg.com/)，我们强烈建议您安装[`ni`](https://github.com/antfu/ni)，这样您在不同项目之间切换时就不需要担心包管理器了。

我们将在下面的代码片段中使用`ni` 的命令。如果你不使用它，你可以自己做转换:`ni = pnpm install`， `nr = pnpm run`。

设置仓库:

| 步骤 | 命令 |
|-------|--------|
| 1. 安装 [Node.js](https://nodejs.org/), 使用 [最新的LTS版本](https://nodejs.org/en/about/releases/) | - |
| 2. [Enable Corepack](#corepack) | `corepack enable` |
| 3. 安装 [`@antfu/ni`](https://github.com/antfu/ni) | `npm i -g @antfu/ni` |
| 4. 在项目根目录下安装依赖项 | `ni` |

## 💡 常用命令

### `nr dev`

启动开发环境。

如果它是一个Node.js包，它将以监视模式启动构建过程，或者[在使用`unbuild`时存根被动监视器](https://antfu.me/posts/publish-esm-and-cjs#stubbing)。

如果是前端项目，它通常会启动开发服务器。然后，您可以开发并实时查看更改。

### `nr play`

如果它是一个Node.js包，它会为广场启动一个开发服务器。代码通常在`playground/`下面。

### `nr build`

构建用于生产的项目。结果通常在`dist/`下。

### `nr lint`

我们使用[ESLint](https://eslint.org/)进行检测和格式化。如果存在JSON、YAML和Markdown文件，它也会检查。

你可以运行`nr lint --fix`来让ESLint格式化和检测代码。

了解更多关于[ESLint设置](#ESLint)。

[**我们不使用Prettier**](#不使用prettier).

### `nr test`

运行测试我们主要使用[Vitest](https://vitest.dev/) - [Jest](https://jestjs.io/)的替代品。

您可以通过`nr test [match]`过滤要运行的测试，例如，`nr test foo`将只运行包含`foo`的测试文件。

配置选项通常位于`vitest.config`的`test`字段下。`vitest.config.ts` 或者 `vite.config.ts`。

Vitest在[默认的监视模式](https://vitest.dev/guide/features.html#watch-mode)下运行，因此您可以修改代码并自动查看测试结果，这对于[测试驱动的开发](https://en.wikipedia.org/wiki/Test-driven_development)非常有用。要只运行一次测试，可以执行`nr test --run`。

对于某些项目，我们可能会设置多种类型的测试。例如，`nr test:unit`用于单元测试，`nr test:e2e`用于端到端测试。`nr test`通常将它们一起运行，您可以根据需要单独运行它们。

### `nr docs`

如果项目包含文档，您可以运行`nr docs`来启动文档开发服务器。使用`nr docs:build`来构建用于生产的文档。

### `nr commit`

我们使用[`commitlint`](https://commitlint.js.org/)来检查提交消息。它将检查提交消息是否符合我们定义的格式。如果提交消息不符合格式，它将返回一个错误，使用`nr commit`=`git add . && cz-git`。

### `nr`

要了解更多信息，您可以运行`nr`，它将提示所有可用脚本的列表。

## 🙌 提交PR

### 先讨论

在开始处理特性拉取请求之前，最好先打开一个特性请求问题，与维护者讨论该特性是否需要以及这些特性的设计。这将有助于节省维护者和贡献者的时间，并有助于更快地发布特性。

对于错字修复，建议将多个错字修复批处理到一个pull请求中，以维护更干净的提交历史。

### Commit规定

我们使用[Conventional Commits](https://www.conventionalcommits.org/)来处理提交消息，它允许基于提交自动生成变更日志。如果你还不熟悉这个指南，请通读一遍。

只有`fix:`和`feat:`会出现在更新日志中。

注意`fix:`和`feat:`是针对**实际的代码更改**(这可能会影响逻辑)。
对于打字错误或文档更改，请使用`docs:`或`chore:`代替:

- ~~`fix: typo`~~ -> `docs: fix typo`

### PR说明

如果你不知道如何发送Pull Request，我们建议你阅读 [指南](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

发送拉取请求时，确保PR的标题也跟着 [Commit规定](#Commit规定).

如果您的PR修复或解决了现有问题，请在您的PR描述中添加以下一行(将`123`替换为实际问题编号):

```markdown
fix #123
```

这将让GitHub知道问题是链接的，并在PR合并后自动关闭它们。欲知详情，请浏览 [the guide](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword).

在一个PR中有多个提交是可以的，你不需要重新定位或强制推送你的更改，因为我们会在合并时使用`压缩和合并`将提交压缩到一个提交中。

## 🧑‍🔧 维护

本节适用于具有写访问权限的维护者，或者想要维护自己的分支的维护者。

### 更新依赖

使依赖项保持最新是保持项目活力和及时获得最新错误修复的重要方面之一。我们建议每隔一周或两周更新依赖项。
我们使用[`taze`](https://github.com/antfu/taze)来手动更新依赖项。

有时我们也常用[Dependabot](https://github.com/dependabot)或[Renovate](https://renovatebot.com/)这样的深度更新机器人为我们自动更新依赖。

使用 `taze`，您可以运行`taze major -Ir`来检查并选择要交互式更新的版本。`-I`代表' `--interactive`，`-r`代表`--recursive`代表monorepo。

在版本更新之后，我们安装它们，运行build和test以验证在推送到main之前没有任何问题。

### 发布流程

在此之前，请确保您有来自上游的最新git提交和所有CI通过。

大多数时候，我们使用 `nr release`。它将提示您想要发布的目标版本列表。选择后，它会更新你的`package.json`并使用`git tag`提交更改，由[`bumpp`](https://github.com/antfu/bumpp)提供支持.

有两种发布设置，它们中的任何一种都已经通过`nr release`完成了。

<table><tr><td width="500px" valign="top">

#### 本地构建

对于这种类型的设置，构建和发布过程是在本地机器上完成的。在执行此操作之前，请确保您的本地[`npm`登录](http://npm.github.io/installation-setup-docs/installing/logging-in-and-out.html)。

在 `package.json`, 我们经常有:

```json
{
  "scripts": {
    "prepublishOnly": "nr build"
  }
}
```

所以当你运行`npm publish`时，它会确保你在发行版中有最新的更改。

</td><td width="500px" valign="top">

#### 基于CI构建

对于需要长时间构建的复杂项目，我们可能会将构建和发布过程转移到CI。所以它不会阻碍你的本地工作流程。

它们将由`bumpp`添加的`v`前缀的git tag触发。该操作通常定义在`.github/workflows/release.yml`下。

> 当维护你自己的分支时，你可能需要看到' `NPM_TOKEN`添加到你的存储库，以便它发布包。

</td></tr></table>

Changelogs(变更日志)一般由GitHub Actions生成。

## 📖 参考

### Corepack

#### TL;DR

要启用它，请运行命令

```bash
corepack enable
```

您只需要在安装Node.js之后执行一次。

<table><tr><td width="500px" valign="top">

#### 什么是Corepack？

[Corepack](https://nodejs.org/api/corepack.html)确保您在运行相应命令时使用正确的包管理器版本。项目的`package.json`中可能有`packageManager`字段。

项目下的配置如右边所示，corepack将安装`v8.14.0`的`pnpm`(如果你还没有)，并使用它来运行命令。这确保了在这个项目上工作的每个人对依赖项和lockfile都有相同的行为。

</td><td width="500px"><br>

`package.json`

```jsonc
{
  "packageManager": "pnpm@8.14.0"
}
```

</td></tr></table>

### ESLint

我们使用[ESLint](https://eslint.org/)通过[`@antfu/eslint-config`](https://github.com/antfu/eslint-config)进行检测和格式化。

<table><tr><td width="500px" valign="top">

#### IDE设置

我们建议使用[VS Code](https://code.visualstudio.com/)和[ESLint扩展](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)。

通过右边的设置，您可以在保存正在编辑的代码时进行自动修复和格式化。

</td><td width="500px"><br>

VS Code's `settings.json`

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true
  }
}
```

</td></tr></table>

### 不使用Prettier

因为ESLint已经被配置为格式化代码，所以没有必要用Prettier复制这个功能。要格式化代码，你可以运行`nr lint——fix`或参考[ESLint部分](#ESLint)进行IDE设置。

如果您在编辑器中安装了Prettier，我们建议您在处理项目时禁用它，以避免冲突。

## 🗒 其他信息

如果你感兴趣，这里是`LeoStar`的个人配置和设置:

- [ileostar/cmd-alias](https://github.com/ileostar/cmd-alias) - CMD 命令行别名配置
- [ileostar/leostar-spec](https://github.com/ileostar/leostar-spec) - lint 规范
- [ileostar/vscode-settings](https://github.com/antfu/vscode-settings) - VS Code 配置

CLI 工具

- [ni](https://github.com/antfu/ni) - 包管理工具
- [esno](https://github.com/antfu/esno) - TS运行工具
- [taze](https://github.com/antfu/taze) - 依赖更新
- [bumpp](https://github.com/antfu/bumpp) - 版本更新

除了`ni`，这里还有一些更**懒**的cmd别名:

```cmd
doskey s=nr start $*
doskey d=nr dev $*
doskey b=nr build $*
doskey bw=nr build --watch $*
doskey t=nr test $*
doskey tu=nr test -u $*
doskey tw=nr test --watch $*
doskey w=nr watch $*
doskey p=nr play $*
doskey c=nr typecheck $*
doskey lint=nr lint $*
doskey lintf=nr lint --fix $*
doskey release=nr release $*
doskey re=nr release $*
```

Ember 的起步是很容易的。Ember 使用命令行构建工具 Ember CLI 来创建和管理项目。 该构建工具有如下特性：

* 现代化静态资源管理(包括文件合并、压缩，以及版本控制)。
* 帮助创建组件、路由及更多的生成器。
* 常规的项目结构使得既有的 Ember 应用程序也很容易套用。
* 通过 [Babel](http://babeljs.io/docs/learn-es2015/) 项目支持 ES2015／ES6 JavaScript。 这也包含了对于 [Javascript 模块](http://exploringjs.com/es6/ch_modules.html)的支持，本指南将通篇使用这一特性。
* 完整的 [QUnit](https://qunitjs.com/) 测试集成。
* 强健的[Ember Addons](https://emberobserver.com/)插件生态.

## 依赖

### Git

Ember 需要 Git 来管理许多它依赖的东西。 Mac OS X 和大多数 Linux 发行版都自带有 Git. Windows 用户可以下载并运行 [this Git installer](http://git-scm.com/download/win)来安装Git。.

### Node.js 和 npm

Ember CLI is built with JavaScript, and expects the [Node.js](https://nodejs.org/) runtime. It also requires dependencies fetched via [npm](https://www.npmjs.com/). npm is packaged with Node.js, so if your computer has Node.js installed you are ready to go.

Ember requires Node.js 0.12 or higher and npm 2.7 or higher. If you're not sure whether you have Node.js or the right version, run this on your command line:

```bash
node --version
npm --version
```

If you get a *"command not found"* error or an outdated version for Node:

* Windows 或者 Mac 的用户可以下载并运行 [此 Node.js 安装程序](http://nodejs.org/download/).
* Mac 用户通常喜欢使用 [Homebrew](http://brew.sh/) 安装 Node。安装好 Homebrew 后，运行 `brew install node` 来安装 Node.js。
* Linux users can use [this guide for Node.js installation on Linux](https://nodejs.org/en/download/package-manager/).

If you get an outdated version of npm, run `npm install -g npm`.

### Bower

Ember requires Bower to manage additional dependencies. Bower is a command line utility that you install with npm. To install Bower run, ```npm install -g bower```

### Watchman (optional)

On Mac and Linux, you can improve file watching performance by installing [Watchman](https://facebook.github.io/watchman/docs/install.html).

### PhantomJS (optional)

You can run your tests from the command line with PhantomJS, without the need for a browser to be open. Consult the [PhantomJS download instructions](http://phantomjs.org/download.html).

## 安装

Install Ember using npm:

```bash
npm install -g ember-cli
```

To verify that your installation was successful, run:

```bash
ember -v
```

If a version number is shown, you're ready to go.
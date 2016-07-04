# Misskeyの開発環境を整える

Misskeyの開発をするには、開発環境を整えないといけません。
ここでは、Misskeyの開発環境を整える方法を紹介します。
(すでに行っている項目はスキップして構いません)

## Node.jsをインストールする

Node.jsを[ここから](https://nodejs.org/en/download/current/)ダウンロード&インストールします。
Linux上の開発環境を整える場合はディストリビューションで用意されているパッケージを利用してもいいですが、一部ディストリビューションではNode.jsのバージョンが古い場合があります。その場合は手動でインストールするか、[nvm](https://github.com/creationix/nvm)などを利用するのも手です。
何らかの理由でインストール済みのNode.jsをアップグレードせずにMisskeyを使いたい場合も、[nvm](https://github.com/creationix/nvm)などが利用できます。
また、一部Linuxディストリビューション等ではnpm(Node.jsのパッケージマネージャ)が一緒にインストールされないことがあるので、その場合はnpmもインストールしてください。(大体のディストリビューションでは`nodejs-npm`や`npm`などの名前です)

## gitをインストールする

Windowsの場合は、[Git for Windows](https://git-for-windows.github.io/)をダウンロード&インストールします。
Macの場合は、XCodeComamandLinesのgitを使うなり、Homebrewのgitを使うなりしてください。
Linuxの場合は、ディストリビューションのパッケージマネージャなどからインストールしてください。
gitがインストールされているかわからない場合は、ターミナル(OSにより端末、cmdなどと表記が違います)で`git`と打ってみてください。
インストールされていれば、以下の様な表示が出るはずです:
```
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```
例えば`bash: git: command not found`とか`'git' は、内部コマンドまたは外部コマンド、操作可能なプログラムまたはバッチ ファイルとして認識されていません。`とか出る場合は、gitがインストールされていないかPATHが通っていない可能性があります。
PATHの通し方などについてはここでは説明しませんので、Googleで検索するなどして解決してください。

## エディタ/IDEをインストールする(任意)

大体の場合、OSに付属しているエディタ(例:メモ帳)はMisskeyの開発に向いていません。そのため、エディタもしくはIDEをインストールすることを推奨します。
例えば:

- [Visual Studio Code](https://code.visualstudio.com/) 
- [Atom](https://atom.io/) (TypeScriptの補完はプラグインが必要)
- [Sublime Text](https://www.sublimetext.com) (TypeScriptの補完はプラグインが必要)

## MongoDBをインストールする
[ここから](https://www.mongodb.com/download-center)MongoDBをダウンロード&インストールします。パッケージマネージャからインストールしても構いません。

## Redisをインストールする

Windowsの場合はMSOpenTechのRedisを[ここから](https://github.com/MSOpenTech/redis/releases)ダウンロード&インストールしてください。
Linuxの場合はディストリビューションのパッケージマネージャでインストールするか、[ここから](http://redis.io/download)ダウンロード&インストールしてください。

## Misskeyのセットアップ

まず、Misskeyのリポジトリをクローンしましょう。
適当なディレクトリをカレントディレクトリにして
```
git clone https://github.com/Misskernel/Misskey-API api
git clone https://github.com/Misskernel/Misskey-Web web
git clone https://github.com/MissKernel/Misskey-File file
```
としてMisskeyのリポジトリをクローンします。

そして、各リポジトリの中でインストール/ビルドをします。
例えばこんな感じで:
```
cd api
npm install
npm run dts
npm run build
cd ..
cd web
npm install
npm run dtsm
./node_modules/.bin/bower install
npm run build
cd ..
cd file
npm install
npm run dtsm
npm run build
```

# Miniconda 環境構築
参考文献
- https://qiita.com/Ihmon/items/11074e1a4c0e397d934f

- https://inorio.hatenablog.com/entry/2022/10/14/190000
- https://www.hinomaruc.com/build-conda-environment-which-allows-commercial-use/#toc3

- https://endaaman.me/tips/better-conda-env

## 手順
### 1. ダウンロード
https://docs.conda.io/projects/miniconda/en/latest/

### 2. インストール
```
$ cd Downloads
$ bash Miniconda3-latest-Linux-x86_64.sh
```
### 3. Path設定
condaコマンドが使用できない場合はパスを通す。
下記の２行をbashrcに追記、ターミナル再起動する。
（.bashrcはホームディレクトリに存在）

```
$ export PATH=~/miniconda3/bin:$PATH
$ source ~/miniconda3/etc/profile.d/conda.sh
```

condaコマンドが使用できない場合

```
$ conda init bash
$ conda init zsh
```

condaのbase環境の自動起動が不要な場合

```
$ conda config --set auto_activate_base false
```

### 4. デフォルトリポジトリを削除
デフォルトリポジトリは規約により商用不可のため、削除する。

```
$ conda config --show channels
$ conda config --remove channels defaults
$ conda config --add channels conda-forge
$ conda config --set channel_priority strict
$ conda config --show channels
$ sudo cat /home/'user'/.condarc
```

デフォルトリポジトリからインストールされているものをconda-forgeのものに置き換える。  

```
$ conda update conda
```
以上

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

※ 以下はWindows環境で実行した結果

```
(base) C:\Users\rdc_taro>conda config --show channels
channels:
  - defaults

(base) C:\Users\rdc_taro>conda config --remove channels defaults

(base) C:\Users\rdc_taro>conda config --show channels
channels: []

(base) C:\Users\rdc_taro>conda config --add channels conda-forge

(base) C:\Users\rdc_taro>conda config --set channel_priority strict

(base) C:\Users\rdc_taro>conda config --show channels
channels:
  - conda-forge
```

確認
```
(base) C:\Users\rdc_taro>type .condarc
channels:
  - conda-forge
channel_priority: strict

$ sudo cat /home/'user'/.condarc << for Linux
```

デフォルトリポジトリからインストールされているものをconda-forgeのものに置き換える。  

```
(base) C:\Users\rdc_taro>conda update conda
Channels:
 - conda-forge
 - defaults
Platform: win-64
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: C:\Users\rdc_taro\miniconda3

  added / updated specs:
    - conda


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2024.2.2           |     pyhd8ed1ab_0         157 KB  conda-forge
    conda-24.4.0               |  py312h2e8e312_0         1.2 MB  conda-forge
    libexpat-2.5.0             |       h63175ca_1         135 KB  conda-forge
    libsqlite-3.45.3           |       hcfcfb64_0         850 KB  conda-forge
    libzlib-1.2.13             |       hcfcfb64_5          54 KB  conda-forge
    openssl-3.3.0              |       hcfcfb64_0         8.0 MB  conda-forge
    python-3.12.2              |h2628c8c_0_cpython        15.3 MB  conda-forge
    python_abi-3.12            |          4_cp312           7 KB  conda-forge
    tk-8.6.13                  |       h5226925_1         3.3 MB  conda-forge
    ucrt-10.0.22621.0          |       h57928b3_0         1.2 MB  conda-forge
    vc14_runtime-14.38.33130   |      h82b7239_18         732 KB  conda-forge
    vs2015_runtime-14.38.33130 |      hcb4865c_18          17 KB  conda-forge
    zlib-1.2.13                |       hcfcfb64_5         105 KB  conda-forge
    ------------------------------------------------------------
                                           Total:        31.0 MB

The following NEW packages will be INSTALLED:

  libexpat           conda-forge/win-64::libexpat-2.5.0-h63175ca_1
  libsqlite          conda-forge/win-64::libsqlite-3.45.3-hcfcfb64_0
  libzlib            conda-forge/win-64::libzlib-1.2.13-hcfcfb64_5
  python_abi         conda-forge/win-64::python_abi-3.12-4_cp312
  ucrt               conda-forge/win-64::ucrt-10.0.22621.0-h57928b3_0
  vc14_runtime       conda-forge/win-64::vc14_runtime-14.38.33130-h82b7239_18

The following packages will be UPDATED:
done
```

以上
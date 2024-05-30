# miniconda-env
create_miniconda_env.md　を参照のこと

# おまけ：Jupyter Notebook のカーネルに仮想環境をセットする方法
## 手順
1. ローカル環境にJupyter Notebookをインストール(既にある人は不要)
2. 仮想環境に入りipykernelをインストール

## 1.について
```
pip install jupyter notebook
```

## 2.について
```
conda activate xxx
pip install ipykernel
ipython kernel install --user --name=test ※testの部分は自由でOK
```
### 確認
```
jupyter kernelspec list
```

### 削除
```
jupyter kernelspec uninstall [カーネル名]
```

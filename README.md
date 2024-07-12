# miniconda-env

# Jupyter Notebook のカーネルに仮想環境をセットする方法
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

以上

# base 環境自動アクティベートの停止
## 手順
以下を実行
```
conda deactivate
conda config --set auto_activate_base false
```

# 任意のディレクトリで任意の仮想環境を自動アクティベートする方法
※Linux（Ubuntu）想定

## 手順
1. yamlファイル作成と配置
2. .bashrcの編集

## 1
以下を実行
```
cd <自動起動したいディレクトリ>
conda activate <仮想環境名>
conda env export > environment.yaml
```

## 2
以下を.bashrcを開く
```
cd ~
nano .bashrc
```

以下を末尾に追加
```
# add 2024/6/6
# Auto activate conda environments
function conda_auto_env() {
  if [ -e "environment.yaml" ]; then
    #echo "environment.yml file found"
    ENV_NAME=$(head -n 1 environment.yaml | cut -f2 -d ' ')
    # Check if you are already in the environment
    if [[ $CONDA_PREFIX != *$ENV_NAME* ]]; then
      # Try to activate environment
      conda activate $ENV_NAME &>/dev/null
    fi
  fi
}
export PROMPT_COMMAND="conda_auto_env;$PROMPT_COMMAND"
```

編集した内容を反映
```
source ~/.bashrc
```

以上

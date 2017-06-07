# Docker Tips 

Docker使用時に使ったコマンドや詰まった内容を書きこんでいく．

<br>



## How to Docker

### 普通にrunしたいんじゃ

    docker run -it —name home:version (CMD (/bin/bashや/bin/sh))

### attach

    docker exec -it <container_name> /bin/bash
    
### detach
 
コンテナを閉じずにコンテナから出たい．
    
    [control-P][control-Q]
    
### none images の削除

    docker rmi $(docker images | awk '/^<none>/ { print $3 }')
    
### Dockerfileの設定 (imageの作成)

Dockerfile があるdir内で...

    nvidia-docker build -t (tag_name) .

コマンドは`docker`でも良い．`-t`指定は正確には`<image_name>:<tag_name>`

### nvidia-docker でのコンテナRUN例

ローカルディレクトリ，GPUディレクトリをマウントさせるコマンド例．
    
    nvidia-docker run --name <container_name> -v <path_to_local_dir>:<path_to_container_dir> --device /dev/nvidia1:/dev/nvidia1 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm -it nvidia/cuda:cudnn /bin/bash
    
    nvidia-docker run --name <container_name> -v <path_to_local_dir>:<path_to_container_dir> --device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidia1:/dev/nvidia1 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm -it nvidia/cuda:cudnn /bin/bash

    nvidia-docker run --name <container_name> -v <path_to_local_dir>:<path_to_container_dir> --device /dev/nvidia0:/dev/nvidia0 --device /dev/nvidia1:/dev/nvidia1 --device /dev/nvidiactl:/dev/nvidiactl --device /dev/nvidia-uvm:/dev/nvidia-uvm -it <image_name>

imageでインストールしたAnaconda(/root内)の場所にローカルディレクトリをマウントすると上書きされて消えてしまうので別pathにマウントする

<br>
<br>


## コンテナ内にPython環境を設定する

### container 内のAnaconda + chainer install

1. `bash Anaconda3-4.2.0-Linux-x86_64.sh` (Anaconda install .shファイルはマウントで持ってくる) 
2. .bashrc にpathを書き込む (source で適用 `export PATH=“/root/anaconda3/bin:$PATH”`)
3. `pip install chainer` (CUDA_PATHは指定しなくて良い，指定しなければ`/usr/local/cuda`を自動的に探す)

### check CUDA GPU 

pythonでCUDA-GPUが使われているか確認する方法

````python
from chainer import cuda
cuda.check_cuda_available()
cuda.init()
```` 

### seq2seq modelを動かす．

chikai-imgでほぼ揃うが，辞書作成で用いるnltkの`word_tokenize()`関数だけ必要なデータを取ってくる必要がある．

````python
import nltk
nltk.download('punkt')
````

を実行する．


<br>
<br>


## iTorch on docker container

### itorch-notebookを使用する

    docker run --name itorch -it -p 8888:8888 -v /Users/nearstructure/IdeaProjects/tutorials:/root/dev dhunter/itorch-notebook

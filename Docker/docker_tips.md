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
    

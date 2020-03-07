---
title: "atom remote kernel 사용하기(hydrogen)"
excerpt: "local atom에서 server의 jupyter kernel 활용하기"

categories:
  - atom
tags:
  - atom
  - ssh
  - kernel
  - hydrogen
last_modified_at: 2020-03-07
---

# Atom Remote Kernel
local atom 에디터에서 hydrogen 패키지를 활용하여 server의 jupyter kernel을 활용하는 방법을 기술하고자 한다.  

ssh 서버 설치 및 포트포워딩은 완료되어 있는 상태에서 시작  
local: windows 10  
server: ubuntu

## 1. Server 설정

### Config 생성
```bash
jupyter notebook --generate-config
```

### Config 파일 업데이트

```bash
cd ~/.jupyter
vim jupyter_notebook_config.py
```
```
# 모든 ip 허용
c.NotebookApp.ip = '0.0.0.0'
# Notebook의 root dir
c.NotebookApp.notebook_dir = '~/YourDir'

# jupyter 실행시 browsing x
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888
```

## 2. Local 설정
### Kernel Gateways 설정
```
[{
  "name": "Remote test",
  "options": {
    "baseUrl": "http://127.0.0.1:<port>", # <port> 포트포워딩에 맞춰서 설정
    "token": "<server token>" # server notebook의 token, 비밀번호 사용 불가능!!
  }
}]
```
![hydrogen_setting](/assets/images/atom-remote-kernel/hydrogen_setting.png)

### 실행방법

ctrl + shift + p  
Hydrogen: Connect to Remote Kernel 선택  

![](/assets/images/atom-remote-kernel/atom_1.png)  

![](/assets/images/atom-remote-kernel/atom_2.png)  

![](/assets/images/atom-remote-kernel/atom_3.png)  


## 참고사이트
* https://teddylee777.github.io/python/jupyternotebook-remote-%EC%A0%91%EC%86%8D%ED%97%88%EC%9A%A9%ED%95%98%EA%B8%B0

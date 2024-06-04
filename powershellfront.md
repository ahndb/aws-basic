=================================================================  
#### 파워셀 경로이동

#### 노드 확인
- node --version 

#### 노드 설치
- curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

#### 수정후 적용
- source ~/.bashrc

#### 사용가능한 노드버전확인
- nvm list-remote

#### 노드 설치
- nvm install v20.14.0

#### npm 최신버전으로 변경
- npm install -g npm


- npm install -g serve

#### 서버 연결
- serve -s build

============================
### 빌드하고 배포를 관리해줌 
- npm install -g pm2

#### 에코시스템 만듬
- pm2 ecosystem

#### vi ecosystem.config.js
- 들어가서 script, watch 빼고 지우기

#### 추가하기
name:'estate-front',  
script:'serve -s build',  
watch:'build'  

#### 실행
- pm2 start ecosystem.config.js

#### pm2 status
- online뜨면 되는거

#### 모든 프로세스 종료
- pm2 kill 

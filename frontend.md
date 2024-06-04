# 프론트

### snscontainer 하드하게 잡아둔것 바꾸기

### front에 .env 파일 만들기  환경변수 저장용
 - REACT_APP_로 시작해야함

- 파일 만들기  
.env.development  
.env.production  
.env.staging  


#### constant에서 변경할거 2개

- export const SERVER_DOMAIN_URL = process.env.REACT_APP_REST_API_SERVER_DOMAIN;

- export const SNS_SIGN_IN_REQUEST_URL = (type: string) => `${SERVER_AUTH_MODULE_URL}/oauth2/${type}`;
======================================================  

- npm install dotenv
- npm i dotenv-cli

- package.json 에서

  "scripts": {  
    "start": "dotenv -e .env react-scripts start",  
    "test": "react-scripts test",  
    "eject": "react-scripts eject",  
    "build:local": "react-scripts build",  
    "build:development": "react-scripts build",  
    "build:staging": "react-scripts build",  
    "build:production": "react-scripts build"  
  },  


- npm install -g serve 글로벌 영역 지정

- serve -s build 빌드하기

- gitignore
주석처리하기  
build  
추가하기  
.env.development  
.env.staging  
.env.production  
.env   


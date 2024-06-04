#### backend

- local  | 127.0.0.1 | ap.pro
- development | db.estate.dev | ap.dev
- staging | db.estate.stg | ad.stg
- production | db.estate.prg | ad.prg

- 환경변수에 따라 값을 가질 수 있게 여러개 만듬

- application-properties에 spring.datasource.url // 뒤에 데이터베이스 엔드포인지 적기 포트앞까지

- 빌드 -> 코드를 실행가능한 파일로 만듬

- war - 웹배포  // jar - 실행

### application.properties
#### # Front End Host
front.host=http://localhost:3000
development에는 인스턴스 front ip주소를 localhost에 집어넣기

bash
`${ # Front End Host
    front.host=http://localhost:3000}`

### OAuth2SuccessHandler 
  @Value("${front.host}")
  private String FRONT_HOST; 추가하고 응답도 변경
response.sendRedirect(FRONT_HOST + "/sns/" + token + "/36000");

내용 변경후에는 빌드를 다시 해야함


### build.gradle
  나중에 war 지우기   
  version = '1'  // 버전이 길면 이름이 길어져서  
  providedRuntime - > runtimeOnly  
  맨마지막에 추가 // 주석처리했음.  

bash
`${ bootrun  {
    if (project.hasProperty('profile')) {  
      args = "--spring.profilees.active=${profile}"  
    }  
  }  
}`  
주석됨

### gitignore  
*.properties    
#build/ < 실제로는 ignore하고 git에 올려야함  

### 터미널
./gradlew clean build
build에 libs 생김

### 실행
java -jar build/libs/back-1.jar

### 디벨롭실행
java -jar -Dspring.profiles.active=development build/libs/back-1.jar


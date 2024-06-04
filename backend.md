#### backend

- local  | 127.0.0.1 | ap.pro
- development | db.estate.dev | ap.dev
- staging | db.estate.stg | ad.stg
- production | db.estate.prg | ad.prg

- 환경변수에 따라 값을 가질 수 있게 여러개 만듬

- application-properties에 spring.datasource.url // 뒤에 데이터베이스 엔드포인지 적기 포트앞까지

- 빌드 -> 코드를 실행가능한 파일로 만듬

- war - 웹배포  // jar - 실행


- build.gradle
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

#### 터미널
./gradlew clean build
build에 libs 생김

#### 실행
java -jar build/libs/back-1.jar

#### 디벨롭실행
java -jar -Dspring.profiles.active=development build/libs/back-1.jar


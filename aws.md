## AWS 정리
- Region 확인하기 

### 루트 계정 
==============================================================
#### IAM에서 사용자 생성
#### 그룹 생성 (이름설정, 사용자 추가) 
#### 권한 정책 연결(PowerUserAccess, IAMFullAccess)
#### 사용자 클릭 보안자격증명(콘솔엑세스 활성화) 비밀번호 설정
#### 계정설정- 암호정책으로 편집가능
==============================================================

### 사용자 계정
#### VPC 만들기(10.0.0.0/16) 나머지 기본값

#### 서브넷 (FRONT1, BACK1, DB2) 최소 4개 만들기 DB는 2개 이상 필요함.  
- front 서울 2a / 10.0.0.0/20  
- back  서울 2a / 10.0.16.0/20  
- db-01 서울 2a / 10.0.32.0/20  
- db-02 서울 2c / 10.0.48.0/20  

#### 인터넷 게이트웨이 (VPC에 달아주기)
- estate-igw  
- 생성후 vpc연결  

#### 라우팅 테이블 각각의 서브넷에 필요함 인터넷게이트웨이에 달아줌
- estate-rt-public (퍼블릭으로 다 할꺼라 1개만 있으면 됨)  
- 서브넷 연결- 연결 편집  
- 라우팅- 라우팅 편집-라우팅 추가(0.0.0.0/0 -  인터넷게이트웨이)  

#### 보안은 각각 직접 들어가서 함 SG:22포트  
- 프론트는 프론트대로 백은 백대로 데이터베이스는 데이터베이스대로 포트번호 끌어줘야함  
- estate-sg-front / front server security group  
  인바운드 규칙  
  SSH anywhere-IPv4  
  사용자 지정TCP / 3000 / anywhere-IPv4  

- estate-sg-back / back server security group  
  인바운드 규칙  
  SSH anywhere-IPv4  
  사용자 지정TCP / 4000 / anywhere-IPv4  
 
- estate-sg-mysql / mysql security group  
  인바운드 규칙  
  SSH anywhere-IPv4  
  MYSQL/Aurora / anywhere-IPv4  


### EC2
#### 인스턴스 시작
- estate-ec2-front / Ubuntu Server 22.04 LTS (HVM), SSD Volume Type
  키페어 생성(.pem 형식으로)  
  네트워크설정   
  vpc변경   
  front subnet  
  IP자동할당  
  기존보안그룹선택(default, front)  

- estate-ec2-back / Ubuntu Server 22.04 LTS (HVM), SSD Volume Type
  키페어 생성(.pem 형식으로)  
  네트워크설정   
  vpc변경  
  back subnet  
  IP자동할당  
  기존보안그룹선택(default, back)  
==================================================================
### RDS
#### 서브넷 그룹
- estate-mysql-subnet / mysql subnet group / 2a, 2c / 32, 48

#### 파라미터 그룹
- estate-mysql-pg / mysql parameter-group / MYSQL /mysql8.0

#### 옵션 그룹
- estate-mysql-og / mysql option group / mysql / 8.0

#### 데이터베이스
- 표준 생성/ mysql / mysql 8.0.36 / 프리 티어
- 설정 
   DB인스턴스 식별자 estate-mysql  
  자체관리 / 마스터 암호   
- 연결
  EC2 컴퓨팅 리소스에 연결 안 함 / IPv4 / vpc 확인 / 퍼블릭 엑세스-예 /  
  VPC 보안 그룹(방화벽) - 기존항목에서 default, mysql 추가하기 /  
  가용 영역 - 2a / 추가구성 포트번호 확인  
- 태그추가 
  estate-mysql  
- 추가구성 
  DB 파라미터 그룹 / 옵션 그룹  
  백업 체크해제  / 암호화활성화 체크해제 / 마이너 버전 자동 업그레이드 사용 체크해제 /  

#### VPC 설정편집  
- DNS 호스트 이름 활성화 체크 하고 저장해야지 데이터베이스 생성가능  
===========================================================  

####  워크벤치 
- 커넥션 생성
- 호스트네임에 데이터베이스 엔드포인트 넣기
- 유저네임에 admin
- 비밀번호 입력하기
- send to sql editer -create

==========================================================

#### 인스턴스 연결 -> 유저 이름 알수 있음
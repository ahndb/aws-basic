### 파워셀
- git clone
- clone된 폴더로 넘어가서
- sudo apt update
- sudo apt install openjdk-17-jdk

환경변수 
echo $JAVA_HOME

cd /usr/lib
cd /jvm
cd ~

# 환경변수등록
sudo vi /etc/environment
i - insert 모드
JAVA_HOME="usr/lib/jvm/java-17-openjdk-amd64"
source /ect/environment
echo $JAVA_HOME

cd estate-back-end/
java -jar build/libs/back-1.jar
java -jar -Dspring.profiles.active=development build/libs/back-1.jar

터미널을 끄면 서버가 종료가 됨



백그라운드에서 돌아가게 해줘야함.

==============================================
cd estate-back

# 프로세서번호보기
nohup java -jar -Dspring.profiles.active=development build/libs/back-1.jar &

tail -f nohup.out
# insurance

## 데이터베이스 설치 및 설정(MariaDB & Oracle)
### Maria DB
1. MariaDB 설치
mariadb.org에서 다운로드 후 설치
설치 시 root 비밀번호 1234--> python 프로젝트 setting.py 파일에서 사용
MySQL client에서 root로 로그인 하고
use mysql
grant all on *.* to 'root'@'localhost' identified by '1234';
grant all on *.* to 'root'@'%' identified by '1234';
flush privileges;
2. 로그인 후 데이터베이스 생성
create database insurance;
exit;
3. Maria DB 에 DataBase 폴더에 있는 MariaDB sql 파일 import 하기
ex) mysql -u username -p new_database < data-dump.sql
mysql -u root -p insurance < D:\m\DataBase\MariaDB.sql

### ORACLE DB
1. Oracle Express Edition 설치(oracle.com)
hr 계정 초기화
conn /as sysdba
exec dbms_xdb.sethttpport(8001)
alter user hr account unlock identified by hr;
conn hr/hr
select count(*) from employees;
2. SQL Developer 설치 및 설정(oracle.com)
3. 기존 테이블 및 시퀀스 삭제
drop table cust_manager;
drop table member;
drop table board_upload_file;
drop table board;
drop table board_category;
drop sequence seq_member;
4. ORACLE DB 에 DataBase 폴더에 있는 ORACLE-2.sql 파일 import 하기 (안되면) ORACLE sql 파일로
@D:\m\DataBase\Oracle-2.sql


## WAS 설정(파이썬 장고 & 자바 스프링)
### 장고
1. 파이썬 설치(python.org)
3.7.7권장(3.8은 설치전 윈도우7 Windows Update를 실행 해야 함)
* 3.7.7 설치하세요.
설치폴더 : C:\Python37
2. 패키지 설치(터미널 창에 pip install -r requirements.txt)
python -m pip install --upgrade pip
python -m pip install -r C:\requirements.txt
3. 파이참 설치(https://www.jetbrains.com/pycharm/)
community edition 설치
4. 프로젝트 열기
insuranceFDS.zip 파일 압축 풀고 프로젝트 열기
5. File > Settings > Project Interpreter 에서 파이썬 인터프린터 추가
DJango, imbalanced-learn, PyMySQL, scikit-learn, numpy, pandas, xgboost, 
6. RUN > Edit Configurations... 
Parameters에 runserver 입력 후 run
또는 터미널에서 python manage.py runserver
7. 테스트(웰컴페이지 없음)
http://127.0.0.1:8000/1

### 스프링
1. JDK설치(1.8)
2. 이클립스 설치(eclipse.org)
3. Perspective변경 -> git으로
4. 프로젝트 가져오기
이클립스에서 File > Import > General > Existing project into workspace
Select archive file : Insurance-Fraud-Detection.zip > Finish
5. 톰캣 설치
6. 이클립스에서 톰캣 서버 설정
7. C:\Users\B0111\.m2\repository\com\oracle\ojdbc\6 폴더에 Database폴더 안에 있는 ojdbc-6.jar 파일을 복사해서 붙여넣기
데이터베이스 계정 정보
 -프로젝트 > Java Resources > src/main/resources/database/jdbc.properties
jdbc.driverClassName=oracle.jdbc.driver.OracleDriver
jdbc.url=jdbc:oracle:thin:@localhost:1521:xe
jdbc.username=hr
jdbc.password=hr

majdbc.driverClassName=org.mariadb.jdbc.Driver
majdbc.url=jdbc:mariadb://127.0.0.1:3306/insurance_data
majdbc.username=root
majdbc.password=1234
8. 서버실행
브라우저 주소는 http://localhost:8080/ins/member/login


보험 판별 프로젝트 실행 순서
장고 서버를 먼저 킨다.
스프링 서버를 킨다.
스프링 서버에서 돌아가는 호스트 URL 로 접속한다.
service 에 들어가 잘되나 확인한다.
관리자 임시 아이디/비밀번호 : admin/admin


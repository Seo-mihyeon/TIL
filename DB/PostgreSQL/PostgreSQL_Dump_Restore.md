Linux에서 Postgresql DB 덤프 및 복원 방법

DUMP
1) psql 접근 권한이 있는 계정으로 접속한다.
2) psql 이 있는 폴더로 접근한다.
 cd /usr/psql-11/bin
3) dump 하고자 하는 DB에 설정값을 입력해서 받는다
옵션사항 : 
  -d, 덤프할 DBNAME 데이터베이스
  -h, 호스트 이름 데이터베이스 서버 호스트 또는 소켓 디렉터리
  -p, PORT 데이터베이스 서버 포트 번호
  -U, 지정된 데이터베이스 사용자로 NAME 연결
  -w, --no-password 비밀번호 확인 안 함
  -W, --password 비밀번호 강제 적용 프롬프트(자동으로 발생해야 함)
4 ) 특정 테이블 DUMP 뜨기
pg_dump -d [DB 이름] -h [DB IP주소] -p [DB 포트] -U [사용자명] -t[받고자하는 테이블 명] > [경로/파일명.확장자]
 -t 덤프 받고자 하는 테이블 
 -T 덤프 제외 테이블
 * DB 전체 DUMP시 -t 사용 안하고 DB명만 적으면 됨
Restore
1) 특정 테이블만 복원
psql -h[DB IP주소] -p [DB 포트] -U [사용자명] -f 백업.sql [DB명]
2) 전체 복원
psql [DB명] < 백업.sql

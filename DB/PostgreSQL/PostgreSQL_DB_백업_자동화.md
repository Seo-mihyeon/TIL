#### ***1. linux 환경에서 자동화 설정을 하기 위해서는 crontab 설정에대해 알아야한다.***
  ``` 
  #크론탭 편집
  crontab -e
  
  #크론탭 작업 내용 확인
  crontab -l
  ```

    - crontab 설정방법
  ```
  #Example of job definition:
  #.---------------- minute (0 - 59)
  #|   .------------- hour (0 - 23)
  #|   |   .---------- day of month (1 - 31)
  #|   |   |  .------- month (1 - 12) OR jan,feb,mar,apr ...
  #|   |   |  |   .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
  #|   |   |  |   |
  #*   *   *  *   *   user-name command to be executed
  #분  시  일 월  요일 명령어 또는 스크립트
  
  분 (minute)	0-59, * 설정 시 1분 단위로 실행
  시 (hour)	0-23, * 설정 시 매시간 실행
  일 (day of month)	1-31, * 설정 시 매일 실행
  월 (month)	1-12, * 설정 시 매달 실행 
  요일 (day of week)	0-7, * 설정 시 월요일부터 일요일까지 매일 실행
  명령어 또는 스크립트 (command)	실행할 명령어 또는 프로그램 등 설정

  ```
   예시)
   ```
   * 2 25 * * /db/dump.sh
   매일 25일 02시에 dump.sh 실행
   ```
   crontab 설정 이후에는 재시작 처리 해줘야한다.
   ```
   # crontab 재시작
   service crond restart
   # crontab 상태 확인
   service crond 
   ```
   
####   *2. 백업 스크립트 작성하기*
  
  	- 디렉토리 생성하기
      ` mkdir /home/db`
    - 스크립트 생성하기
       `vim /home/db/dump.sh`
    - 스크립트 작성하기
    ```
   #!/bin/bash
  FILENAME=$(backUpDB +"%Y-%m-%d_%H%M").dump
  cd $BACKUP_DIR
  PGPASSWORD="비밀번호" pg_dump -h "ip주소" -U "사용자명" "DB명" -Fc -v > "${BACKUP_DIR}/DBNAME_${FILENAME}"
  echo "Delete old file DBNAME_${DEL_FILE}"
  echo "BACKUP - End time : " $(date +"%Y-%m-%d %H:%M:%S")
    ```
    
     - FILENAME : dump.sh 실행시 결과물로 만들어질 파일명
    - BACKUP_DIR : FILENAME 과 같이 변수로 설정하거나 혹은 고정된 디렉토리 값을 입력해도 무관하다.
    - 추가적으로, dump.sh 실행과 동시에 일정 시간이 지난 오래된 dump의 결과물을 삭제하고자 한다면
    
    ```
    DEL_FILE=$(backUpDB -d '60 day ago' +'%Y-%m-%d_')"*.dump"
    rm "${BACKUP_DIR}/DBNAME_${DEL_FILE}" 
    ```
   을 추가적으로 작성해주면 된다.  '60 day ago' 부분의 숫자의 값만 변경하면 된다.    
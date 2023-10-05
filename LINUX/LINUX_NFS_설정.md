**리눅스 NFS 설치 작업**

## NFS 서버 설정 ( 서버IP )
1. 패키지 설치
: yum install nfs-utils
: rpm -qa nfs-utils

2. NFS 가동 및 재부팅 시 자동 활성화 설정

: systemctl start nfs-server
: systemctl enable nfs-server

3. 폴더 설정

: vim /etc/exports

/home/sonic/SN/upload 클라이언트IP(ro)
/home/sonic/SN/upload 클라이언트IP(ro)

[ 공유할 디렉터리 ] [허가할 호스트][디렉터리 권한]

|권한|설명|
| :- | :- |
|rw|읽기, 쓰기 가능 (read, write)|
|ro|읽기만 가능 (read only)|
|secure|포트번호 1024 이하의 요청만 허가|
|root\_squash|클라이언트의 root권한 무시|
|no\_root\_squash|클라이언트의 root권한 인정|
|all\_squash|모든 권한 무시하고 nobody 권한 부여|

4. 수정된 내용 반영

: exportfs-r

5. 방화벽 실행 시 nfs 서비스 허가 방화벽에 따로 설정해주기

: firewall-cmd-permanent-add-servic=nfs
: firewall-cmd-reload
: firewall-cmd-list-all

6. 확인

: showmount -e
: exportfs -v

## NFS 클라이언트 설정 ( 클라이언트IP )
1. 패키지 설치

: yum -y install nfs-utils

2. NFS 서버 공유 디렉터리 확인

: showmount -e [서버\_IP]
: showmount -e 서버IP

3. 마운트 작업

: mount -t nfs 서버IP:/home/sonic/SN/upload /home/sonic/SN/upload

4. 재부팅시 자동 활성화

: vim /etc/fstab
: 서버IP:/home/sonic/SN/upload /home/sonic/SN/upload nfs defaults 0 0

5. 마운트 확인
: df

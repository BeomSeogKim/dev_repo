### 명령어 
- 실행중인 컨테이너를 모두 삭제하는 방법
	- docker rm -f $(docker ps -aq)
- 메뉴얼 확인
	- docker --help
- 컨테이너 실행
	- docker run (실행 옵션) 이미지명
- 컨테이너 삭제
	- docker rm 컨테이머명 / ID
- 로컬 이미지 조회 
	- docker image ls (이미지명)
- 실행중인 컨테이너 리스트 조회 
	- docker ps 
- 실행중인 컨테이너 삭제
	- docker rm - f
- 이미지의 세부 정보 조회 
	- docker image inspect 이미지명
- 컨테이너의 세부 정보 조회
	- docker container insepct 컨테이너명
- 컨테이너 실행 시 메타데이터의 cmd 덮어쓰기
	- docker run 이미지명 (실행명령)
- 컨테이너 실행 시 메타데이터의 env 덮어쓰기
	- docker run --env KEY=VALUE 이미지명
- 컨테이너의 로그 조회 
	- docker log (컨테이너명)
- 컨테이너 로그를 터미널로 연결 (실시간 로그 확인)
	- docker logs -f (컨테이너명)
- 로컬 스토리지로 이미지 다운로드 
	- docker pull 이미지명
- 로컬 스토리지의 이미지명 추가
	- docker tag 기존이미지명 추가할 이미지명
- 이미지 레지스트리에 이미지 업로드
	- docker push 이미지명
- 이미지 레지스트리 인증 정보 생성
	- docker login
- 이미지 레지스트리 인증 정보 삭제
	- docker logout
- 로컬 스토리지에서의 이미지 삭제
	- docker image rm 이미지명
- 이미지의 레이어 이력 조회
	- docker image history 이미지명
- 컨테이너 실행과 동시에 터미널 접속
	- docker run -t --name 컨테이너명 이미지명 bin/bash
- 실행중인 컨테이너를 이미지로 생성
	- docker commit -m 커밋명 실행중인컨테이너명 생성할 이미지명
-  도커파일을 통해 이미지 빌드
	- docker build -t 이미지명 Dockerfile경로
- 도커파일명이 Dockerfile이 아닌 경우 별도 지정
	- docker build -f 도커파일명 -t 이미지명 Dockerfile 경로
- 컨테이너와 호스트 머신 간 파일 복사 
	- docker cp 원본위치 복사위치
- 컨테이너 -> 호스트머신으로 파일 복사
	- docker cp 컨테이너명:원본위치 복사위치 
- 호스트머신-> 컨테이너로 파일 복사
	- docker cp 원본위치 컨테이너명:복사위치
- 도커 볼륨 마운트
	- docker run -v {도커의볼륨명}://{컨테이너의 내부 경로}
- 도커 볼륨 리스트 조회
	- docker volume ls
- 볼륨상세 정보 조회
	- docker volume inspect 볼륨명
- 볼륨 생성
	- docker volume create 볼륨명
- 볼륨 삭제
	- docker volume rm 볼륨명

보통 도커 명령어는 다음을 따른다. 
(Management Command의 경우 종종 생략 가능하다.)
```shell
docker (Management Command) Command
```

```shell
docker run -d --name {컨테이너명} 이미지명
```
- -d : 백그라운드 실행
- 컨테이너명은 로컬에서 중복 될 수 없음

### docker container lifecycle
![[Pasted image 20250301130001.png]]

### Image 명명 규칙
![[Pasted image 20250301133501.png]]

### 기본 Dockerfile 지시어
![[Pasted image 20250304093501.png]]
![[Pasted image 20250304213052.png]]
![[Pasted image 20250304213909.png]]![[Pasted image 20250304214518.png]]

#### 도커 볼륨
![[Pasted image 20250310205948.png]]

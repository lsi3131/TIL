## 강의 영상

[7-1. Docker 컨테이너 리소스를 관리해야지 - 이론편](https://www.youtube.com/watch?v=7HA_00KNtbc&list=PLApuRlvrZKogb78kKq1wRvrjg1VMwYrvi&index=17)

[7-2. Docker 컨테이너 리소스를 관리해야지 - 실습편](https://www.youtube.com/watch?v=TM3DvwwvsLg&list=PLApuRlvrZKogb78kKq1wRvrjg1VMwYrvi&index=18)

## 학습 내용

컨테이너 리소스 제한
컨테이너 모니터링
cAdvisor 설치 및 사용


## 컨테이너 리소스 제한
### 부하 테스트 
리눅스 stress 툴을 사용하여 부하테스트를 진행한다.
사용법은 다음과 같다.

__CPU 부하 테스트__

```
$ stress --cpu 2
```

2개 cpu core를 100% 사용하도록 부하 발생

___메모리 부하 테ㅅ트__
```
$ stress --vm 2 --vm-bytes <사용할 크기>
```

프로세스 수 2개와 사용할 메모리만큼 부하 발생

다음 내용으로 dockerfile을 작성 후 해당 docker image로 부하테스트를 실행한다.
```
FROM debian
MAINTAINER silee <lsi9393@naver.com>
RUN apt-get update; apt-get install stress -y
CMD ["/bin/sh", "-c", "stress -c 2"]
```

다음 명령어로 빌드를 진행한다,
```
$ docker build -t stress . 
```

다음과 같이 문자가 출력된다.
```
silee@docker-ubuntu:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
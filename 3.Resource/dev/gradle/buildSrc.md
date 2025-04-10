buildSrc는 자동으로 인식되고 자동으로 빌드 됨
- buildSrc/ 디렉토리가 root project에 있으면, Gradle이 디렉토리를 자동으로 별도의 프로젝트처럼 다룸.
- Gradle이 빌드를 시작할 때, buildSrc를 먼저 컴파일 하고, 컴파일 결과를 빌드 스크립트의 classpath에 추가
- => buildSrc에 작성한 클래스나 플러그인, 유틸리티 함수 등을 별다른 설정 없이 바로 빌드 스크립트에서 사용이 가능함 


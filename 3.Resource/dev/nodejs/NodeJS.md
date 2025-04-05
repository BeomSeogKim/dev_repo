- JavaScript 실행 환경 ( == 구동기 )
- 초기 : 웹 페이지 내부에 필요한 단순한 기능을 개발하기 위해 만들어짐 -> 수요가 많아짐
- 웹 서버, 모바일 앱, 데스크톱 앱 등등에 사용되기 시작

### 설치 
- https://nodejs.org/en
- 설치 확인 `node -v`

### NPM (Node Package Manager)
- node.js 의 프로젝트 단위인 패키지를 관리하는 Tool
- 패키지 설치 / 삭제, 라이브러리 관리 등등에 사용됨
- 설치 확인 `npm -v`
- npm init : 새로운 패키지를 생성하기위한 command
![[npm.png]]
```
{
...
"scripts": {

	"test": "echo \"Error: no test specified\" && exit 1",

	"start": "node src/index.js"

},

"author": "",

"license": "ISC",

"description": ""

}
```
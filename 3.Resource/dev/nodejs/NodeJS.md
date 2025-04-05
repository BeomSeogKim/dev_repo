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
- scripts : 일종의 단축키 역할을 함
- npm run {script 에 명시된 단축어}
```
{
...
"scripts": {
	"test": "echo \"Error: no test specified\" && exit 1",
	"start": "node src/index.js"
},
}
```

### Node.js Module System
- 모듈을 다루는 시스템 (생성, 불러오기, 사용 ...)
- JavaScript Module System
	- Common JS (CJS)
	- ES Module (ESM)

#### Common JS
- module.exports로 내보낼 함수들을 지정한다
- key : vale 형식으로 지정을 하나. key와 value가 같다면 key 만 사용 
```
function add(a, b) {return a + b;}
function sub(a, b) {return a - b;}
// CJS => module.exports 로 내보낼 function들을 지정 
module.exports = {add,sub};

--- 사용하는 곳 
const { add, sub } = require("");
```

#### ES Module
- package.json에 "type": "module" 명시
- *확장자까지 명시를 해 주어야 한다.*
- export { } 방식으로 내보낼 수 있음 (여러개 동시에 내보냄)
- export function ... 방식으로 내보낼 수 있음
- export default function -> 대표 function 내보낼 때 사용 
```
function add(a, b) {return a + b;}
function sub(a, b) {return a - b;}

// ES 
export { add, sub };

--- 
사용하는 곳 
import { add, sub } from ""
```
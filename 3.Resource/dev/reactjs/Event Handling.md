- 웹 내부에서 발생하는 사용자의 행동이 일어났을 때 처리하는 것
	- 버튼 클릭, 메세지 입력, 스크롤 등등 ...

```
const Button = ({ children, text, color = "black" }) => {
return (
<button

onClick={() => {

console.log(text);

}}

style={{ color: color }}

>

{text} - {color.toUpperCase()}

{children}

</button>

);

};
```
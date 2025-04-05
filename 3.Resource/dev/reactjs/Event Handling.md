- 웹 내부에서 발생하는 사용자의 행동이 일어났을 때 처리하는 것
	- 버튼 클릭, 메세지 입력, 스크롤 등등 ...

```
const Button = ({ children, text, color = "black" }) => {
	return (
		<button
			// Event handler
			onClick={() => {
				console.log(text);
			}}
			style={{ color: color }}
        >	
</button>

);

};
```

### SyntheticBaseEvent (합성 이벤트)
- 모든 웹 브라우저의 이벤트 객체를 하나로 통일한 형태
- CrossBrowsingIssue를 해결 할 수 있음
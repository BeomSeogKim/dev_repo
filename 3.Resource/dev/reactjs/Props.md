- 컴포넌트에 값을 전달 
- text, img에 값을 지정해 줄 수 있는 방식이다.
- Component를 값에 따라서 다른 UI를 렌더링 하도록 만들 수 있음
- 함수의 변수를 받는 곳에 받고자 하는 값을 넣어주면 됨
```
function App() {

	return (
		<>
			<Button text={} color={}/>
			<Button text={} color={}/>
			<Button>
				<h1> child div </h1>
			</Button>
		</>
	)

}

--- 
function Button = ({ children, text, color }) => {
	return (
		<button style = {{color:color}}> 
			{text} - {color}
		</button>
	)
}
```
> 현재 가지고 있는 형태나 모양을 정의
> 변화할 수 있는 동적인 값

- State의 값에 따라 렌더링 되는 UI를 결정할 수 있음

#### useState
**단일 상태 관리**
```
const Button = () => {

	const [input, setInput] = useState("");

	const onChangeInput = (e) => {
		setInput(e.target.value);
	}

	return (
	<div>
		<input 
		value = {input}
		onChange={onChangeInput}
		placeHolder={"default value"}
		/>
	</div>
	)
}
```

**복수 상태 관리**
```
const Button = () => {

	// { } 타입으로 상태를 관리하고자 하는 값들을 정의
	const [input, setInput] = useState({
		name: "",
		...
	});

	const onChangeInput = (e) => {
		setInput({
			...input,
			// 상태를 관리하고자 하는 값의 Key
			[e.target.name]: e.target.value
		});
	}

	return (
	<div>
		<input 
		name="name"  // 추가
		value = {input.name}
		onChange={onChangeInput}
		placeHolder={"default value"}
		/>
	</div>
	)
}
```
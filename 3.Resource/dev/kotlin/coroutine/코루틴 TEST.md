### 코루틴 테스트 라이브러리

#### TestCoroutineScheduler
- 가상 시간에서 테스트를 진행할 수 있도록 하는 기능을 제공한다.
- advanceTimeBy로 가상의 시간을 조절 할 수 있음
- currentTime 프로퍼티를 사용해 테스트 환경의 현재 시간(가상 시간)을 알 수 있음

```
@Test
fun `test-1`() {
val testCoroutineScheduler = TestCoroutineScheduler()

testCoroutineScheduler.advanceTimeBy(4000L)
assertEquals(5000L, testCoroutineScheduler.currentTime)
}
```

#### StandardTestDispatcher
- dispatcher를 생성한뒤 해당 CoroutineDispatcher를 조절하는 방식
- advanceUntilIdle을 사용할 경우 가상 시간 스케쥴러를 사용하는 모든 코루틴이 완료될 때 까지 시간이 흐름
```
val testCoroutineScheduler = TestCoroutineScheduler()
val testDispatcher = StandardTestDispatcher(scheduler = testCoroutineScheduler)
val testCoroutineScope = CoroutineScope(context = testDispatcher)

testCoroutineScope.launch {
  // ... 
}

testCoroutineScheduler.advanceTimeBy(5000L)
```

#### runTest 
- runTest 함수로 생성된 코루틴 내부에서 실행된 코루틴의 시간만 흐름
- 만약 TestScope을 사용하여 새로운 코루틴이 실행된다면, 해당 코루틴은 시간이 자동으로 흐르지 않음
- 따라서 advanceUntilIdle을 명시적으로 호출
```
@Test
fun `test-2`() = runTest{
	// ... 
}
```
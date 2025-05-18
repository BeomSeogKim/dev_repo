- Web Server에 HTTP 요청을 보내고 응답을 받아 검증하는 테스트에서 유용하게 사용 가능 
```java
@Test
void hello() {
	TestRestTemplate template = new TestRestTemplate();
	ResponseEntity<String> res = template.getForEntity(
	"http://localhost:8080/hello", String.class
	);

	assertThat(res.getStatusCode()).isEqualTo(HttpStatus.OK);
	assertThat(res.getBody().grim()).isEqualTo("Hello Spring");
}
```
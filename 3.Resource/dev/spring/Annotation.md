### Meta Annotation
- 애노테이션에 적용한 애노테이션을 Meta Annotation이라 함
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component   // Meta Annotation
public @interface Service {

}
```

### Composed Annotation
- 하나 이상의 메타 애노테이션이 적용된 애노테이션을 ㅁ라함
- 합성 애노테이션을 활용하면 모든 메타 애노테이션이 적용된 것과 동일한 효과를 가진다.
```java

@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Controller     // Meta Annotation
@ResponseBody   // Meta Annotation
public @interface Service {

}
```
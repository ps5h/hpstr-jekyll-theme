# @ControllerAdvice 정리

스프링의 컨트롤러 예외 전역 처리에 대한 방법.

*안돌려보고 md에 직접 작성했다...!*


## 예제 1
~~~
@ControllerAdvice
public class AdviceClassName() {
  
  @ExceptionHandler(xxxxException.class)
  public void handleXXX(Exception e) {
    e.getMessage();
  }
  
  // HTTP Status Code가 404로 리턴된다.
  @ExceptionHandler(xxxxException.class)
  @ResponseStatus(HttpStatus.NOT_FOUND, reason="전달하고싶은 에러메시지 입력")
  public void handleXXX(Exception e) {
    e.getMessage();
  }
  
  // 직접 Response를 설정할 수 있다.
  @ExceptionHandler(xxxxException.class)
  public ResponseEntity handleXXX(Exception e) {
    return new ResponseEntity("찾을 수 없다! 하지만 Status Code는 200을 리턴한다!", HttpStatus.OK);  // 에러가 났지만 200을 리턴하는! 이런 작업도 가능하다
  }
  
  // 여러개의 Exception을 받기
  @ExceptionHandler({xxxxException.class, secondException.class})
  public String handleXXX(Exception e) {
    return "실패!";
  }
}
~~~

TODO




### 참조
##### https://springboot.tistory.com/33
##### https://springboot.tistory.com/25
##### https://cnpnote.tistory.com/entry/SPRING-Spring-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC%EB%A1%9C-%EC%97%90%EB%9F%AC-404%EB%A5%BC-%EC%B2%98%EB%A6%AC%ED%95%9C%EB%8B%A4

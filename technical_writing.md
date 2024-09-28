# API 에러 응답 problem detail: 스프링에서 사용하기

## 기존의 예외 처리
서버에서 예외가 발생하면, 스프링을 사용해서 전역적으로 예외를 처리하기 위해선 주로 아래와 같은 방법을 사용합니다.
```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler
    public ResponseEntity<ResponseForError> handleException(Exception e) {
        ResponseForError responseForError = new ResponseForError(e.getMessage(), HttpStatus.BAD_REQUEST.value());
        return ResponseEntity.status(HttpStatus.BAD_REQUEST)
                .body(responseForError);
    }
}

public record ResponseForError(
        String message,
        String status
) {
}
```
위와 같은 방식에는 오류 응답 형식을 정해야 한다는 문제가 존재합니다. 이에 대한 고민을 줄이기 위해 RFC에서 정의한 오류 응답 표준이 존재합니다.

## API 예외 표준: RFC 7807
RFC7807에선 HTTP API에 대한 새로운 오류 응답 형식을 정의할 필요가 없도록 HTTP 응답에 기계가 읽을 수 있는 오류 세부 정보를 전달하는 방법으로 'problem detail'을 정의합니다. 이는 JSON과 XML 형식으로 표현될 수 있습니다. 이 글에서는 JSON 형식으로 설명하겠습니다. <br/>
problem detail은 아래와 같은 구성 요소를 가지고 있습니다.
- type

- status
- title
- detail
- instance
- properties

## ProblemDetail
RFC 9457의 예외 표준 응답의 body를 구현한 클래스 ProblemDetail에 대해 알아본다.
### 사용법
간단하게 사용하는 방법을 알아본다.
### 메서드
각 메서드에 대해 자세히 알아본다.

## ErrorResponse
RFC 9457의 예외 표준 응답 전체를 나타낸 인터페이스 ErrorResponse를 알아본다.
### 구조
ErrorResponse의 기본 구조를 알아본다.
### 메서드
ErrorResponse가 가지고 있는 메서드들을 알아본다.
### 구현 방법
인터페이스를 구현할 때, 필드와 메서드를 어떻게 설정하는 것이 좋을 지 알아본다.
### ErrorResponseException
예외 클래스에서 사용할 수 있는 ErrorResponse의 구현체 ErrorResponse를 알아본다.

## 팁: 스프링 기존 예외 응답을 사용하면서 커스텀 응답도 사용하는 방법
로깅 처리를 하기 위해 이와 같은 방식도 선택함을 명시

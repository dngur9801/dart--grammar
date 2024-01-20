# dart 기본 문법 정리

- 정수 타입
    
    ```dart
    int number = 10;
    ```
    

- 실수 타입
    
    ```dart
    double numbe = 10.5;
    ```
    

- 불리언 타입
    
    ```dart
    boolean isTrue = true;
    ```
    
- 문자열 타입
    
    ```dart
    String name = "홍길동";
    ```
    

- nullable 타입
    
    ```dart
    String? name = "홍길동";
    name = null;
    ```
    
    해당하는 타입이 null 이 될수도 있음.
    
    물음표를 넣지않으면 non-nullable함.
    

- List 타입
    
    ```dart
    List list = [1,2,3];
    
    // string타입의 배열만 가능
    List<String> list = ["홍","길","동"];
    ```
    

- Map 타입
    
    ```dart
    Map<String,String> dictionary = {
    	"Harry Potter" : "해리포터"
    };
    ```
    

- Set 타입
    
    ```dart
    Set<String> dictionary = {
    	"Harry Potter"
    };
    ```
    
    Map타입과 달리 Set타입은 중복을 제거해줌
    

- var
    
    ```dart
    var name = "홍길동";
    print(name.runtimeType);
    ```
    
    이렇게 하면 자동으로 타입이 String으로 추론이됨.
    

- dynamic
    
    ```dart
    dynamic name = "홍길동";
    print(name.runtimeType);
    ```
    
    dynamic도 var와 마찬가지로 자동으로 타입이 추론됨.
    
- var, dynamic 차이점
    
    ```dart
    var name1 = "홍길동";
    name1 = "강감찬"; ❌
    
    dynamic name2 = "홍길동";
    name2 = "강감찬"; ⭕️
    
    ```
    
    var는 재할당 불가능
    
    dynamic은 재할당 가능
    

- final
    
    ```dart
    final String name = "홍길동";
    // 재할당 불가능
    name = "강감찬" ❌
    
    // 타입 생략 가능
    final name = "홍길동"
    ```
    

- const
    
    ```dart
    const String name = "홍길동";
    // 재할당 불가능
    name = "강감찬" ❌
    
    // 타입 생략 가능
    const name = "홍길동"
    ```
    

- final const 차이점
    
    final은 빌드타임에 값을 알고있지않아도 실행이되지만
    
    const는 빌드타임에 값을 알고있어야 실행가능
    
    ```dart
    final DateTime now = DateTime.now();
    
    print(now);
    
    const DateTime now2 = DateTime.now();
    
    print(now2); // error
    
    ```
    
    위 코드에서 DateTime은 런타임 환경에서 코드가 실행되면서 값을 알수 있기에 
    
    const를 사용하면 에러가 나타남.
    
- 재할당
    
    final, const 키워드를 사용하지않은 모든 선언은 재할당이 가능하지만
    
    var 같은 경우 final과 const 키워드를 사용하지 못하기 때문에 재할당을 막을수가 없다.
    
    그러기에 의도적으로 재할당을 해야하는 경우가 아니라면 var 사용을 지양하여서 코드를 읽을때 흐름을 방해하는 일이 없도록 하는게 좋을 것 같다.

## operator
- null 인지 연산자 (??=)
    
    ```dart
    int number = 3;
    number ??= 5;
    ```
    
    number가 null일 경우 5를 할당 아닐경우 기존값 유지
    
- is
    
    ```dart
    int number = 4;
    print(number is int); // true
    print(number is! int); // false
    ```
    
    변수가 주어진 타입과 동일한지

## 함수 
- 함수 선언
    
    ```dart
    int addNumber(int num1,int num2) {
    	return num1 + num2
    };
    ```
    

- 화살표 함수 선언
    
    ```dart
    int addNumber(int num1, int num2) => num1 + num2;
    ```
    

- optional parameter
    
    ```dart
    void main() {
    	addNumber(10);
    }
    
    // 기본값 지정
    addNumber(int x, [int y = 20]) {
    	print(x); // 10
      print(y); // 20
    }
    
    // 기본값 지정 X
    addNumber(int x, [int? y]) {
    	print(x); // 10
      print(y); // null
    }
    ```
    
    []로 감쌀경우 필수값이 아니게됨.
    
    대신 int로 선언하였기에 기본값을 넣어줌. (넣지않을경우 null)
    

- named parameter
    
    ```dart
    void main() {
      addNumber(x:10);
    }
    
    addNumber({
      required int x,
      int y = 30
    }) {
      print(x); // 10
      print(y); // 30
    }
    ```
    
    required는 필수값, required를 제거할경우 optional로 지정됨.

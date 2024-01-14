# dart 기본 문법 정리

## 변수

dart에서 변수는 할당하려는 값에 타입에 맞게 선언해주어야 한다

- 정수 타입

```dart
int number = 10;
```

- 실수 타입

```dart
double numbe = 10;
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

이렇게 하면 자동으로 타입이 String으로 추론이 되지만

명시적으로 타입을 작성하는것이 유지보수 측면에서 유리함

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

print(now2);

```

위 코드에서 DateTime은 런타임 환경에서 코드가 실행되면서 값을 알수 있기에 

const를 사용하면 에러가 나타남.

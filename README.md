# dart 기본 문법 정리

## 타입

### 정수 타입

```dart
int number = 10;
```

### 실수 타입

```dart
double numbe = 10.5;
```

### 불리언 타입

```dart
boolean isTrue = true;
```

### 문자열 타입

```dart
String name = "홍길동";
```

### nullable 타입

```dart
String? name = "홍길동";
name = null;
```

해당하는 타입이 null 이 될수도 있음.

물음표를 넣지않으면 non-nullable함.

### List 타입

```dart
List list = [1,2,3];

// string타입의 배열만 가능
List<String> list = ["홍","길","동"];
```

### Map 타입

```dart
Map<String,String> dictionary = {
	"Harry Potter" : "해리포터"
};
```

### Set 타입

```dart
Set<String> dictionary = {
	"Harry Potter"
};
```

Map타입과 달리 Set타입은 중복을 제거해줌

### var

```dart
var name = "홍길동";
print(name.runtimeType);
```

이렇게 하면 자동으로 타입이 String으로 추론이됨.

### dynamic

```dart
dynamic name = "홍길동";
print(name.runtimeType);
```

dynamic도 var와 마찬가지로 자동으로 타입이 추론됨.

### var, dynamic 차이점

```dart
var name1 = "홍길동";
name1 = "강감찬"; ❌

dynamic name2 = "홍길동";
name2 = "강감찬"; ⭕️

```

var는 재할당 불가능

dynamic은 재할당 가능

### final

```dart
final String name = "홍길동";
// 재할당 불가능
name = "강감찬" ❌

// 타입 생략 가능
final name = "홍길동"
```

### const

```dart
const String name = "홍길동";
// 재할당 불가능
name = "강감찬" ❌

// 타입 생략 가능
const name = "홍길동"
```

### final const 차이점

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

### 재할당

final, const 키워드를 사용하지않은 모든 선언은 재할당이 가능하지만

var 같은 경우 final과 const 키워드를 사용하지 못하기 때문에 재할당을 막을수가 없다.

그러기에 의도적으로 재할당을 해야하는 경우가 아니라면 var 사용을 지양하여서 코드를 읽을때 흐름을 방해하는 일이 없도록 하는게 좋을 것 같다.

## operator
### null 인지 연산자 (??=)

```dart
int number = 3;
number ??= 5;
```

number가 null일 경우 5를 할당 아닐경우 기존값 유지

### is

```dart
int number = 4;
print(number is int); // true
print(number is! int); // false
```

변수가 주어진 타입과 동일한지

## 함수 
### 함수 선언

```dart
int addNumber(int num1,int num2) {
	return num1 + num2
};
```

### 화살표 함수 선언

```dart
int addNumber(int num1, int num2) => num1 + num2;
```

### optional parameter

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

### named parameter

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

## class

### class 선언과 인스턴스 생성

class란 객체를 만들기위한 설계서로 class에서 정의한 속성들을 가지고 여러 객체를 생성할때 사용한다.

```dart
void main() {
  // new Idol, Idol 둘다 가능
  Idol bts = Idol("방탄소년단", ["정국,RM"]);

  print(bts.name); // 방탄소년단
  print(bts.members); // ["정국","RM"]
  bts.sayHello(); // 안녕하세요 방탄소년단입니다.
}

class Idol {
	// 변수 선언
  final String name;
  final List<String> members;

  // constructor
  Idol(this.name, this.members);

  void sayHello() {
    print("안녕하세요 ${this.name}입니다.");
  }
}
```

- 하나의 class로 여러 instance를 선언할 수 있다.
- constructor 사용시 instance를 생성할때 원하는 값을 넣어서 생성이 가능하다.
- this는 자신이속한 class를 지칭한다.

### 상속 (inheritance)

```dart
void main() {
  // new Idol, Idol 둘다 가능
  Idol apink = Idol(name: "에이핑크", membersCount: 5);

  apink.sayHello();
  apink.sayMembersCount();

  BoyGroup bts = BoyGroup("BTS", 7);

  // Idol class의 모든 속성 사용가능
  bts.sayHello();
  bts.sayMembersCount();
}

class Idol {
  final String name;
  final int membersCount;

  // constructor
  Idol({required this.name, required this.membersCount});

  void sayHello() {
    print("안녕하세요 ${this.name}입니다.");
  }

  void sayMembersCount() {
    print("${this.name}은 ${this.membersCount}명의 멤버가 있습니다");
  }
}

class BoyGroup extends Idol {
  BoyGroup(
    final String name,
    final int membersCount,
  )
  // super 키워드로 부모 constructor 상속받음
  : super(
          name: name,
          membersCount: membersCount,
        );
}
```

- extends 키워드로 부모 class를 상속받을 수 있음.
- 상속 받은 자식 class는 부모 class의 모든 속성 사용 가능.
- 부모 constructor를 사용하기 위해서 super 키워드를 사용해야함.

### override (덮어쓰기)

```dart
void main() {
  TimesTwo tt = TimesTwo(2);

  print(tt.calculate());

  TimesFour tf = TimesFour(2);

  print(tf.calculate());
}

class TimesTwo {
  final int number;

  TimesTwo(this.number);

  int calculate() {
    return this.number * 2;
  }
}

class TimesFour extends TimesTwo {
  TimesFour(int number) : super(number);

  @override
  int calculate() {
    return super.number * 4;
  }
}
```

@override 키워드를 사용후 override할 메서드를 재정의하면 가능하다.

### static

```dart
void main() {
  Employee seulgi = Employee('슬기');

  // static으로 선언하지 않은 속성은 인스턴스 귀속
  seulgi.printNameAndBuilding();
  // static으로 선언한 속성은 클래스 귀속
  Employee.printBuilding();
}

class Employee {
  static String? building = "오투타워";
  final String name;

  Employee(
    this.name,
  );

  void printNameAndBuilding() {
    print("제 이름은 ${name}입니다. ${building} 건물에서 근무하고 있습니다.");
  }

  static void printBuilding() {
    print('저는 ${building} 건물에서 근무중입니다.');
  }
}
```

static은 instance에 귀속되지 않고 class에 귀속된다. 즉 instance에서는 접근이 불가하고 class선언으로만 접근이 가능하다.

### interface

어떤 특수한 구조를 강제하기 위한 일종의 설계서

interface를 선언 후 implements 키워드를 사용한다.

```dart
void main() {
  BoyGroup bts = BoyGroup("BTS");
}

// abstract 키워드로 IdolInterface로 인스턴스를 생성하지 못하도록 제어
abstract class IdolInterface {
  String name;

  IdolInterface(this.name);

  void sayName();
}

// IdolInterface에서 선언한 타입을 필수로 작성하지 않으면 에러가 나타남.
class BoyGroup implements IdolInterface {
  String name;

  BoyGroup(this.name);

  void sayName() {
    print("제 이름은 ${name} 입니다.");
  }
}
```

### generic

타입을 외부에서 받을때 사용

```dart
void main() {
  Lecture<String> lecture1 = Lecture("123", "lecture1");
  lecture1.printIdType(); // String

  Lecture<int> lecture2 = Lecture(123, "lecture2");
  lecture2.printIdType(); // int
}

// T대신 원하는 네이밍으로도 입력 가능
class Lecture<T> {
  final T id;
  final String name;

  Lecture(this.id, this.name);

  void printIdType() {
    print(this.id.runtimeType);
  }
}
```

- generic은 여러 타입을 넣을수 있음 (<T, U, Type>)

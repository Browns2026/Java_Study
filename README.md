# Java_Study
@ 03 June, 2026

핵심 6가지
1. 클래스 / 객체 / 생성자
2. static / final
3. 상속 / 오버라이딩
4. 다형성
5. 추상 클래스 / 인터페이스
6. 제네릭 기초

---

클래스와 객체 (Class and Object)
---
- Class 는 객체를 만들기 위한 설계도다.

        class Student
        {
            String name;
            int age;

            void printInfo()
            {
                System.out.printIn(namd+ "," + age);
            }
        }

|코드|뜻|
|---|---|
|Student| 클래스 이름|
|String name| 필드, 객체가 갖는 데이터|
|int age| 필드|
|printInfo()|메소드, 객체가 수행하는 기능|

즉, 플래스 안에는 보통 필드 + 메소드가 들어간다.

---
객체(Object)
---
- 클래스로부터 실제로 만들어진 대상이다.

        Student s1 = new Student();

    이 말은 곧, Student 타입 변수 s1 을 만들고,  
    new Student()로 Student 객체를 생성한 뒤, 그 객체를 s1이 가리킨다.

    예시로 다시 설명하자면, 
        
        class Stduent{
            String name;
            int age;

            void printInfo()
            {
                System.out.pringIn(name + "," + age);
            }
        }
        public class Main{
            public static void main (String{} args) {
                Student s1 = new Student();

                s1.name = "Kim";
                s1.age = 20;

                s1.printInfo();
            }
        }

    이때 출력값은 Kim 과 20 이 되며, s1.name 은 s1 객체의 name 필드에 접근한다는 뜻이자,  
    s1.printInfo()는 s1 객체의 메소드를 실행한다는 뜻이다.

---

생성자
---
- 객체가 만들어질 때 자동으로 실행되는 초기화 메소드다.

        public class Main{
            public static void main (String[] args) {
                Student s1 = new Student("Kim", 20);
                s1.printInfo();
            }
        }

|특징|설명|
|---|---|
|클래스 이름과 동일| Student 클래스의 생성자는 Student() 이다|
|반환형이 없다|void도 사용하지 않음|
|객체 생성시 자동 실행된다|new Student(...) 할때 실행|
|필드 초기화에 자주 사용|name, age 값 설정 등|

---
this
---
- 현재 객체 자신을 의미한다.
        class Student {
            String name;
            int age;

            Student(String name, int age) {
                this.name = name;
                this.age - age;
            }
        }
    이게 무슨 말이냐면, this.name 은 객체의 필드, name 은 생성자의 매개변수를 뜻한다.  
    즉, **현재 객체의 name 필드에 매개변수 name 값을 넣어라.** 라는 의미가 된다.

---
Static
---
기본적으로 크게 Static Field 와 Static Method 가 나온다.

- Static 필드
    - 객체마다 따로 생기는 값이 아닌, 클래스가 공유하는 값이다.

            class Counter {
                static int count = 0;

                Counter() {
                    counter++;
                }
            }
            public class Main{
                public static void main(String[] args){
                    Counter c1 = new Counter();
                    Counter c2 = new Counter();
                    Counter c3 = new Counter();

                    System.out.println(Counter.count);
                }
            }

        이렇게 했을 때 나오는 출력값은 3이다.

        그 이유는
        1. new Counter()가 세번 실행되기 때문이다.
        2. 생성자가 실행될 때마다 count++
        3. count 는 객체별 값이 아닌 클래스 공유값이다.
        
        따라서 최종값은 3이 된다.

    
### 일반 필드와 static 필드의 차이
        class Counter{
            int normalCount = 0;
            static int staticCount = 0;

            Counter(){
                normalCount++;
                staticCount++;
            }
        }
    
    
객체를 3개 만든다면, 
|필드|결과|
|---|---|
|normalCount|각 객체마다 1|
|staticCount|클래스 전체에서 3|

쉽게 말해, 일반 필드는 객체마다 따로 공유하고
static 필드는 클래스 전체가 공유된다.

---
static 메소드
---
객체를 만들지 않고 클래스 이름으로 호출할 수 있다.

    class MathUtil{
        static int add(int a, int b){
            return a+b;
        }
    }
    public class Main {
        public static void main(string[] args) {
            System.out.println(MathUtil.add(3,5));
        }
    }

출력 결과는 8이 된다.
여기서의 핵심은 MathUtil.add(3,5) 가 된다.
그 이유는 별도의 객체 없이 호출이 가능했기 때문이다.

즉, static 메소드는 객체 없이 클래스명 만으로 호출이 가능하다.

---
final
---
**변경불가/ 재정의불가/ 상속불가** 라고 생각하면 된다.

|위치|의미|
|---|---|
|final 변수|갑 변경 불가|
|final 메소드|오버라이딩 불가|
|final 클래스|상속 불가|

이 세가지를 중심으로 다뤄진다고 보면 된다.

가장 처음인 final 변수의 경우,

    final int MAX = 100;
    MAX = 200; // 에러

이 말은 즉, final int MAX 에 100 이란 숫자를 넣으면 값을 바꿀 수 없다.

---
### final 메소드

    class Parant {
        final void print(){
            System.out.println("parant);
        }
    }
    class Child extends Parent{
        void print(){
            System.out.println("child);
        } // 에러 발생
    }
부모 메소드가 final 이면 자식이 overriding 될 수 없다 라는 의미이다.

---
상속
---
부모 클래스의 필드와 메소드를 자식 클래스가 물려받는 것이다.

    class Animal {
        void sound() {
            System.out.println("animal");
        }
    }

    class Dog extends Animal {
        @Override
        void sound() {
            System.out.println("dog");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Dog d = new Dog();
            d.sound();
        }
    }
출력 결과는 dog 이 되겠다. 그 이유는, 
- Dog 이 Animal 의 sound()를 다시 정의했기 때문이다.
- Dog 객체에서 sound()를 호출하면 자식 메소드가 실행된다.

### 오버라이딩 조건
|조건|설명|
|---|---|
|메소드 이름 같아야 함| sound()|
|매개변수 같아야 함|괄호 안 구조가 같아야 한다|
|상속 관계여야 함|부모-자식 클래스 관례를 의미한다|
|반환 타입도 호환되어야 함|기본적으로 같다고 생각하면 됨|

---
다형성
---
금일 복습하는 내용중 가장 중요하다고 볼 수 있는 단락이다.

- 부모 타입 변수로 자긱 객체를 참조할 수 있는 성질 이다.

        Animal a = new Dog();
    이걸 보고 다형성 이라고 한다.

    다형성 즉, Polymorphism은
        
        class Animal {
            void sound(){
                System.out.println("animal");
            }
        }
        class Dog extends Animal {
            void sound(){
                System.out.println("dog");
            }
        }
        public class Main{
            public static void main(String[] args) {
                Animal a1 = new Dog();
                Animal a2 = new Cat();

                a1.sound();
                a2.sound();
            }
        }
    이런식으로 부모 자식 관계를 중심으로 이뤄져있고, 이때 출력되는 값은 dog 그리고 cat 이다.  
    명확하게 구분하자면,  
    
    - a1.sound() 에서는 dog 이런식으로,  
    - a2.sound() 에서는 cat 로 출력될 것이다.

그렇다면 그렇게 나오는 이유가 뭘까?

|변수|참조타입|실제객체|실행메소드|
|---|---|---|---|
|a1|Animal|Dog|Dog의 sound|
|a2|Animal|Cat|Cat의 sound|

이 표를 풀자면, 참조변수 타입은 Animal 이지만, 실제 객체가 Dog 라면 Dog 메소드가 실행된다.  
실제 객체가 Cat 이면 Cat 메소드가 실행된다.  
따라서, **오버라이딩** 된 메소드는 참조변수 타입이 아닌 실제 객체 타이블 기준으로 실행된다.

---
---
추상 클래스
---
추상클래스는 두개로 나눌 수 있다.
하나는 일반적인 추상 클래스와 인터페이스가 되겠다.

우리가 알고 있는 추상 클래스는 미완성 클래스라고 볼 수 있다.

    abstract class Shape {
        abstract double getArea();

        void print(){
            System.out.println("Shape");
        }
    }
|특징|설명|
|---|---|
|abstract 사용|추상 클래스/메소드|
|객체 생성 불가|new Shape()사용 불가|
|추상 메소드 가능|몸체 없는 메소드|
|일반 메소드 가능|print()처럼 구현된 메소드도 가능|
|자식 클래스 구현|추상 메소드를 자식이 완성시킴|

예시로는

    abstract class Shape{
        abstract double getArea();
    }
    class Circle extend Shape{
        double radius;

        Circle(double radius){
            this.radius = radius;
        }
        double getArea(){
            return radius * radius * 3.14;
        }
    }
    public class Main{
        public static void main(String[] args){
            Shape s = ew Circle(10);
            System.out.println(s.getArea());
        }
    }
이때 출력되는 값은 314.0 이다.

그런 이유는 쉽게
1. shape 는 추상 클래스라 직업 객체 생성 불가하다.
2. 하지만 Circle 은 Shape 를 상속하고 getArea()를 구현한다.
3. Shape s = new Circle(10); 는 다향성을 의미하고
4. 실제 객체는 Circle 이므로 Circle 의 getArea() 실행된다.

---
인터페이스
---
구현해야 할 가능의 약속/계약 이라고 보면 된다.

    interface Flyable{
        void fly();
    }
이 인터페이스를 구현하는 클래스는 fly()를 반드시 구현해야 한다.

    class Bird implements Flyable{
        public void fly(){
            System.out.println("bird");
        }
    }

.
    
    public class Main{
        public static void main(String[] agrs){
            Flyable f = new Bird();
            f.fly();
        }
    }
출력되는 값은 bird fly 이다.

1. 인터페이스는 implements로 구현한다.
2. 인터페이스 타입으로 구현 객체를 참조할 수 있다.
3. 다형성이다.
---
---


추상 클래스와 인터페이스 비교
---
|구분|추상클래스|인터페이스|
|---|---|---|
|키워드|abstract class|interface|
|사용|extends|implement|
목적|공통 부모 역할|기능 계약/규칙|
|객체 생성|불가능|불가능|
|다중 적용|클래스 상속 하나만 가능|여러개 구현 가능|
|일반 메소드|가능|기능명세|

예시로,
    
    abstract class Animal{
        abstract void sound();
    }
이건 동물이라는 동통 부모 라고 한다면

    interface Flyable{
        void fly();
    }
이건 날 수 있는 기능을 가진다고 볼 수 있다.

---
제네릭
---
타입을 나중에 정하는 문법이다.

예를 들어, 제네릭이 없을 때

    class Data{
        private Object object;

        public void set(Object object){
            this.object = object;
        }
        public Object get(){
            return object;
        }
    }

사용하게 된다면,
        
        Data data = new Data();
        data.set("hello");

        String s = (String)data.get();
1. get()의 반환 타입이 Object 라서
2. String 으로 형변환 해야하며
3. 이를 잘못 형변환하면 실행도중 오류가 발생한다.

그래서 제네릭을 사용한다면

    class Data<T>{
        private T value;

        public void set(T value){
            this.value = value;
        }

        public T get(){
            return value;
        }
    }
-
    
    Data<String> data = new Data<String>();
    data.set("hello");

    String s = data.get();
    System.out.println(s);

출력값은 hello 가 된다.

이는
1. 형변환이 불필요하며
2. 타입 안정성이 높아지고
3. 동시에 컴파일 시점에 타입 오류를 잡을 수 있다.

---
제네릭에는 핵심이 존재하는데,
    
    Data<String>
은 Data 객체는 String 타입을 저장한다는 의미이다.

    Data<Integer>
는 Data 객체는 Integer 타입을 저장한다는 의미이다.

쉽게 말하자면
- 제네릭은 클래스나 메소드에서 사용할 타입을 미리 고정하지 않고, 객체 생성 시 타입을 지정할 수 있게 하는 기능이다.


오늘의 공부 요약

|개념|의미|
|---|---|
|클래스|객체를 만들기 위한 설계도|
|객체|클래스로부터 생성된 실제 대상|
|필드|객체의 데이터|
|메소드|객체의 기능|
|생성자|객체 생성 시 초기화|
|this|현재 객체 자신|
|static|클래스 소속, 객체들이 공유|
|final 변수|값 변경 불가|
|상속|부모 기능을 자식이 물려받음|
|오버라이딩|부모 메소드를 자식이 재정의|
|다형성|부모 타입으로 자식 객체 참조|
|추상 클래스|미완성 클래스, 객체 생성 불가|
|인터페이스|구현해야 할 기능 계약|
|제네릭|타입을 나중에 지정|

---

@06 June,2026 이어서 공부
---
1. 패키지
    - 관련 있는 클래스들을 묶어 놓은 단위이다. 즉, 클래스들을 정리하기 위한 폴더 같은 개념이다.

    |패키지|역할|
    |---|---|
    |java.lang|기본 클래스 제공|
    |java.util|컬렉션, 날짜, Scanner 등|
    |java.io|입출력 관련|
    |java.nio|new 입출력/파일 경로 처리|
    |java.sql|JDBC, DB 연결 관련|

---
#### import
- 다른 패키지에 있는 클래스를 사용하려면 import 를 사용해야한다.
    
        import java.util.Scanner;
        이 말은 즉, java.util 패키지에 있는 Scanner 클래스를 사용해겠다 라는 의미이다.

        유니티 게임에서도 이와 비슷한 것이 있다. 는 사실 개발 언어에는 다 있는 것 같다... ㅠ

        또는

        import java.util.*;

        java.util 패키지의 여러 클래스를 사용하겠다 라는 의미이며, java.lang 패키지는 자동으로 포함되므로 별도로 import 하지 않아도 된다 라는 뜻이다.

    예를 들어, String, System, Math, Object, Integer 과 같은 것들은 java.lang 에 내포된 내용이라 바로 사용이 가능하다.

---

2. 예외처리
- 예외처리란, 말 그래도 예외 상황을 처리힐 때 사용하는 건데, 예외가 발생하면 프로그램이 비정상 종료가 될 수 있기에 Java에서는 예외처리 문법을 제공한다.

1. try-catch문
        
        try {
            예외 발생 가능한 코드 
        } catch (Exception e) {
            예외가 발생 했을 때 처리할 코드
        }
    
    |구분|의미|
    |---|---|
    |try|예외 발생 가능 코드|
    |catch|예외 발생 시 처리 코드|
    |Exception e|발생한 예외 객체|

    를 기본 문법을 바탕으로 사용된다.
    즉 이 말은 try 블록에서 예외가 발생하면 catch 블록에서 이를 처리 한다는 뜻으로도 볼 수 있다.

    ---
2. finally
- 예외 발생 여부와 상관없이 실행된다.

        try {
            // 예외발생 가능 코드
        } catch (Exception e) {
            // 예외 처리
        } finally {
            // 항상 실행
        }

    ---

3. throws
- 예외 처리를 현재 메소드에서 하지 않고 호출한 쪽으로 넘기는 것이다.

        void reaDile() throws IOExecpeion {
            // 파일 읽기
        }
    이는 곧 해당 메소드에서는 IOException이 발생할 수 있으니, 이를 호출한 쪽에서 처리해라 라는 의미가 된다.

그 외에도 checked exception/ unchecked exception 이 있는데,
    
1. checked exception - 컴파일러가 예외처리를 강제한다.
2. unchecked exception - 실행 중 발생, 컴파일러는 이를 강제하지 않는다. 

와 같은 조건 등이 있다.

|예외|종류|
|---|---|
|IOException|checked exception|
|SQLException|checked exception|
|NullPointerException|unchecked exception||ArithmeticException|unchecked exception|
|ArrayIndexOutOfBoundsException|unchecked exception|

---

java.lang 패키지
---
- Java의 기본 패키지다. 이는 위에서 언급한 대로 별도로 import 하지 않고 자동으로 사용할 수 있다는 큰 장점이 있다.

주요 클래스로는 우리가 잘 알고 있는

|클래스|뜻|
|---|---|
|Object|모든 클래스의 최상위 클래스|
|String|문자열|
|StringBuffer|변경 가능한 문자열|
|StringBuilder|변경 가능한 문자열|
|System|표준 입출력, 시스템 기능|
|Math|수학 메소드 - C# 에서는 Mathf 로 사용됨|
|Integer, Double 등|Wrapper 클래스|

이것들이 포함된다.

---
그러면 이제부터 위의 목록들에 대해 알아보자.

Object 객체 클래스
---
- 모든 Java클래스의 푀상위 클래스다.
즉, 모든 클래스는 직접/간접적으로 Object를 상속받는다.

주요 메소드로는
1. toString() - 객체를 문자열로 표현 -> 클래스명@해시코드
2. equals() - 객체 비교 -> ==는 참조값 비교, equals()는 내용 비료용으로 재정의해서 사용 가능
3. hashCode() - 객체의 해시값 반환 -> 객체 저장/검색에서 사용된다. 이전 DB 에서 배운 내용과 유사하며 HashSet, HashMap 같은 해시 기반 자료구조에서 중요하다.
4. getClass() - 객체의 클래스 정보 반환
5. String / StringBuffer / StringBuilde - 쉽게 말해 문자열, 변경가능 문자열을 의미한다.
여기서의 변경가능 문자열 이라 함은, StringBuffer 에서는 멀티스레드 환경에서 상대적으로 안전하며, StringBuilder 은 단일 스레스 환격에서 적합하다는 차이만 존재한다.

---

Wrapper 클래스
---
이는 기본 자료형을 객체처럼 다루기 위한 클래스다.

|기본형|Wrapper 클래스|
|---|---|
int|Integer
double|Double
char|Character
boolean|Boolean
long|Long
float|Float

예를 들면 이렇게 구분할 수 있다.
        
    Integer a = 10; // 오토 박싱
    int b = a; // 오토 언박싱


여기서의 오토 박싱/언박싱 이 뭔지 알아보자.

### Boxing / Unboxing
1. Boxing - 기본형을 객체로
2. Unboxing - 객체 를 기본형으로

바꾸는 것을 의미한다.

---

컬렉션
---
- 여러 데이터를 저장하고 관리하는 자료구조다. 배열과 비슷하지만 사용성이 더 유연하다.

|인터페이스|특징|
|---|---|
List|순서가 있으며 중복허용 가능하다
Set|순서 보장 안되며 중복허용도 불가능하다
Queue|먼저 들어간 데이터가 먼저 나오는 구조
Map|key-value 쌍으로 저장


1. ArrayList - 배열, 조회 빠름
2. LinkedList - 연결 구조, 삽입/삭제에 유리

3. HashSet - 해시기반, 중복제거
4. TreeSet - 정렬된 Set

5. Key-value - 한 쌍으로 저장된다.
    - HashMap - 해시기반 key-value 저장
    - TreeMap - key 기준 정렬
    - Map은 key-value 쌍으로 데이터를 저장하며, key는 중복될 수 없다.

### 중요한 비교도
|구분|List|Set|Map|
|---|---|---|---|
|저장방식|값 목록| 값 집합|key-value|
|순서|유|무|key 기반 유|
|중복|가능|불가능|key값 중복 불가|
|대표|ArrayList|HashSet|HashMap|

---

스트림 Stream
---
- 컬렉션이나 배열같은 데이터들을 흐름처럼 처리하는 기능이다.

사용하는 복적으로는 반복, 필터링, 변환, 정렬, 집계 등을 간결하게 처리 하기 위해 사용된다.

이를 사용하기 위해서는 외부/내부 반복이 존재하는데,

1. 외부반복은 사용자가 직접 반복문을 작성한다.
    - for / while / Iterator 문이 존재하며
2. 내부반복은 반복 처리를 스트림이나 컬렉션에 맡긴다.
    - forEach() 문이 대표가 되겠다.

### 중요 메소드
|메소드|뜻|
|---|---|
|forEach()|각 요소 하나씩 처리|
|filtear()|조건에 맞는 요소만 선택 : 반복 처리|
|map()|요소 형태 변환, 예 학생 객체 -> 학생 이름|
|sorted()|정렬|
|distinct()|중복제거|
|count()|개수|
|collect()|결과 수집|

지금까지 봐온 각 함수, 메소드의 이름은 직관적이라 바로 유추 할 수 있다. 휴우-

---

입출력 스트림 java.io
---
- 데이터가 이동하는 통로다.
쉽게 말하자면, 외부 -> 프로그램 으로의 이동을 입력 스트림이라 하며, 프로그램 -> 외부 로 출려되는걸 출력 스트림이라고 한다.

이러면 설명이 더 필요하겠다;;
간단하게, 키보드에서 입력(외부) -> 프로그램(VScode) 이걸 입력 스트림, 그 반대 상황을 출력 스트림 이라고 하는게 더 맞는 표현이겠다. 대신에 외부다 그 외부다 아닌, 데이터를 읽냐 보내냐의 관점으로 바꿔야 한다.

바이트 스트림 / 문자 스트림
- byte stream/byte 단위 구성 - InputStream, OutupStream
- char Stream/문자 단위 구성 - Reader,Writer

### 주요클래스
|클래스|뜻|
|---|---|
|FileInputStream|파일에서 byte 단위 입력|
|FileOutputStream|파일에 byte 단위 출력|
|FileReader|파일에서 문자 단위 입력|
|FileWriter|파일에 문자 단위 출력|
|BufferedReader|버퍼를 이용한 문자 입력|
|BufferedWriter|버퍼를 이용한 문자 출력|

---

NIO
---
- 기존 java.io 보다 더 발전된 입출력 기능을 제공하는 패키지이다.
java.nio.file에서는 파일 경로와 파일 처리를 다룬다.

- Path 는 파일이나 디렉터리의 경로를 표현하는 인터페이스다.
- Files 클래스는 파일을 다루는 여러 정적 메소드를 제공한다.
    - 예를 들면 파일 존재여부 확인, 복사, 삭제, 읽기, 쓰기 등
---

스레드
---

|개념|뜻|
|---|---|
|프로세스| 실행중인 프로그램|
|스레드|프로게스 안에서 실행되는 작업 흐름|

이는 곳 하나의 프로세스 안에 여러 스레드가 존재할 수 있다는 얘기다.

1. 멀티 스레드
- 하나의 프로그램 안에서 멀티(Multi) 즉, 여거 작업 흐름이 동시에 실행되는 것이다.
이에 따른 장점으로는 동시에 여러 작업 처리가 가능하며 자원 활용 효율성이 증가 한다는 점이지만, 공유 데이터로 접근 시, 동기화가 반드시 필요하다.

2. 스레드 생성 방법
- Thread 클래스 상속시, Thread를 상속받아 run() 를 재정의하고
Runnable 인터페이스 구현시, Runnable의 run() 구현 후 Thread 에 전달한다.

그러면, 스레드를 사용하려면 어떻게 해야 할까, 

|메소드|뜻|
|---|---|
|start()|새 스레드를 시작한다.
|run()|스레드가 수행할 작업 내용을 의미

이 말은 즉, 스레드를 시작하려면 run()을 직접 호출하는 것이 아닌, start()를 이용해, 호줄해야 한다는 점이다.

그러면 아까 말한대로, 공유 데이터로 접근기, 동기화가 필요하다고 했는데, 

3. 동기화
- 여러 스레드가 같은 데이터를 동시에 수정하면 문제가 생길 수 있는데 이를 막기 위해 동시화를 사용한다. 이는 곧 동기화는 여러 각종 자원에 의해 동시 접근해서 irragular 하게 수정되는 부분을 막기 위해 생긴 방안이다.

---

JDBC
---
- Java에서의 데이터베이스(DB)에 접속하고 SQL을 실행하기 위한 API이다.
JDBC (Java Database Connectivity)

사용되는 흐음은 이러하다.

|단계|뜻|
|---|---|
1. 드라이버 준비 - DBMS에 맞는 JDBC 드라이버 사용
2. Connection 생성 - DB 연결
3. Statement 생성 - SQL 실생 객체 생성
4. SQL 실행 - SELECT, INSERT 등 실행
5. ResultSet 처리 - SELECT 결과 처리
6. close - 자원 닫기

### 주요 객체
|객체|의미|
|---|---|
|Connection|DB 연결|
|Statement|SQL 실행|
|PreparedStatement|미리 준비된 SQL 실행
|ResultSet|SELECT 결과 저장|
|DriverManager|DB 열결 관리|

즉, Connection은 DB 연결, Statement는 SQL 실행, ResultSet은 조회 결과를 의미한다.

---

라이브러리와 모듈
---
- 라이브러리
    - 라이브러리는 재사용 가능한 클래스와 기능을 묶어놓은 것이다.
    - 예를 들면 jar 파일, 외부 API, 공통 기능 묶음 등이 있다.
- JAR
    - Java Archive의 약자로, 여러 클래스 파일과 자원을 하나로 묶은 파일을 의미한다.
- 모듈
    - Java 9 이후 도입된 기능으로, 관련 패키지와 리소스를 묶고 의존성을 명시적으로 관리한다.

    1. module-info.java
        - 모든 정보를 정의하는 파일이다.
        - moudule : 모듈 선언
        - required : 필요한 다른 모듈 지정
        - export : 외부에 공개할 패키지 지정

---

## 정리표
|비교|반드시 외울 것|
|---|---|
|인스턴스 필드 vs static 필드|객체별 존재 vs 클래스 공유
|final 변수/메소드/클래스|변경 불가 / 오버라이딩 불가 / 상속 불가
|오버로딩 vs 오버라이딩|매개변수 다름 / 부모 메소드 재정의
|추상 클래스 vs 인터페이스|공통 부모 / 기능 계약
|throw vs throws|직접 발생 / 호출자에게 위임
|checked vs unchecked|컴파일러 강제 / 실행 중 예외
|== vs equals()|참조 비교 / 내용 비교
|String vs StringBuffer vs StringBuilder|불변 / 동기화 변경 가능 / 비동기화 변경 가능
|List vs Set vs Queue vs Map|순서+중복 / 중복X / FIFO / key-value
|filter vs map vs forEach|조건 / 변환 / 처리
|byte stream vs character stream|byte / char
|Thread vs Runnable|클래스 상속 / 인터페이스 구현
|start() vs run()|새 스레드 시작 / 실행 내용
|Connection vs Statement vs ResultSet|DB 연결 / SQL 실행 / 결과 저장
|requires vs exports|필요한 모듈 / 공개 패키지|

@07 June, 2026
일단 공부 내용 정리는 여기까지 하고, 다시 보면서 내용을 수정 및 추가는 이후에 할 예정
---


생성자 = 클래스 이름과 같고 new 할 때 자동 호출  
static = 클래스가 하나를 공유  
오버로딩 = 같은 이름, 매개변수 다름  
오버라이딩 = 상속 관계에서 부모 메소드 재정의  
다형성 = 부모 타입으로 자식 객체 참조, 실행은 실제 객체 기준  
==는 참조 비교, equals()는 내용 비교

List = 순서 있음, 중복 가능  
Set = 중복 불가  
Map = key-value, key 중복 불가

---

### 출근길 복습표
1. 클래스 / 객체 / 생성자 / this
2. static / final
3. 오버로딩 / 오버라이딩
4. 상속 / 다형성
5. 추상 클래스 / 인터페이스
6. Object / String / equals
7. 컬렉션 List / Set / Map
8. Stream / Thread / JDBC

        class Student {
            String name;

            ______(String name) {
                this.name = name;
            }
        }

---

        class Counter {
            ______ int count = 0;
        }


---
        class Animal {
            void sound() {
                System.out.println("animal");
            }
        }

        class Dog ______ Animal {
            void sound() {
                System.out.println("dog");
            }
        }

---

        class Counter {
            static int count = 0;

            Counter() {
                count++;
            }
        }

        public class Main {
            public static void main(String[] args) {
                new Counter();
                new Counter();
                new Counter();

                System.out.println(Counter.count);
            }
        }

---

        class Animal {
            void sound() {
                System.out.println("animal");
            }
        }

        class Dog extends Animal {
            void sound() {
                System.out.println("dog");
            }
        }

        public class Main {
            public static void main(String[] args) {
                Animal a = new Dog();
                a.sound();
            }
        }

---


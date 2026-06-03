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

    이 말은 곧, Student 타입 변수 s1 을 만들고, new Student()로 Student 객체를 생성한 뒤, 그 객체를 s1이 가리킨다.

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

    이때 출력값은 Kim 과 20 이 되며, s1.name 은 s1 객체의 name 필드에 접근한다는 뜻이되며, s1.printInfo()는 s1 객체의 메소드를 실행한다는 뜻이다.

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
    이게 무슨 말이냐면, this.name 은 객체의 필드, name 은 생성자의 매개변수를 뜻한다. 즉, 현재 객체의 name 필드에 매개변수 name 값을 넣어라. 라는 의미가 된다.

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
변경불가/ 재정의불가/ 상속불가 라고 생각하면 된다.

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
final 메소드

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

그렇다면 그렇게 나오는 이유가 뭘까?

|변수|참조타입|실제객체|실행메소드|
|---|---|---|---|
|a1|Animal|Dog|Dog의 sound|
|a2|Animal|Cat|Cat의 sound|

이 말을 풀자면, 참조변수 타입은 Animal 이지만, 실제 객체가 Dog 라면 Dog 메소드가 실행된다.
실제 객체가 Cat 이면 Cat 메소드가 실행된다.
따라서, 오버라이딩 된 메소드는 참조변수 타입이 아닌 실제 객체 타이블 기준으로 실행된다.

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
            System.out.println("bird fly);
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

        ppublic void set(T value){
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


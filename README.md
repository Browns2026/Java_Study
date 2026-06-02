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

1. 클래스와 객체 (Class and Object)
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

- 객체(Object)는 클래스로부터 실제로 만들어진 대상이다.

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

2. 생성자
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

3. this
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

4. Static

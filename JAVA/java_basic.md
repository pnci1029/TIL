
`단일 책임 원칙(SRP)`
````
    - 하나의 클래스는 단 한 가지의 변경 이유만을 가져야 한다.
        => 변경이유 = 책임
        
    - 객체가 가진 공개 메서드, 필드, 상수 등은 
    해당 객체의 단일책임에 의해서만 변경되는가?
    
    - 관심사의 분리
    
    -높은 응집도, 낮은 결합도
````
<br />
<br />


## 클래스와 객체
`클래스를 왜 사용하는가?`
```
  case 1. 각각의 변수로 사용 -> 학생이 늘어나는 만큼 코드수가 기하급수적으로 늘어난다..
    String stu1Name = "학생1";
    int stu1Age = 18;
    int stu1Grade = 90;

    String stu2Name = "학생2";
    int stu2Age = 18;
    int stu2Grade = 100;

    System.out.println("이름 : "+ stu1Name+" 나이 : "+stu1Age+" 성적 : "+stu1Grade);
    System.out.println("이름 : "+ stu2Name+" 나이 : "+stu2Age+" 성적 : "+stu2Grade);

  case 2. 배열에 담아 사용 -> 각 변수보다는 낫지만 수정이나 시 정확한 인덱스에 수정/삭제되어야함
    String[] stuNames = {"학생1", "학생2"};
    int[] stuAges = {18, 18};
    int[] stuGrades = {90, 100};

    for (int i = 0; i < stuNames.length; i++) {
        System.out.println("이름 : "+ stuNames[i]+" 나이 : "+stuAges[i]+" 성적 : "+stuGrades[i]);
        }

  -> 여러 속성들을 통칭할 수 있는 개념(클래스) 도입

        Student student1 = new Student();
        student1.name = "학생1";
        student1.age = 17;
        student1.grade = 90;

        Student student2 = new Student();
        student2.name = "학생1";
        student2.age = 17;
        student2.grade = 90;
```
#  
`클래스와 객체와 인스턴스`
```
ex) Student student1 = new Student();

  클래스
  사용자가 직접 정의하는 사용자가 정의한 설계도를 클래스라고한다.

  객체
  클래스를 사용하여 메모리에 올라간 실체를 객체 또는 인스턴스 라고 한다.

  인스턴스
  특정 클래스로부터 생성된 객체를 의미.
  객체와 인스턴스는 자주 혼용되는데,
  인스턴스는 주로 객체가 어떤 클래스에 속해 있는지 강조할 때 사용된다.

  예를들어 student1 객체는 Student클래스의 인스턴스다 라고 표현

  * 그러나 둘 다 같은 클래스에서 나온 실체라는 핵심의미가 같기 때문에
  보통 둘을 구분하지 않고 사용한다.
```
`객체 생성 과정`
```
  1. 객체 생성(메모리 할당)
  2. 참조값 반환(메모리 어딘가에 생성된 객체에 접근할 수 있는 참조값 반환)
    Student student1 = new Student();
  3. student1 변수는 메모리의 참조값을 가지고 있다.
    따라서 이 변수(student1)를 통해 객체에 접근

  * 참조값을 객체에 보관하는 이유
    - 객체를 생성하는 new Student(); 코드 자체에는 아무 이름이 없다.
      반환되는 참조값을 생성하는 변수에 담음으로써 실제 메모리에 접근할 수 있다.

```
#  
#  
## 기본형과 참조형
```
  변수의 데이터 타입 가장 크게 보면 기본형과 참조형으로 분리 가능하다.

  사용하는 값을 변수에 직접 넣을 수 있는 기본형,
  그리고 객체가 저장된 메모리 위치를 가르키는 참조값을 넣을 수 있는 참조형이 있다.

  기본형을 재외한 나머지는 모두 참조형이다.
```
`기본형`
  - int, long, double, boolean 처럼 변수에 직접 넣을 수 있는 데이터 타입
  - 실제 사용하는 값을 변수에 담기 때문에 값을 바로 사용 가능
  - 바로 사용 가능하기 때문에 그대로 계산이 가능하다.(숫자)
#  
`참조형`
  - 객체와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입
  - 객체나 배열에 사용
  - 객체는 .을 통해서 메모리 상에 생성된 객체를 찾아서 사용
  - 배열은 []를 통해 메모리 상에 생성된 배열을 찾아서 사용
#  
```
  메서드 호출 시 기본형인지 참조형인지에 따라 동작이 달라진다.

  기본형일 경우 파라미터로 받는 값이 그대로 넘어온다.
  메서드 내부에서 파라미터 값이 변하더라도 호출자의 값에는 영향이 없다.

  참조형일 경우 참조값이 복사되어 전달됨으로
  전달된 객체의 멤버변수가 변할 경우 호출자의 객체의 멤버변수 값도 변한다.
```
#  
## 자바 메모리 구조
```
  1. 메서드 영역 : 프로그램을 실행하는데 필요한 공통 데이터 관리
    - 이 영역은 프로그램 모든 영역에서 사용
    - 클래스 정보(바이트 코드), 필드, 메서드, 생성자 등 보관
    - static 영역 : 스태틱 변수 보관
    - 런타임 상수 풀 : 프로그램을 실행하는데 필요한 공통 리터럴 상수 보관



  2. 스택 영역 : 실제 프로그램이 실행되는 영역.
    - 자바 실행 시 하나의 실행 스택이 생성됨(main() args)
    - 각 스택 프레임은 지역변수, 중간 연산 결과, 메서드 호출 정보 보관
    - 메소드를 실행할때마다 하나씩 쌓임
    - 스택 영역은 스레드 별로 하나의 실행 스택이 생성된다.
    - 즉 스레드 수 만큼 스택 영역이 생성됨


  3. 힙 영역 : 객체(인스턴스) + 배열이 생성되는 영역
    - 가비지 컬렉션이 이루어지는 영역
    - 더이상 참조되지 않는 객체는 GC에 의해 제거됨
  

```
#  
## static
`static 변수의 종류`
```
  인스턴스 변수 : static 이 붙지 않은 변수
    - static이 붙지 않은 변수는 인스턴스를 생성해야 사용할 수 있고, 인스턴스에 소속되어 있다.
      따라서 인스턴스 변수라 한다.

  클래스 변수 : static 이 붙은 변수
    - 클래스 변수, 정적변수, staitc변수 등으로 부른다.
    - static이 붙은 멤버 변수는 인스턴스와 무관하게 클래스에서 바로 사용할 수 있다
    - 클래스 변수는 자바 프로그램을 시작할 때 딱 1개가 만들어진다.
```
#  
`변수와 생명주기`
```
  1. 지역변수 : 스택 영역에 있는 스택 프레임안에 보관된다.
    메서드가 종료되면 스택 프레임도 제거되는데 이때 해당 지역 변수도 함께 제거된다.
    따라서 지역변수는 생존 주기가 짧다.

  2. 인스턴스 변수 : 인스턴스에 있는 멤버 변수를 인스턴스 변수라고 한다.
    인스턴스 변수는 힙 영역을 사용하는데, GC가 발생하기 전까지 생존하기 떄문에 지역변수보다 생존주기가 길다.

  3. 클래스 변수 : 메서드 영역의 static 영역에 보관되는 변수이다.
    메서드 영역은 프로그램 전체에서 사용하는 공용 공간이고
    클래스 변수는 JVM에 로딩 되는 순간 생성되고 JVM이 종료될때까지 생명주기가 이어진다.
```
#  
#  
`static 메소드의 종류`
```
  * static이 붙은 메서드는 객체 생성 없이 클래스명.메서드명으로 호출이 가능하다.
  정적 메서드 덕분에 불필요한 객체 생성 없이 편리하게 메서드를 사용 할 수 있다.

  1. 클래스 메서드
   - 메서드 앞에 static을 붙인 메서드로 인스턴스 생성 없이 클래스에서 바로 메서드를 호출이 가능하다.

  2. 인스턴스 메서드
    - static이 붙지 않은 메서드는 인스턴스를 생성해야 호출할 수 있다.
```
#  
`주의사항`
```
  package static2;

public class DecoData {
    private int instanceValue;
    private static int staticValue;

    public static void staticCall() {
//        instancevalue++;       compile error
//        instanceMethod();      compile error
        
        staticMethod();
        staticValue++;
    }

    public void instanceMethod() {
        System.out.println("instanceValue = " + instanceValue);
    }

    public static void staticMethod() {
        System.out.println("staticValue = " + staticValue);
    }

  *
  정적(static) 메서드에서 인스턴스 변수나 메서드를 호출할 수 없다.
  정적메서드나 변수는 JVM실행시에 메모리에 값이 할당되기 때문에 사용이 가능하나,

  인스턴스 변수나 메서드는 인스턴스 객체가 생성되지 않았기 떄문에 참조값이 만들어지지 않은 상태이다.
  따라서 정적 메서드에서 사용이 불가능하다.

}

```








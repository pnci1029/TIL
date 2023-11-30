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
`클래스와 객체`
```
  사용자가 직접 정의하는 사용자가 정의한 설계도를 클래스라고한다.

  클래스를 사용하여 메모리에 올라간 실체를 객체 또는 인스턴스 라고 한다.
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


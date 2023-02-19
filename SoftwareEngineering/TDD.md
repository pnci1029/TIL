# TDD 이전의 개발
  1. 만들 기능에 대해 설계하고 고민한다.
  2. 어떤 클래스, 인터페이스를 도출할지 고민하고, 어떤 타입에 어떤 메소드를 넣을지 생각한다.
  3. 1번, 2번을 수행하며 구현에 ㄷ대해 고민한다. 어떻게 구현할지 생각하며 코드를 작성한다.
  4. 3번을 완료한것같으면 테스트를한다.
  5. 4번을 토대로 동작하지않거나 문제가 발생했을 때 디버깅을 하며 원인을 찾는다.
  ```
  문제점
  1. 3번에 작성한 코드의 내용이 많아졌을 때 디버깅하는 시간이 더 오래걸릴 수 있음.
  2. 최초 코드 작성자와 테스트하는 개발자가 달라지는 문제가 발생 가능
  3. 테스트 시 톰캣 재실행...
  ```  
#  
#
# Tdd ?
  - 오직 자동화된 테스트가 실패하 경우에만 새로운 코드 작성
  - 중복을 제거
  - 신속한 리팩토링
## 작성 순서
  - Red - 반드시 실패하는 작은 테스트 작성 (컴파일 오류가 날 수 있음)
  - Green - 반드시 성공하는 테스트 작성 (어떤 죄악을 저질러도 상관없다.)
  - Refactoring - 테스트를 통과하는 조건 하에 반복 제거
 
#  
#
## ex) 암호 검사기
  - 길이가 8자 이상
  - 0~9 숫자를 포함
  - 대문자 포함
  - 3가지 규칙을 모두 충족하면 강함
  - 2가지 규칙을 충족하면 보통
  - 1개 이하는 약함. 
#. 
### 첫번째 테스트는 가장 예외적이거나 쉬운게 좋다. -> 모든 경우를 통과한 경우
### 두번째 길이를 제외한 조건 2개를 만족하는 경우 -> 보통출력
### 세번째 숫자를 포함하는 조건을 제외한 나머지 조건을 만족하는 경우 -> 보통출력
### 메소드와 테스트코드 리팩토링
### 발생할수있는 예외처리 -> null값, 빈값 처리 -> Invalid
### 네번째 대문자를 포함하는 조건을 제외한 나머지 조건을 만족하는 경우 -> 보통출력


모든 조건을 충족한 경우 → Strong

@SpringBootTest
public class PasswordStrengthTest {
  @DisplayName("모든 경우가 통과하는 케이스_Strong")
    @Test
    void allConditionPassed() {
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter =  Passwordpassword.meter("Abc1234!@#");
      Assertions.assertEquals(meter, PasswordStrength.STRENGTH)
    }
}



public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){
    return PasswordStrength.STRONG;
  }
}



public enum PasswordStrength {
    STRONG
}





1.2 테스트 코드 하나 더 추가

@SpringBootTest
public class PasswordStrengthTest {
  @DisplayName("모든 경우가 통과하는 케이스_Strong")
    @Test
    void allConditionPassed() {
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter1 =  Passwordpassword.meter("Abc1234!@#");
      
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter2 =  Passwordpassword.meter("CC12345!@#");
      
      Assertions.assertEquals(meter1, PasswordStrength.STRONG)
      Assertions.assertEquals(meter2, PasswordStrength.STRONG)
    }
}





길이를 제외한 조건 충족 → Normal

    @DisplayName("길이를 제외한 조건을 충족한 경우_Normal")
    @Test
    void meetOtherConditionWithOutLength() {
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter1 =  Passwordpassword.meter("Ab34!@#");
      
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter2 =  Passwordpassword.meter("CCa34#");
      
      Assertions.assertEquals(meter1, PasswordStrength.NORMAL)
      Assertions.assertEquals(meter2, PasswordStrength.NORMAL)
    }
}



public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){
    if (s.length() < 8) {
      return PasswordStrength.NORMAL;
    }
    return PasswordStrength.STRONG;
  }
}



public enum PasswordStrength {
    STRONG, NORMAL
}





숫자 포함 조건만 충족하지 못한 경우 → Normal

@DisplayName("숫자 포함을 제외한 조건을 충족한 경우_Normal")
    @Test
    void meetOtherConditionWithOutContainNumber() {
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter1 =  Passwordpassword.meter("ABCDEF!@#");
      
      PasswordStrengthMeter password = new PasswordStrengthMeter();
      PasswordStrength meter2 =  Passwordpassword.meter("!@#$ABCdcd");
      
      Assertions.assertEquals(meter1, PasswordStrength.NORMAL)
      Assertions.assertEquals(meter2, PasswordStrength.NORMAL)
    }
}



public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){
    if (s.length() < 8) {
      return PasswordStrength.NORMAL;
    }
    boolean isContainsNumb = false;
    char[] values = s.toCharArray();
    for(char value : values){
      if(value>='0' && value<='9'){
        isContainsNumb = true;
      }
    }
    if(!isContainsNumb) return PasswordStrength.NORMAL;
    return PasswordStrength.STRONG;
  }
}



3.2 서비스 로직 리팩토링

public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){
    if (s.length() < 8) {
      return PasswordStrength.NORMAL;
    }
    
    boolean isContainsNumb = containingNumberCondition(s);
    if(!isContainsNumb) return PasswordStrength.NORMAL;
    
    return PasswordStrength.STRONG;
  }
}

private boolean containingNumberCondition(String s) {
    char[] chars = s.toCharArray();
    for (char value : chars) {
        if (value >= '0' && value <= '9') {
            return true;
        }
    }
    return false;
}



4. 테스트 코드 리팩토링





5. 예외 발생(null, ““) → INVALID

@SpringBootTest
public class PasswordStrengthTest {
    PasswordStrengthMeter password = new PasswordStrengthMeter();

    @DisplayName("모든 경우가 통과하는 케이스_Strong")
    @Test
    void allConditionPassed() {
        assertStrength("Abc1234!@#",PasswordStrength.STRONG);
        assertStrength("CC12345!@#", PasswordStrength.STRONG);
    }

    @DisplayName("길이를 제외한 조건을 충족한 경우_Normal")
    @Test
    void meetOtherConditionWithOutLength() {
        assertStrength("Abc123!", PasswordStrength.NORMAL);
        assertStrength("A@B!c12", PasswordStrength.NORMAL);
    }

    @DisplayName("숫자 포함을 제외한 조건을 충족한 경우_Normal")
    @Test
    void meetOtherConditionWithOutContainNumber() {
        assertStrength("ABCDEF!@#",PasswordStrength.NORMAL);
        assertStrength("!@#$ABCdcd",PasswordStrength.NORMAL);
    }

    @DisplayName("값이 없는 경우_Invalid")
    @Test
    void meetInvalidCondition() {
        assertStrength(null, PasswordStrength.INVALID);
        assertStrength("", PasswordStrength.INVALID);
    }
    
    /**
     * 메소드 추출
     */
    private void assertStrength(String s, PasswordStrength passwordStrength) {
        PasswordStrength meter = password.meter(s);
        assertEquals(meter, passwordStrength);
    }



public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){

    if (s.length() < 8) {
      return PasswordStrength.NORMAL;
    }
    
    boolean isContainsNumb = containingNumberCondition(s);
    if(!isContainsNumb) return PasswordStrength.NORMAL;
    
    return PasswordStrength.STRONG;
  }
}

private boolean containingNumberCondition(String s) {
    char[] chars = s.toCharArray();
    for (char value : chars) {
        if (value >= '0' && value <= '9') {
            return true;
        }
    }
    return false;
}



6. 대문자 포함 조건 실패 → Normal

    @DisplayName("대문자 포함 조건을 제외한 조건을 충족한 경우_Normal")
    @Test
    void meetOtherConditionWithOutUpperLetter() {
        assertStrength("abcd1234!@",PasswordStrength.NORMAL);
        assertStrength("122dfg!@",PasswordStrength.NORMAL);
    }




public class PasswordStrengthMeter{
  public PasswordStrength meter(String s){

    if (s.length() < 8) {
      return PasswordStrength.NORMAL;
    }
    
    boolean isContainsNumb = containingNumberCondition(s);
    if(!isContainsNumb) return PasswordStrength.NORMAL;
    
    boolean isContainsUpperCase = containingUpperLetterCondition(s);
    if(!isContainsUpperCase) return PasswordStrength.NORMAL;
    
    return PasswordStrength.STRONG;
  }
}

private boolean containingNumberCondition(String s) {
    char[] chars = s.toCharArray();
    for (char value : chars) {
        if (value >= '0' && value <= '9') {
            return true;
        }
    }
    return false;
}

private boolean containingUpperLetterCondition(String s) {
    char[] chars = s.toCharArray();
    for (char value : chars) {
        if (value >= 'A' && value <= 'Z') {
              return true;
        }
    }
    return false;
}





7. 세 가지 경우 중 한가지만 통과한 경우 + 하나도 충족하지 못한 경우


public class PasswordStrengthMeter {
    public PasswordStrength meter(String s) {
        if (s == null || s.isEmpty()) {
            return PasswordStrength.INVALID;
        }
        int conditionCount = 0;

        if(lengthCondition(s))  conditionCount++;
        if(containingNumberCondition(s)) conditionCount++;
        if(containingUpperLetterCondition(s)) conditionCount++;

        if (conditionCount <= 1) {
            return PasswordStrength.WEAK;
        } else if (conditionCount == 2) {
            return PasswordStrength.NORMAL;
        }
        return PasswordStrength.STRONG;
    }

    private boolean lengthCondition(String s) {
        if (s.length() >= 8) {
            return true;
        }
        return false;
    }
    private boolean containingNumberCondition(String s) {
        char[] chars = s.toCharArray();
        for (char value : chars) {
            if (value >= '0' && value <= '9') {
                return true;
            }
        }
        return false;
    }

    private boolean containingUpperLetterCondition(String s) {
        char[] chars = s.toCharArray();
        for (char value : chars) {
            if (value >= 'A' && value <= 'Z') {
                 return true;
            }
        }
        return false;
    }
}






작성 순서

모든 규칙 통과 → 강함

한 가지 규칙 실패 → 보통

 한 가지 규칙 통과 → 약함
#  
# 
 

정해진 값 리턴

상수로 리턴

다양한 상수를 추가하며 구현을 일반화
#  
# 
## 유의점
  - 필요한 만큼만 설계
    - 비밀번호 강도 enum 클래스 생성 시 Week, Normal, Strong 모두 만들지 않고, 전체 충족하는 경우 Strong 먼저 생성 후 나머지 후 설계
  - 직관적인 이름
    - 구현하는 기능을 명확하게 인지할 수 있는 이름 설계가 중요
#  
#  
#  
#  
# Junit을 활용한 테스트코드
### 테스트 라이프 사이클
  1. 테스트메서드를 포함한 테스트 객체 생성
  2. (존재 시)@BeforeEach 어노테이션이 붙은 메소드 실행
  3. @Test 어노테이션이 붙은 메서들 실행
  4. (존재 시)@AfterEach 어노테이션이 붙은 메소드 실행
#  
#  
## 단위테스트 이해?
  ```
  단위테스트는 다른 단위테스트와 독립적이야한다.
  프레임워크에서 각각의 단위테스트 실패여부를 확인 가능해야한다.
  어떤 단위테스트를 실행할지 판단이 쉬워야한다.
  ```

#  
#  
## 대역을 활용한 테스트
### 대역을 이용하는 이유?
  - 테스트 대상이 외부 Http 서버와 통신이 필요한 경우
  - 테스트 대상에서 File 시스템을 사용하는 경우
  - 테스트 대상이 db를 조회하거나 db 테이블을 추가하는 등 db 접근이 필요한 경우
### 대역의 종류
  - Mock / Stub/ Fake / Spy








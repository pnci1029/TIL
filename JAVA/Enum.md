## ENUM
  ```
    enum은 자바뿐 아니라 C++, C#과 같은 다른 프로그래밍 언어에서도 사용한다
    자바에서는 클래스 형태로 다양하게 사용이 가능하다.
  ```
#  
#### Q. 남자는 1, 여자는 0으로 값이 들어올 때 생년월일을 보고 남자는 1 or 3 여자는 2 or 4로 db에 처리
  ```
  public enum Gender {
    MALE("1", "3"),
    FEMALE("0", "2");

    private final String code; // db에 저장될 값
    private final String anotherCode; // db에 저장될 값

    Gender(String code, String anotherCode) {
        this.code = code;
        this.anotherCode = anotherCode;
    }

    public String getCode(boolean isMale) {
        return isMale ? code : anotherCode;
    }
}
  ```
  #  
  ```
  String genderCodeFromApi = "1"; // 외부 API로부터 받은 성별 값
  boolean isMale = genderCodeFromApi.equals("1"); // 1이면 남자, 0이면 여자

  Gender gender = isMale ? Gender.MALE : Gender.FEMALE;
  String genderCodeForDb = gender.getCode(isMale);
  ```
  #  
  ```
    @Test
    void genderTest() {
        String genderMaleFromApi = "1";
        String genderFemaleFromApi = "0";
        boolean isMale = genderMaleFromApi.equals("1");
        boolean isFemale = genderFemaleFromApi.equals("0");

        Gender genderMale = isMale ? Gender.MALE
                : Gender.FEMALE;
        Gender genderFemale = isFemale ? Gender.FEMALE : Gender.MALE;

        Assertions.assertThat(genderMale.getCode(isMale)).isEqualTo("1");
        Assertions.assertThat(genderFemale.getCode(isFemale)).isEqualTo("2");

    }
  ```
  

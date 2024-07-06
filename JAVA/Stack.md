`자바에서의 스택`
```
void main(String [] args){
  int x = 1;
  int y = 2;

  int result = sum(x, y);

}

int sum (int a, int b){
  int s = a + b;
  return s;
}
```


<br />


```
  스레드가 메소드에 들어가면
  스택 위 공간을 메소드에 맞게 생성함

  이 공간을 스택 프레임이라고 한다.


  메소드 인수는 메소드 프레임에 있는 스택에 푸시된다.
  stack [
    args [
      b = 2;       // 현재 메소드가 다른 메소드를 호출해야하면
      a = 1;       //스택 프레임은 새로운 스택프레임이 상단에 할당됨



      y = 2;       // 순서대로 스택에 푸시됨
      x =1;
  ],  ...

]
```


<br />

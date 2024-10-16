


# Java


## VM 과 메모리 구조

- 힙과 메서드 영역
- VM 스택
- 네이티브 
- pc 레지스터



## GC

GC root 개념

C 의 그림자인 finalizer()

## 도구

JDK imbedded
- jps
- jconsole
- javac

Ecosystem
- gradle
- jmeter
- jfr

## 유용한 지식들

### split() vs. StringTokenizer

타겟이 아주 짧고 delimeter 가 유니코드가 아니라면 StringTokenizer 가 조금 더 빠르다.

그 외엔 split() 이 안정적 성능을 보여준다.

### NPE 방어적 코드

1. 출신이 확실하지 않은 객체의 메서드를 쓰는걸 피하기
2. StringUtils 같은 라이브러리 사용
3. Optional 사용

### 스트림과 Side effect

자바에서 스트림은 보통 두가지
1. streaming (갯수가 정의되지 않은 콜렉션 비슷한 것.)
2. stream api 를 유한한 콜렉션에 쓰는 것.

첫 번째는 reactor 에서 사용하는 모노 플럭스. (~함수형 프로그래밍)
소스, 싱크 개념.

두 번째도 함수형 프로그래밍인데, 갯수가 정해져 있는 경우에도 쓰는 경우.

대체로 스트림 API 사용하면 보기도 편하고 좋긴 한데, side effect 가 금지되어 있는 점만 주의하면 됨.

Side effect 를 주고 싶으면 스트림 안으로 끌어들이던지, for 문으로 고쳐쓰던지 하면 된다.

### 비동기 프로그래밍

스프링 프레임워크에선 @Async 를 void 리턴하는 메서드에 달아서 딸깍 만들지만, js 에서 하듯 Future 를 사용해야 할 일이 생길 수 있다고 봄.

스레드를 하나하나 관리하지 않아도 되니 @Async 는 좋은 어노테이션이긴 하다. 그래도 프레임워크 도움 없이는 어떻게 구현하는진 기억해 두고 있어야 함.








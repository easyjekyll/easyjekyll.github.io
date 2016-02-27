---
layout: post
title: JAVA Interface와 AutoWired annotation에 대해서
tags: Interface AutoWired DI Spring 의존성 주입
---


웹프로그램을 개발 하면서 Interface를 이용 하고 구현체를 주입하는 과정이 너무나 불필요 하게 느껴졌다. 
이미 나는 원하는 결과가 있고, 내가 원하는 클래스를 초기화 하면 되는것 아닌가? 하는 생각이 지배적 일뿐, 확장성을 고려 한다거나 관심사를 분리해야 한다는 생각 까지는 미치지 못했기 때문이다.
이번 포스팅을 통해 Interface 의 특징들과 중요성을 확인 해 보자.



### Inteface 의 메커니즘 ###
설명 조차도 너무나 추상적인 Interface 의 특징 들을 알아보자
1. 구현된 메소드는 올 수 없고 추상 메소드만 정의할 수 있다.
2. 상속을 받은 일반 클래스는 interface의 추상메서드 전체를 모두 재정의 해 주어야 한다.
3. 일반 클래스는 여러 interface를 다중 상속 할 수 있다.




### Interface 의 확장성 ###
먼저 흔히 볼수 있는 Interface 사용 예제를 보자.

```java
//Map Interface 에 HashMap 구현체를 주입
Map map1 = new HashMap();
map1.put("a","a");
map1.put("b","b");

// Map Interface 에 LinkedHashMap 구현체를 주입
Map map2 = new LinkedHashMap();
map2.put("a","a");
map2.put("b","b");

System.out.println(map1.toString());    // {b=b, a=a}
System.out.println(map2.toString());    // {a=a, b=b} 위 map1 과는 상반된 결과.
```

Map Interface를 어떻게 초기화 하느냐에 따라 서로 상반된 결과를 볼수 있다. 
처음에 HashMap을 이용하여 개발 했더라도, 추후 put() 한 순서대로 정렬된 출력을 원한다면 LinkeHashMap 으로 구현체를 변경하면 된다.
또한 구현체가 변경이 되었더라도 그 이하에서 사용된 .put() .get() 등 구현체의 메소드는 정상적으로 작동 할 것이다.
Interface를 상속받는 모든 구현체는 반드시 Interface에서 작성된 모든 추상 method를 모두 구현해야만 하는 특징 덕분에 어떤 구현체든 동일한 메소드가 존재 하기 때문이다.

### Interface 를 이용한 관심사 분리 ###

웹프로그램에서 Controller.java 를 작성할 때 Service.java 가 어떤 일을 하는지는 관심 밖이다. 다음과 같이 Controller 내에서 User List 객체를 초기화 하는 과정이 있다.
###### 클래스 초기화 방법을 통한 객체 생성 방법 ######

```java
Service(클래스명) service = new Service();
List<User> list = service.getUserList();
```
Controller 제작자는 service로부터 그저 `List<User>` 타입의 객체를 잘 반환 해 주기를 기대 할 뿐이고, getUserList가 DB처리를 하고 어떻게 가공 하는지 알고싶지 않다. 그것은 service 개발자의 몫일뿐... (공감하기 어렵다면 역할의 분리에 촛점을 맞추고 바라보자. )
Service.java 를 만들어 놓고 getUserList() 메소드에 return null 해 둬도 일단 빌드 하는데 문제는 없겠지만 날코딩 해놨다는 찜찜한 느낌을 지울수가 없다. 이러한 상황에 대처 하라고 JAVA에서 제공 하는 것이 Interface 이고, 이를 중간에 두어 분리하는 것이다.

###### 인터페이스를 통한 객체 주입 방법 ######

```java
Service(인터페이스) service = new ServiceImpl();
List<User> list = service.getUserList();
```

이렇게 해두면, ServiceImpl을 작성 하는 개발자에게 Service Interface만 제공을 하면 되고, 이때 소스상 명시적으로 '내가 getUserList() 를 호출 할 테니 알아서 List<User> 타입의 Object를 반화하는 구현체를 만들어 달라' 는 약속을 하게 되는 것과 같다. (Interface의 특징 2번)
하지만 이것도 사용자 입장 에서는 new ServiceImpl() 이라던지, new OnotherServiceImpl() 이라던지.. 구현체 클래스 이름을 정확히 알고 있어야만 코딩을 할 수 있다는 단점이 있다.

###### 완전한 분리, @AutoWired ######
위 단점인, Interface를 어떤 구현체로 초기화 해줄지 결정하지 않아도 되기 위해 [팩토리 패턴](http://warmz.tistory.com/entry/Abstract-Factory-Pattern-%EC%B6%94%EC%83%81-%ED%8C%A9%ED%86%A0%EB%A6%AC-%ED%8C%A8%ED%84%B4) 이란것이 존재한다.
팩토리패턴.. 보고 이해하고 있노라면 현기증이 난다.
나같은 사람을 위해서 만들어진 것이 @AutoWired 어노테이션 이다.
팩토리 패턴을 왜 써야하는지. 그리고 내부적으로 어떻게 작동 하는지 몰라도 되게끔 만들어 주기 때문이다.
아래 소스를 보면 어떠한 구현체를 초기화 하지 않고도 instance 변수를 선언 해 놓으면 알아서 service 변수에 구현체가 담긴 클래스가 주입이 된다.

```java
@AutoWired
Service(인터페이스) service;  // ApplicationContext 가 @Service 를 찾아서 갖고있다가 적절히 주입시켜줌 
// ...
List<User> list = service.getUserList(); // error따위 나지 않는다.
```


이렇게 하여 확장성이 높고, 관심사가 분리된, 조금 더 객체지향적인 소스가 완성 되었다.


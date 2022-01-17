---
title: "Composite Pattern"
excerpt_separator: "<!--more-->"
categories:
  - Patterns
tags:
  - Composite Pattern
---

***Composite Pattern***  
# 정의
>컴포지트 패턴(Composite pattern)이란 객체들의 관계를 트리 구조로 구성하여 부분-전체 계층을 표현하는 패턴으로,
>사용자가 단일 객체와 복합 객체 모두 동일하게 다루도록 한다.


## Composite Pattern UML
![image](\assets\image\composite_pattern_uml.png)

**Component**  
 - 모든 component 들을 위한 추상화된 개념으로써, "Leaf" 와 "Composite" 클래스의 인터페이스이다.  

**Leaf**  
 - "Component" 인터페이스를 구현하고, 구체 클래스를 나타낸다.  

**Composite**  
 - "Component"  인터페이스를 구현하고, 구현되는 자식(Leaf or Composite) 들을 가지고, 이러한 자식들을 관리하기 위한 메소드(addChild, removeChild...)를 구현한다.  
   또한, 일반적으로 인터페이스에 작성된 메소드는 자식에게 위임하는 처리를 한다.





## Composite Pattern Ex

### Component  ...  Animal
```java
/* Component */
public interface Animal {
    public void speak();
}
```

### Leaf  ...  Cat, Dog
```java
/* Leaf */
public class Cat implements Animal {
    @Override
    public void speak() {
        System.out.println("나는 야옹이");
    }
}

/* Leaf */
public class Dog implements Animal {
    @Override
    public void speak() {
        System.out.println("나는 강아지");
    }
}
```

### Composite   ...   AnimalGroup
```java
/* Composite */
public class AnimalGroup implements Animal {
    private List<Animal> animalGroup = new ArrayList<Animal>();

    public void add(Animal animal) {
        animalGroup.add(animal);
    }

    public void speak() {
        for (Animal animal : animalGroup) {
            animal.speak();
        }
    }
}
```


### 실행결과
```java
public class Main {
    public static void main(String[] args) {

        AnimalGroup cat_group = new AnimalGroup();
        cat_group.add(new Cat());
        cat_group.add(new Cat());
        cat_group.add(new Cat());

        AnimalGroup dog_group = new AnimalGroup();
        dog_group.add(new Dog());
        dog_group.add(new Dog());

        AnimalGroup zoo = new AnimalGroup();
        zoo.add(cat_group);
        zoo.add(dog_group);

        zoo.speak();
    }
}
```
![image](\assets\image\composite_pattern_result.png)




#### 출처  
   [https://mygumi.tistory.com/343](https://mygumi.tistory.com/343)  
   [https://ko.wikipedia.org/wiki/컴포지트_패턴](https://ko.wikipedia.org/wiki/컴포지트_패턴)  



<!--
줄바꿈       스페이스바를 두번 + Enter 해준다.
문법표시     마크다운 문법 앞에 \를 붙여준다.
링크        <링크주소>
이미지삽입   ![image](이미지주소)
헤더        # h1
            ## h2
            ### h3
            #### h4
            ##### h5
            ###### h6

굵게         **강조된 텍스트입니다**
기울기       *기울여진 텍스트입니다*
취소선       ~~취소된 텍스트입니다~~
밑줄        <u>밑줄 있는 텍스트입니다</u>
글씨색      <span style="color:yellow">노란 글씨입니다.</span>

```언어 이름(소문자)
이 부분에 코드 적기
```

체크박스    - [ ] 체크 안됨
            - [X] 체크 됨

-->

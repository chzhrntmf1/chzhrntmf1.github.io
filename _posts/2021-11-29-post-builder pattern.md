---
title: "Builder Pattern"
excerpt_separator: "<!--more-->"
categories:
  - Patterns
tags:
---

***빌더 패턴의 설계구조와 장단점을 이해하고 어떠한 문제에 대해 적용 가능한 패턴인지 공부한다.***<br>

<h5>1. 빌더 패턴(Builder Pattern) 이란</h5>
  > 복잡한 객체를 생성하는 클래스와 표현하는 클래스를 분리하여, 동일한 절차에서도 서로 다른 표현으로 이를 생성하는 방법을 제공하는 패턴<br>

  - 빌더 패턴은 인스턴스를 생성할 때 생성자를 통해서만 생성하는 방식에 어려움을 해결하고자 고안된 패턴이다. <br>
    객체에 많은 Optional한 멤버 변수(혹은 파라미터)나 지속성 없는 상태 값들에 대해 처리해야 하는 문제들을 해결할 수 있다고 한다. <br>
    간단하게 이해하자면, 빌더 패턴은 생성자에 파라미터가 많은 복잡한 객체를 생성할 때 사용하는 것이 좋다. <BR>
    **생성자에 파라미터가 너무 많다면, 어떤 파라미터가 어떤 값(의미)을 갖는지 알기 어렵기 때문이다.**
<br>


<br><br>


<h5>2. 빌더 패턴(Builder Pattern) Example Source Code</h5>
<h6>Buider Class</h6>
```java
public class PersonInfoBuilder {
    private final String name;
    private final int age;
    private final String favoriteColor;
    private final String favoriteAnimal;
    private final int favoriteNumber;

    public static class Builder {
        // Required parameters(필수 인자)
        private final String name;
        private final int age;

        // Optional parameters - initialized to default values(선택적 인자는 기본값으로 초기화)
        private String favoriteColor = '';
        private String favoriteAnimal = '';
        private int favoriteNumber = 0;

        public Builder(String name, int age) {
            this.name = name;
            this.age = age;
        }
        public Builder favoriteColor(String val) {
            favoriteColor = val;
            return this; // 이렇게 하면 . 으로 체인을 이어갈 수 있다.
        }
        public Builder favoriteAnimal(String val) {
            favoriteAnimal = val;
            return this;
        }
        public Builder favoriteNumber(int val) {
            favoriteNumber = val;
            return this;
        }
        public PersonInfoBuilder build() {
            return new PersonInfoBuilder(this);
        }
    }

    private PersonInfoBuilder(Builder builder) {
        name = builder.name;
        age = builder.age;
        favoriteColor = builder.favoriteColor;
        favoriteAnimal = builder.favoriteAnimal;
        favoriteNumber = builder.favoriteNumber;
    }

    public String getName() {
        return name;
    }
    ...
}
```
<br><br>
<h6>Main</h6>
```java
public class BuilderPattern {
    public static void main(String[] args) {
        // 빌더 객체에 원하는 데이터를 입력합니다. 순서는 상관 없습니다.
        PersonInfoBuilder personInfoBuilder = new PersonInfoBuilder
                .Builder("Hyeonwoo", 19)
                .favoriteColor("puppy")
                .favoriteColor("green")
                .favoriteNumber(7)
                .build();                 // 마지막에 .build() 메소드를 호출해서 최종적인 결과물을 만들어 반환합니다.
    }
}
```

<h5>3. 빌더 패턴의 장점</h5>
1. 가독성 향상<br>
   - 객체 생성에 필요한 파라미터의 의미를 코드 단에서 명확히 알 수 있다.<br>
2. 유연성을 확보할 수 있음<br>
   - 생성에 필요한 파라미터가 추가될 때 마다, 생성자 오버로딩을 안해도 된다.<br>
3. 불변객체<br>
   - 생성된 객체는 setter 메소드를 제공하지 않기 때문에 멤버 변수 값을 변경할 수 없다.<br>
<br><br>



<h5>4. 빌더 패턴은 왜 사용할까?</h5>
**빌더 패턴을 이해하고 나에게 와닿은 장점은 클린코드이다.**
![icon](/assets/image/Builder_pattern_ex.png)<br>
출처:[https://okky.kr/article/396206](https://okky.kr/article/396206)<br>


---
<h6>Todo..내가 더 생각해봐야 할 이야기들</h6>

‘GoF 디자인 패턴’에서 제시한 빌더 패턴과 ‘Effective Java’에서 제시한 빌더 패턴에 대한 갑론을박이 많다.<br>
‘GoF 디자인 패턴’에서 보다 깊은 빌더 패턴에 대한 이해를 얻을 수 있을 것 같다.<br>

빌더패턴은 소프트웨어 디자인 패턴 중 생성 패턴(Creational Pattern)에 속한다.<br>
생성패턴이란 인스턴스를 만드는 절차를 추상화하는 패턴으로, 객체의 생성과 조합을 캡슐화하여 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성 및 확장성을 제공한다.<BR>
앞서 공부한 싱글톤 패턴도 생성 패턴에 속함.<br>

팩토리 메서드 패턴(Factory Method Pattern)<br><br>


출처<br>

   [https://4z7l.github.io/2021/01/19/design_pattern_builder.html](https://4z7l.github.io/2021/01/19/design_pattern_builder.html)<br>
   [https://junhyunny.github.io/information/design-pattern/builder-pattern/](https://junhyunny.github.io/information/design-pattern/builder-pattern/)<br>
   [https://jdm.kr/blog/217](https://jdm.kr/blog/217)<br>  

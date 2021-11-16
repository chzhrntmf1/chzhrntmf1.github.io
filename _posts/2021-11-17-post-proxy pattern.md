---
title: "Proxy Pattern"
excerpt_separator: "<!--more-->"
categories:
  - Patterns
tags:
---


**프록시 패턴(Proxy Pattern) ?**
  > 어떤 객체에 대한 접근을 제어하기 위해 대리인이나 대변인에 해당하는 객체를 제공하는 패턴


**프록시 패턴의 클래스 다이어그램**<br>
![icon](/assets/image/proxy_pattern.png)

INode : Client에서 필요로 하는 기능을 명시 <br>
Node1, Node2 : 실제 작업을 처리하는 객체 <br>
NodeProxy : 실제 작업을 처리하는 객체 대한 레퍼런스를 가지고 있어 Client로 받은 요청을 전달 <br>




**프록시 패턴의 소스 예제**

  INode.java(인터페이스)
  ```java
  interface INode {
  	// 추상 메소드
  	void print();
  }
  ```
  Node1.java
  ```java
  // INode를 상속받은 Node1클래스
  class Node1 implements INode {
  	public void print() {
  		System.out.println("Node1 class");
  	}
  }
  ```
  Node2.java
  ```java
  // INode를 상속받은 Node2클래스
  class Node2 implements INode {
  	public void print() {
  		System.out.println("Node2 class");
  	}
  }
  ```

  NodeProxy.java(Proxy Pattern 클래스)
  ```java
  // Proxy 패턴 클래스
  class NodeProxy implements INode {
  	private INode node;
  	// 생성자 - 파라미터가 없으면 true
  	public NodeProxy() {
  		this(true);
  	}
  	// 생성자
  	public NodeProxy(boolean check) {
  		// 파라미터 check에 의해 생성되는 인스턴스가 다르다.
  		if (check) {
  			// Node1 인스턴스 생성
  			node = new Node1();
  		} else {
  			// Node2 인스턴스 생성
  			node = new Node2();
  		}
  	}
  	// 함수 재정의
  	public void print() {
  		// node 인스턴스의 print 함수 실행
  		node.print();
  	}
  }
  ```
  Program.java(실행 클래스)
  ```java
  // 실행 클래스
  class Program {
  	// 실행 함수
  	public static void main(String[] args) {
  		// 파라미터가 없는 NodeProxy 인스턴스 생성
  		INode node = new NodeProxy();
  		// print 함수 호출
  		node.print();
  		// 파라미터가 false인 NodeProxy 인스턴스 생성
  		node = new NodeProxy(false);
  		// print 함수 호출
  		node.print();
  	}
  }
  ```
  Result
  ```
  Node1 class
  Node2 class
  ```

Program 클래스에서 INode 인스턴스가 생성되는 과정을 살펴보면,<br>
Node1 클래스나 Node2 클래스에 직접 접근하지 않고 **NodeProxy에 의해 Node1 또는 Node2 인스턴스가 생성**된다.<br>
Node1 인스턴스를 생성하는지, Node2 인스턴스를 생성하는지 여부는 NodeProxy의 파라미터에 의해 결정된다.<br><br>


**프록시 패턴 장단점**
<br>
  장점
1. 사이즈가 큰 객체(ex : 이미지)가 로딩되기 전에도 프록시를 통해 참조를 할 수 있다.
2. 실제 객체의 public, protected 메소드들을 숨기고 인터페이스를 통해 노출시킬 수 있다.
3. 로컬에 있지 않고 떨어져 있는 객체를 사용할 수 있다.
4. 원래 객체의 접근에 대해서 사전처리를 할 수 있다.
<br><br>

  단점
1. 객체를 생성할때 한단계를 거치게 되므로, 빈번한 객체 생성이 필요한 경우 성능이 저하될 수 있다.
2. 프록시 내부에서 객체 생성을 위해 스레드가 생성, 동기화가 구현되야 하는 경우 성능이 저하될 수 있다.
3. 로직이 난해해져 가독성이 떨어질 수 있다.

<br><br><br><br><br><br>










추후 시간날 때..<br>
  프록시 패턴의 다양한 쓰임새
  - 원격 프록시 : 원격 객체에 대한 접근 제어가 가능합니다.
  - 가상 프록시 (Virtual Proxy) : 객체의 생성비용이 많이 들어 미리 생성하기 힘든 객체에 대한 접근 및 생성시점 등을 제어합니다.
  - 보호 프록시 (Protection Proxy) : 객체에 따른 접근 권한을 제어해야하는 객체에 대한 접근을 제어할 수 있습니다.
  - 방화벽 프록시 : 일련의 네트워크 자원에 대한 접근을 제어함으로써 주 객체를 '나쁜' 클라이언트들로부터 보호하는 역할을 합니다.
  - 스마트 레퍼런스 프록시 (Smart Reference Proxy) : 주 객체가 참조될 때마다 추가 행동을 제공합니다. ex) 객체 참조에 대한 선 작업, 후 작업 등
  - 캐싱 프록시 (Caching Proxy) : 비용이 많이 드는 작업의 결과를 임시로 저장 하고, 추후 여러 클라이언트에 저장된 결과를 실제 작업처리 대신 보여주고 자원을 절약하는 역할을 합니다.
  - 동기화 프록시 (Synchronization Proxy) : 여러 스레드에서 주 객체에 접근하는 경우에 안전하게 작업을 처리할 수 있게 해줍니다. 주로 분산 환경에서 일련의 객체에 대한 동기화 된 접근을 제어해주는 자바 스페이스에서 쓰입니다.
  - 복잡도 숨김 프록시 (Complexity Hiding Proxy) : 복잡한 클래스들의 집합에 대한 접근을 제어하고, 복잡도를 숨깁니다.
  - 지연 복사 프록시 (Copy-On-Write Proxy) : 클라이언트에서 필요로 할 때까지 객체가 복사되는 것을 지연시킴으로써 객체의 복사를 제어합니다. '변형된 가상 프록시'라고 할 수 있으며, Java 5 의 CopyOnWriteArrayList 에서 쓰입니다.


출처<br>
   [https://nowonbun.tistory.com/449](https://nowonbun.tistory.com/449)<br>
   [https://coding-factory.tistory.com/711](https://coding-factory.tistory.com/711)<br>
   [https://developside.tistory.com/80](https://developside.tistory.com/80)

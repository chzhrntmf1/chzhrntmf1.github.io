---
title: "Proxy Pattern"
excerpt_separator: "<!--more-->"
categories:
  - Patterns
tags:
---

**Proxy Pattern의 소스 예제**

```java
// 인터페이스
interface INode {
	// 추상 메소드
	void print();
}

// INode를 상속받은 Node1클래스
class Node1 implements INode {
	// 함수 재정의
	public void print() {
		// 콘솔 출력
		System.out.println("Node1 class");
	}
}

// INode를 상속받은 Node2클래스
class Node2 implements INode {
	// 함수 재정의
	public void print() {
		// 콘솔 출력
		System.out.println("Node2 class");
	}
}

// Proxy 패턴 클래스
class NodeProxy implements INode {
	// 맴버 변수
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
출처 [https://nowonbun.tistory.com/449](https://nowonbun.tistory.com/449)

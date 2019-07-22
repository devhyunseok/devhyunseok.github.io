---
layout: post
title: "명령형 패러다임 vs 선언적 패러다임"
author: Hyunseok
categories: Frontend
comments: true
---

원본: https://medium.com/front-end-weekly/imperative-versus-declarative-code-whats-the-difference-adc7dd6c8380

위 포스팅을 읽고 요점을 정리한 내용입니다.

### 명령적 패러다임
- 절차적, 객체지향 프로그래밍은 명령적 패러다임
- C, C++, C#, PHP, Java 같은.
- 프로그램의 상태를 변경하는 명령문을 작성.
- 하드웨어가 일하는 내용과 밀접한 관계가 있음.
- 조건문, 루프, 상속

<pre>
<code>
class Number {
  constructor (number = 0) {
    this.number = number;
  }
  
  add (x) {
    this.number = this.number + x;
  }
}
const myNumber = new Number (5);
myNumber.add (3);
console.log (myNumber.number); // 8
</code>
</pre>


### 선언적 패러다임
- 논리형, 함수형 도메인 특정 언어는 선언적 패러다임.
- 범용 프로그래밍 언어가 아닐 수 있음.
- 소프트웨어 흐름을 묘사하는것보다 소프트웨어 로직을 구축하는 것에 중점을 둠.
    - Ex) <img src="./image.jpg" />의 경우 브라우저에게 이미지를 표시하라고 말하지만, 어떻게 표시하는지는 정의하지 않음.
- 람다 계산법 기반
    - 상태, 사이드 이펙트, 변할수 있는 데이터를 피함.
- 명령문 대신 표현식을 작성
- 동일한 파라미터 입력 시, 항상 같은 값을 반환.

<pre>
<code>
const sum = a => b => a + b;
console.log (sum (5) (3)); // 8
</code>
</pre>

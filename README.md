auxiliary-utils
===============

# 목적
- 프로그램에 도움이 될 수 있는 유틸리티를 만든다.

Change Log
==========

## 1.0.0 (2014-12-18)

Features:
  - com.g0software.auxiliary.reflect 제작
  - `ReflectionUtil` : 객체 리플렉션을 통해 내부 Value 들을 보는 기능을 가진 유틸리티
  - `StackTraceUtil` : 현재 자리에서의 StackTrace 나 Method Call 을 한 Method 들을 보는 유틸리티


# Solution

## swe-hw-calculator 실행
* 콘솔로 입력받는 프로그램입니다
  1. Application Main Class 실행
  2. mvn package 후에 java -jar target/swe-hw-calculator.jar 실행

## Calculator 설명
> SpringBoot Framework 를 사용하여 작성하였습니다
> 이유는 입력방법에 대한 고민을 하다가 Web 또는 콘솔 아니면 GUI 로도 가장 빠르게 변환 할 수 있는 프레임워크라고 생각했습니다
> 또한 Spring DI 를 쉽게 사용할 수 있는 장점이 있다고 판단하였습니다 
> 
> Homework 은 Application 에서 CommandCalculator Bean 을 실행시키는 부분에서 시작합니다.
> CommandCalculator 는 Calculator 의 run 을 상속받아 콘솔에서 실행되도록 구현하였습니다.
> 
> CommandCalculator 에서는 문자변수를 치환하고 CalculateService 로 수식을 넘겨서 계산결과값을 받아옵니다.
> (문자변수 치환의 경우에는 위 Case2, 3 에서의 abcde 등 한개의 캐릭터가 한개의 숫자를 추가로 입력받는 것으로 이해하고 구현하였습니다)
 
> 계산식은 가장 보편적으로 사용되는 방법인 후위표현식으로 전환하여 계산하는 방법을 택했습니다
> CalculateService의 calculate 에서는 
1. 수식의 숫자, 부호, 괄호등을 정규식으로 나누기
2. 수식의 문법이 적법한지 판별하기
3. 중위표현식으로 나뉘어진 수식을 후위표현식으로 변환하기 (Stack, LinkedList 사용)
4. 우선순위에 맞추어 계산하기
> 와 같은 순서로 계산되어집니다.

> 추가적으로 수식표현개체는 Expression enum 으로 패턴구분 타입구분 및 우선순위에 대한 부분을 판별 합니다.
> Stack, LinkedList 에서 사용하기 위해서 Node 로 실제 Value 와 Expression 을 가진 구조체를 만들었습니다.

또한 계산 부분에 있어서는 CalculateService 에 집중될 수 있는 무거운 로직을 줄이기 위하여,
계산로직을 제외한 validation check, stack, list 만들기 등이 작업을 CalculatorOperator 에서 처리하도록 하였으며,
유틸리티성 메소드를 가지고 있는 CalculatorUtils 를 구현하였습니다

## Package 설명 
표준 Maven 디렉토리 구조를 가지고 있습니다
src-main-java : Main Java 코드가 위치한 디렉토리
src-main-test : Test 코드가 위치한 디렉토리 

com.riotgames.recruit.calculator : Spring Boot Application 이 위치한 상위 패키지
com.riotgames.recruit.calculator.application : UI (App) 가 위치한 패키지
com.riotgames.recruit.calculator.exception : 예외사항 패키지
com.riotgames.recruit.calculator.expression : 숫자 부호 괄호등 수식의 메타 정보를 가지고 있는 클래스가 위치한 패키지
com.riotgames.recruit.calculator.structure : 계산기의 구조체 관련된 클래스가 위치한 패키지 
com.riotgames.recruit.calculator.service : 비지니스 로직이 위치한 패키지
com.riotgames.recruit.calculator.utility : 유틸리티성 클래스가 위치한 패키지 


---

# Calculator
(), {} 를 허용하는 4측 연산 계산기를 구현하세요.

* +, -, *, /, ^ 연산 모두 적용됨. (^는 power 연산임.)
* 익히 알고 있는 4측 연산의 우선 순위가 적용됨.
* () < {} 상위 우선 순위를 가짐.
* 입력에 변수가 주어질 수 있으며, 해당 변수가 있는 경우에는 변수값을 추가로 입력받는다.
* 변수는 여러개가 존재할 수 있으며, 각 변수의 이름을 각자 입력받아야 한다.


## 입력 예제
* Case1: 4 + (8 + 1/8 * 8 + 1) / { 1 + {1 - 1}} - 0.001
* Case2: 1 + abc (이 경우 abc가 변수임.)
* Case3: 1 + abc + abcd + abcde (abc, abcd, abcde 모두 변수임.)

## 기본 조건
* 테스트 코드가 포함되어야 합니다.
* 테스트 코드를 통한 Coverage가 50% 이상이어야 합니다.
* 입력 형식은 자유 형식으로 사용할 수 있으나, 어떤 형식으로 입력받는지는 알 수 있어야 한다.






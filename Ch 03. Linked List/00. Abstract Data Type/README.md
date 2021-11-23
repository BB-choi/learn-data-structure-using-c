# 추상자료형 : Abstract Data Type

교재 윤성우의 열혈 자료구조와 같이, 자료구조에서의 추상자료형을 설명

## 자료구조에서의 추상 자료형 (ADT)

구체적인 기능의 완성과정을 언급하지 않고, 순수하게 기능이 무엇인지를 나열한 것

-   자료형의 정의

    💡 **구조체 정의**, 해당 구조체를 기반으로 한 **연산**(해당 구조체를 기반으로 제공할 수 있는 기능 관련 연산)의 종류를 결정하는 것까지 포함

    💡 즉, **자료형**의 정의에 **기능**(연산)과 관련된 내용을 명시할 수 있다.

### 예시

-   구조체 Wallet 과 Wallet의 ADT

    구조체 Wallet도 자료구조의 일종 (지갑이라는 데이터를 표현한 결과)

```
type def struct_wallet  // 동전 및 지폐 일부만을 대상으로 표현한 지갑
{
    int coin100Num;     // 100원짜리 동전의 수
    int bill5000Num;    // 5,000원짜리 지폐의 수
} Wallet;
```

```
// 기능을 명시
int TakeOutMoney(Wallet* pw, int coinNum, int billNum)
void PutMoney(Wallet* pw, int coinNum, int billNum)
```

## 리스트 자료구조의 학습 순서

[리스트 자료구조](../01.%20Array%20List/README.md)에 대한 학습순서

1. 리스트 자료구조의 **ADT 정의**
2. ADT를 근거로 리스트 자료구조를 활용하는 **main 함수** 정의
3. ADT를 근거로 **리스트 구현**

리스트 사용자에게 사용방법 이외의 불필요한 부분까지 알도록 하지 않는다는 본질을 위해 2 → 3의 순서로 진행한다.
---
layout: post
title:  "[MeetUp] 인프런 퇴근길 밋업 with KotlinConf 2023 후기"

categories: Kotlin
---

## 2023 Inflearn kotlinConf

<br>

오늘은 전에 신청해 두었던 인프런 퇴근길 밋업에 50명 중 당첨이 되어서

강의와 네트워킹을 다녀왔습니다.

이전 회사에서 코틀린을 이용한 백엔드 개발을 했지만

커리어에서는 굳이 고집할 필요가 있을까란 생각을 하게 되었습니다.

들은 내용을 정리하고, 공부해보며 언어에 대해 더 고민해봐야겠다고 생각했습니다.

<br>

***

<br>

~~밑의 내용은 다시 정리해야 됩니다~~

<br>

### Session 1. Kotlinconf is back!

- 기존 컴파일 속도가 느리다는 단점이 있다
    - K2 컴파일러가 새로 나올 것 → kotlin2.0과 같이
    - 프론트엔드 부분이 많이 개선 될 것
        - 백엔드는 어떤 차이가 있을지?
    - 2.0 버전 출시 이후 새로운 문법들이 나올 예정(아직 정확하게는 미정)
        - static extension → 이게 가장 의견이 많다
        - Explicit Fields → class 필드 설정 중 custom getter등을 field라는 키워드로 간단히 사용 가능
        - 하나 빔
        - Name-based Destructring → 구조 분해 할당을 순서가 아닌 이름을 중점으로 값이 할당
        - Collection Literals → listOf(…) 등과 같은 함수가 아닌 [..] 등으로 사용 가능(내부 리터럴 방식 어떻게 짰는지 궁금)
    - Gradle: Groovy kts → kotlin kts가 먼저 적용됨 → 찾아보기

Compose Multiplatform → Flutter, React Native, ionic 같은 거인듯

참고) Compose for web(Web Assembley)?

→ 해당 강좌 예시에서는 Desktop, iOS, Android, Web server(Spring Boot)를 하나의 프로젝트(base)로 제작 하셨음.

cf) iOS는 폐쇄적인 성격 때문에 따로 퍼일을 구성함

<br>

---

<br>

### Session 2. 함수형 코틀린

~~패캠에서 강의하셨던 분 아닌가 → 맞네~~

- 함수형 언어는 완성이 되게 느렸다
    - 함수형 언어 → 고차함수? 관심사를 분리? 모나드?
        
        47Degree?? 
        
    - 명령형 프로그래밍(Imperative programming) → 일반적  프로그래밍?(변수와 mutation)
    - 선언적 프로그래밍(Expression oriented programming) → 함수형 언어로 생각했던 선언 프로그래밍(what이 아닌 how)
        - mutation 때문에 선언적 프로그래밍이 불가능하지 않나? → scope function으로 해결이 가능하다(kotlin의 경우)
        - 공통되지 않는 로직은 어떻게 처리해야 하는지? → 일급함수의 성질을 이용하여 해결(파라미터에 () → {…} 같이 선언 후 사용)
            - 이 경우는 유닛 테스트시에도 사용 가능
        - Monad(뭔지 좀 더 알아보기) → 용어에 너무 매료되지 말자
            - collections
                - Monoid:  combine되는 경우(아니면 연산 되는 경우..?) == monaid하다(어떤 연산이 충족되는 경우?)
                - Functor: collection이 **map**같이 새로이 변화가 가능?
                - Monad: **flatMap**을 이용해 다른 collection으로 변화가 가능?
                - Optional, Mono도 여기에 속함
        - 코틀린에서는  flatMap이 중첩 될수 밖에 없는 한계가 존재
            - 다른 언어에서는 Monad comprehension이 존재하여 간결하게 사용이 가능
            - 그럼 어떻게 해결?
                - Result의 경우 수신객체를 이용하여 Result에 대한 람다함수를 만듦
                - bind()로 뭔가 붙이는거 같은데 잘 안보임
                - 구현에 있어서 잘 안되는 경우는 수신객체를 이용해서 풀어보면 될 수도 있음
                - HKT → 제너릭 안에 제너릭 넣는…?(Scala에서는 이게 가능하다고 함)
            - Monad가 이, 삼중으로 쓰이는 경우 kotlin은 이걸 해결할 수 없다
                - 해결 하려면 Monad 자체를 줄여야 함
                - Mono<Result<Optional<T>>>의 경우
                    - suspend
                    - nullable type 선언
                    
                    로 하나로 줄일 수 있다.(아름다운 방법은 아니라고 함)
                    
                - arrow Library를 이용하면 어느정도 문제들을 간단히 할 수 있다.
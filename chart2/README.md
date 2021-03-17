### :apple: Propositional Logic (명제 논리)

- 질문자의 질문에 대해 knowledge base의 지식을 바탕으로 추론하여 대답을 출력하는 시스템

- knowledge base에 저장된 "지식은 어떻게 표현" 되며 지식을 사용하여 "어떻게 추론" 하는가?

- 지식표현과 추론에 있어서 knowledge base내용과 추론을 따로 분리할 수 있는 지식 표현 추론 방법이어야 한다.

---

#### :goat: Propositional Logic

- 지식을 (1)표현 하고, 지식을 사용하여 (2)추론하는 방법에 대한 연구 중 하나

- 명제나 문장들 간의 논리적 관계를 다룬다.

- 명제와 명제 간의 논리적 관계가 충분히 정의되어 있다면, 추론 방식으로 질의 명제가 참인지 아닌지 추론할 수 있다.

KB에 Propositional logic을 사용하여 지식을 저장하고, KB의 지식을 사용하여 질의 명제가 참인지 거짓인지 판별하는 시스템

---

#### :fish: Syntax

- 명제를 어떻게 표현할 것인가?
- 명제 간의 논리적 관계는 어떤 관계가 있으며 어떻게 표현할 것인가?

---

#### :bug: Semantics

- 표현된 명제는 참인가 거짓인가를 어떻게 판단할 것인가? ( 해석 )

---

- 명제는 변수로 표현되며 (t) or (f) 을 판단할 수 있다.
- 변수(명제) 사이의 논리적 관계는 부정, AND, OR, if A then B, A if and only if B (동치?)

- 부정 AND OR if A then B , A if and only if B
- ￢ ∧ ∨ ⇒ ⇔

#### :dog: fomula

```
단일 변수로 표현된 명제 및 명제 사이에 정의된 논리 관계는 formula라 불린다.
```

￢ A, (A), A∧ B, A∨ B, A⇒B, A ⇔ B 등

---

Conjunctive Normal Form

연습 (A ⇒ B) ∧ ((A ∧ B) ⇒ C) ∧ ((A ∨ B) ⇒ C) ∧ (¬A ⇒ ¬C)

(~A V B) ^ (~(A ^ B) V C) ^ (~(A V B) V C ) ^ ( A V ~C)

(~A V B) ^ (~A V ~B V C) ^ (~A V C) ^ (~B V C) ^ (A V ~C)

Conjunctive Normal Form 을 통해 질문지에 대한 해답을 빠르게 판단할 수 있었다.
Resolution Rule 적용

---

### :cat: Horn Clauses

Conjunctive Normal Form을 만족하는 것 중에

positive한 변수가 최대 1개

(~A V ~B V ~C) => Horn clauses
(~A V ~B V C) => Horn clauses
(~A V ~B V C V D) => X
(D) => Horn clauses

---

### :zap: Resolution Rule

```
a (t)
a => b (t)                   => b(t)
```

```
a v b (t)
b => c (t)                   => a v c (t)

- 증명 => a v c 가 f 라면 a (f) and c (f) 여야 하는데 그럼 기존 식이 모순을 일으키기 때문에 a v c (t) 라는것은 옳다.
```

```
a v b (t)

~b v c (t)                  => a v c (t)

- b => c  <=> ~b v c 인 이유는 진리표를 이용해 증명 가능하다.

```

---

### :orange: RESULUTION 적용

```
아빠 => 스페인에 가는 중이다 ( 우리는 뉴케슬에서 왔다)
엄마 => 우리는 스페인을 가는중이 아니고 뉴케슬에서 왔다.(파리를 들렀고 스페인을 가는중이 아니다.)
딸 => 우리는 뉴케슬에서 오지 않았다. (우리는 파리를 들렀다.)


a (스페인에 가는중이다)
b (뉴케슬에서 왔다)
c (파리에 들렀다.)

아빠 => a v b
엄마 => (~a ^ b) v (c ^ ~a)
딸   => ~b v c

아빠 엄마 딸이 모두 참이라고 한다면, kb는

(a v b) ^ ((~a ^ b) v (c ^ ~a)) ^ (~b v c)

(a v b) ^ (~a) ^ (b v c) ^ (~b v c)             => a (f)

(a v b) ^ (~a)                                  => b (t)

(b v c) ^ (~b v c)                              => c (t)


결론으로 스페인은 가는중이 아니고 뉴케슬에서 왔으며 파리르 들렸다.

```

---

### :apple: SLD resolution

- inference rule을 사용하여 가장 최근에 도출한 결과로 생성된 clause를 사용하여 다음 clause를 infer한다.

```
A1 ^ A2 ^ An => B1  ,   B1 ^ B2 ^ Bn => f

~(A1 ^ A2 ^ An) v B1 ,  ~(B1 ^ B2 ^ Bn) v f

~(A1 ^ A2 ^ An) v B1 , ~B1 V ~B2 v ~Bn v f

~A1 V ~A2 V ~An V B1 , ~B1 V ~B2 v ~Bn v f

~A1 V ~A2 V ~An V ~B1 V ~B2 V ~Bn V f   (t)

A1 ^ A2 ^ An ^ B1 ^ B2 ^ Bn ^ t   (f)

A1 ^ A2 ^ An ^ B1 ^ B2 ^ Bn (f)

```

```
목적 => 스키를 탈 수 있나 없나

a = nice_weather
b = snowfall
c = snow
d = skiing

d =  true or false

(a) ^ (b) ^ (b => c) ^ (a ^ c => d)

스키를 탈수없다라고 가정한다면 d => f 를 추가

(a ^ c => d) , d=> f

~(a ^ c) V d , ~d v f

~(a ^ c) v f  = (t)

~(a ^ c) = t

(a ^ c) => f 라는 것을 도출한다. 이것을 이용해서

b -> c , (a ^ c) -> f 을 이용하면

~b v c , ~(a ^c) v f

~b v c , ~a v ~c v f

~b v ~a v f = t

~b v ~a = t

b ^ a -> f  을 도출한다.

a , b ^ a -> f

a , ~(b ^ a) v f

a , ~b v ~a v f  t

~b v f = t

b -> f 도출

b , b -> f

b , ~b v f

f != t 즉 모순이 발생하므로 d 가 f 라는것은 틀렸다 그러므로

d  = t  이고 스키는 탈 수 있다.


```

#### exercise 2.2

1. ~(a ^ b) <=> ~a v ~b (동치이고 같다. 이유는 진리표)
2. a -> b <=> ~b -> ~a

```
a -> b

~a v b

~b -> ~ a

b v ~a         ~a v b ==== b v ~a
```

3. ((a->b) ^ (b -> a)) <-> (a<->b)
4. (a v b ) ^ (~b v c) => (a v c) 모순 a (f) c (f)

---

#### exercise 2.3

- conjunctive normal form 변경

1. a <-> b

```
a <-> b  <=> (a->b) ^ (b->a)

(~a v b) ^ (~b v a)

```

2. a ^ b <-> a v b

```
((a ^ b) -> (a v b) ) ^ ((a v b) -> (a ^ b) )

(~(a ^ b) v (a v b)) ^ (~(a v b ) v (a ^ b))

(~a v ~ b v (a v b)) ^ (~(a v b ) v (a ^ b))


```

3 A ^ (A -> B) -> B

```
~( A ^ (A -> B) ) V B

~A V ~(~A V B) V B

~A V (A ^ B) V B

```

#### exercise 2.4

A V ~(A V ~B) ^ B

TT TF FT FF 모두 불만족

#### exercise 2.10

```
b = 공범이있다.
c = 키가 있다.
d = 범인이 차를 타고 왔다.

b -> d  (t)
c       (t)
(~b ^ ~c) v ( b ^ c)      (T)

d ->f 라고 가정

b -> d , d -> f

~b v d , d -> f

~b v d , ~d v f

~b v f  = (t)

b = f (t)

(~b ^ ~c) v (b ^ c) , b -> f

(~b ^ ~c) v f    (t)

(~b ^ ~c)   (t)

c  => f 여야 하는데 c -> t 이므로 모순이다 그렇기 때문에 범인이 차를 타고 오지 않았다는 거짓이므로 범인은 차를 타고 왔다.

```

#### exercise 2.11

(a v b ) ^ (~b v c) => (a v c)

```
a (f)  and c (f) 라고하면 모순이 되기 때문에 참
```

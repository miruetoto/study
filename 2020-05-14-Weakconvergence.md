---
layout : post 
title : (정리) 분포수렴
---
### About this doc

- 수통강의노트 

- 학부수준 

- 이번에는 김우철 교수님 교재 5장 중 분포수렴을 정리함. 

### 분포수렴 

- 확률변수열 $Y_1,Y_2,\dots$ 이 적당한 확률변수 $Y$로 분포수렴한다는 (***의문: 이러한 확률변수 $Y$가 항상 존재해??, 일단 존재한다고 보자. 이유는 이따가 설명할것임.***) 의미는 [확률변수 $Y$의 누적분포함수 $F(y)$가 연속인 모든점 $y$에서]
\begin{align}
\lim_{n\to\infty}P(Y_n\leq y)=P(Y\leq y), \quad \forall y \in \mathbb{R}
\end{align}
라는 의미로 생각할 수 있다. 여기에서 $Y_n$대신에 $\sqrt{n}(\bar{X}-\mu)$을 $Y$대신에 $Z^* \sim N(0,\sigma^2)$을 대입하면 중심극한 정리가 된다. 

- 여기에서 왜 굳이 아래와 같은 표현을 하는지에 대한 이해는 쉽지않다. 
> [확률변수 $Y$의 누적분포함수 $F(y)$가 연속인 모든점 $y$에서]

- 그래도 차근차근 이해해보자. $P(Y_n\leq x)=F_n(y)$, $P(Y\leq x)=F(y)$라고 두면 위의 정의를 아래와 같이 쓸 수 있다. 
\begin{align}
\lim_{n\to\infty}F_n(y)=F(y), \quad \forall y: y \in \mathbb{R}-D_{F(\cdot)}
\end{align}
여기에서 $D_{F(\cdot)}$는 $F(y)$가 불연속인 점들의 집합 이다. 즉 
\begin{align}
D_{F(\cdot)}=\big\\{y: F(y)\mbox{ is discontinuous } \big\\}
\end{align}
이다. 이때 $F(y)$를 $Y_1,Y_2,\dots,Y_n$의 극한분포라고 한다. 

- 즉 극한분포는 엄밀하게 아래와 같이 정의한다. 
>$F(y)$가 확률변수열 $\big\\{Y_n\big\\}$의 극한분포라고 하는 것은 아래가 성립한다는 말과 같다. 
\begin{align}
\lim_{n\to\infty} cdf_{Y_n}(y) = F(y) \quad \forall y: y \in \mathbb{R}-D_{F(\cdot)}
\end{align}

- 보통은 위에서 $\forall y: y \in \mathbb{R}-D_{F(\cdot)}$조건을 생략한것이 극한분포의 정의로 알고 있는데 이는 사실이 아니다. 

- $y \in \mathbb{R}-D_{F(\cdot)}$와 같은 조건을 고려하는 이유는 누적분포함수의 극한이 항상 누적분포함수는 아니기 때문이다. 교재의 5.2.1의 예제를 살펴보자. 
\begin{align}
F_n(y)=\begin{cases} 
0, & y<0 \\\\ \\
\frac{y}{2(1+1/n)}, & 0\leq y < 1+1/n \\\\ \\
1, & y\geq 1+1/n
\end{cases}
\end{align}
은 누적분포함수인데 (즉 증가하고, 오른쪽 연속임) 그 것의 극한값 $\lim_{n\to \infty}F_n(y)=G(y)$은 누적분포함수가 아니다. 
\begin{align}
G(y)=\begin{cases}
0, & y<0 \\\\ \\
\frac{y}{2}, & 0\leq y \leq 1 
1, & y>1
\end{cases}
\end{align}
왜냐하면 오른쪽 연속이 아니기 때문이다. 

- $G(y)$를 적당히 수정하여 아래와 같이 $F(y)$를 만들면 $F(y)$는 누적분포함수가 된다. 
\begin{align}
F(y)=\begin{cases}
0, & y<0 \\\\ \\
\frac{y}{2}, & 0\leq y <1 \\\\ \\
1, & y\leq 1 
\end{cases}
\end{align}

- ***의문: 이런식으로 계속 $G(y)$를 $F(y)$로 바꿀 수 있을까?? 즉 확률변수열 $Y_1,Y_2,\dots,Y_n,\dots$의 cdf가 점별수렴하면 확률변수열의 극한분포가 항상 존재할까? 일단은 이게 가능하다고 믿자.***

- $G(y)$를 무조건 $F(y)$로 바꿀수 있다고 치자. 그런데 $F(y)$가 *cdf*이므로 $F(y)$를 누적분포함수로 삼는 어떠한 확률변수가 반드시 존재할 것이다. (이건 정리 4.4.3(b)에서 증명했다!! 이따가 이 내용에 대한 간략한 소개를 하겠다.) 이 확률변수를 $Y$라고 하자. 그럼 처음에 제기하였던 $Y$의 존재성에 대한 의문이 해결된다. 

- 그럼 이제 우리는 확률변수 $Y_1,Y_2,\dots,Y_n,\dots$의 *cdf*가 어떤 함수로 $G(\cdot)$으로 점별수렴한다면 (여기에서 어떤함수 $G(\cdot)$은 반드시 *cdf*일 필요는 없음) <br/><br/>
(1) $Y_1,Y_2,\dots,Y_n,\dots$의 극한분포가 항상존재하고 (헬리셀렉션) <br/>
(2) $Y_1,Y_2,\dots,Y_n,\dots$의 극한분포와 동일한 분포를 가지는 확률변수 $Y$가 반드시 존재함을 보일수 있다. (정리 4.4.3.(b), 즉 확률적분변환) <br/>

- *(Helly’s selection theorem)* For every sequence $\{F_n\}$ of distribution functions, there is a subsequence $\{F_{n(k)}\}$ and a right continuous nondecreasing function $F$ so that 
\begin{align}
\lim_{k \to \infty}F_{n(k)}(y)= F(y)
\end{align}
at all continuity points $y$ of $F$.

- 결국 헬리셀렉션정리는 [순증가하고 유계인함수라면 점프가 기껏해야 유한개임]을 이해하면 아무것도 아니다. 아래와 같은 로직으로 증명 할 수 있다. <br/><br/>
(1) 분포함수열 $F_n(\cdot)$의 극한이 있다면 이는 반드시 증가함수이고 최소값이 0 최대값이 1일 것이다. 즉 $G(\cdot)$가 존재한다면 이는 순증가함수이고 최소값이0 최대값이 1이다. <br/>
(2) [$\dots$]의 내용을 이용하면 $F_n(\cdot)$의 극한 $G(\cdot)$도 점프가 기껏해야 유한개임을 쉽게 유추할 수 있다. <br/>
(3) 점프가 있는 곳에서 $G(\cdot)$가 오른쪽 연속이 아닐수도 있는데 이를 오른쪽 연속이 되도록 수정하면 $G(\cdot)$과 기껏해야 유한개의 점에서만 함수값이 차이는 새로운 함수 $F(\cdot)$을 만들 수 있다. 


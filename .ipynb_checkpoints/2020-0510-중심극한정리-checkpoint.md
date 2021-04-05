---
layout : post 
title : (정리) 중심극한정리 
---

### About this doc

- 수통강의노트 

- 이번에는 김우철 교수님 교재 5장 중 중심극한정리를 정리함. 

- 학부수준 

### 중심극한 정리 

- 확률변수 $X_1,\dots,X_n$이 서로 독립이고 동일한 분포를 따른다고 하자. 그리고 $V(X_1)$이 양의실수라고 하자. 또한 $EX_1=\mu$, $VX_1=\sigma^2$ 이라고 하자. 

- 이 조건은 생각보다 강한조건들이다. 우선 (1) ***iid***가정을 사용하였고 (2) 분산이 유한함을 가정하였다. 

- 교재에서는 증명의 편의성을 위해서 (3) $X_1$의 *mgf*가 존재한다고 가정하였다. 참고로 *mgf*가 존재하려면 모든 모멘트가 유한하여야 하므로 (3)의 조건은 (2)의 조건을 포함한다. 

- 분산이 유한함을 가정하는것도 엄청난 조건인데 *mgf*가 존재한다는 조건은 더 엄청난 조건이다. 따라서 수리통계에서 얼마나 강한가정하에서 중심극한 정리를 증명했는지 보여준다. 

- 아무튼 이러한 조건에서 아래가 성립한다. 
\begin{align}
\lim_{n\to\infty}P\Bigg(\frac{\bar X-\mu}{\sigma/\sqrt{n} }\leq x\Bigg)=P(Z\leq x)
\end{align}
위의 조건을 간략하게 아래와 같이 표현하기도 한다. 
\begin{align}
\frac{\bar X-\mu}{\sigma/\sqrt{n} } \overset{d}{\to} Z, \quad Z\sim N(0,1)
\end{align}
그리고 $\frac{\bar X-\mu}{\sigma/\sqrt{n} }$가 표준정규분포를 따르는 확률변수 $Z$로 분포수렴한다고 한다. 영어로는 convergence in distribution 혹은 convergence in law 라고 한다. 

- 이때 위에서 $\frac{\bar X-\mu}{\sigma/\sqrt{n} }= \frac{\sqrt{n}(\bar{X}-\mu)}{\sigma }$를 정리하여 아래와 같이 표현하기도 한다. 
\begin{align}
\frac{\sqrt{n}(\bar{X}-\mu)}{\sigma } \overset{d}{\to} Z, \quad Z\sim N(0,1)
\end{align}
사실 아래가 가장 일반적인 표현이다. 
\begin{align}
\sqrt{n}(\bar{X}-\mu)\overset{d}{\to} Z^* , \quad Z^ * \sim N(0,\sigma^2)
\end{align}
위를 간단하게 아래와 같이 쓰기도 한다. 
\begin{align}
\sqrt{n}(\bar{X}-\mu)\overset{d}{\to} N(0,\sigma^2)
\end{align}


--- 

### 중심극한 정리의 물결증명

- 증명은 테일러 정리를 이용한다. 그렇게 어렵지 않다고 말하고 싶지만 생각보다 어렵다. 

- 우선 김우철 교수님의 교재 p.208의 64)의 내용이 무엇인지 살펴보자. 아래와 같이 되어있다.
> 일반적으로 $Z$의 누적분포함수가 연속함수일 때 다음이 성립한다. 
\begin{align}
&\lim_{n \to \infty}mgf_{Z_n}(t)=mgf_Z(t), ~~ \forall t: \|t\|<h ~ (\exists h>0) \\\\ \\
&\Longrightarrow \quad \lim_{n\to\infty}P(Z_n\leq x)=P(Z\leq x), ~~ \forall x
\end{align}


- 위의 말은 결국 분포수렴임을 보이려면 원래 *cdf*가 수렴함을 보여야하는데 극한분포가 연속일경우 (예를들면 표준정규분포 같은) *mgf*가 수렴함을 보이면 충분하다는 의미이다. 따라서 결국 우리는 $\frac{\sqrt{n}(\bar{X}-\mu)}{\sigma^2}$의 *mgf*가 $n \to \infty$일때 $e^{t^2/2}$로 수렴함을 보이면 된다. 즉 
\begin{align}
\lim_{n\to \infty} mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t) = e^{t^2/2}
\end{align}
임을 보이면 된다. 

- *mgf*의 정의에 의해서 바로 아래를 관찰할 수 있다. 
\begin{align}
mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t)=\big(mgf_{(X_1-\mu)/\sigma}(t/\sqrt{n})\big)^n
\end{align}
이는 다음의 사실들을 상기하면 쉽게 위의 식이 성립함을 알수있다. (연습장) <br/><br/>
**(1)** $mgf_{aX}(t)=mgf_X(at)$. ($pdf_{aX}(x)=\frac{1}{a}pdf_X(\frac{x}{a})$와 혼돈하지말것. 일반적으로는 $mgf_{aX+b}(t)=e^{bt}mgf_X(at)$임) <br/>
**(2)** $X_1,\dots,X_n$은 ***iid.***

- $mgf_{(X_1-\mu)/\sigma}(t/\sqrt{n})$를 테일러 전개하자. 함수이름이 너무 기니까 $m(\cdot):=mgf_{(X_1-\mu)/\sigma}(\cdot)$이라고 정의하자. $m(x)$를 $x=0$에서 테일러 전개하면 
\begin{align}
m(x)=m(0)+(x-0)m^{(1)}(0)+\frac{(x-0)^2}{2!}m^{(2)}(0)+\dots
\end{align}
와 같이 된다. 

- 여기에서 $\dots$는 나머지텀이라고 부르는데 $x\to 0$ 일 수록 0에 가까워지는 항목이다. 사실 $m(0)$을 제외한 모든 항목은 $x\to0$ 일수록 0에 가까워진다. 편의상 $m(0)$을 0차-미분항, $(x-0)m^{(1)}(0)$을 1차-미분항, $\frac{(x-0)^2}{2!}m^{(2)}(0)$를 2차-미분항으로 부르기로 하자. 따라서 나머지텀은 3차-미분항, 4차-미분항... 등을 포함하는 항목인데 편의상 이를 뭉뚱그려서 3차이상의 고차미분항으로 부르자. 아무튼 대충 아래의 느낌으로 이해하면 된다. 
\begin{align}
m(x)\approx m(0)+xm^{(1)}(0)+x^2m^{(2)}(0)
\end{align}

- $m(0)=1$, $m^{(1)}(0)=mgf_{(X_1-\mu)/\sigma}(0)=E\big(\frac{X_1-\mu}{\sigma}\big),\dots$ 등을 활용하면, 
\begin{align}
m(x) \approx 1+xE\bigg(\frac{X_1-\mu}{\sigma}\bigg)+\frac{x^2}{2}E\bigg(\frac{X_1-\mu}{\sigma}\bigg)^2
\end{align}
그런데 $E\big(\frac{X_1-\mu}{\sigma}\big)=0$이고 $E\big(\frac{X_1-\mu}{\sigma}\big)^2=1$이므로 
\begin{align}
m(x)\approx 1+\frac{x^2}{2}
\end{align}
$x$대신에 $t/\sqrt{n}$을 대입하면 
\begin{align}
m(t/\sqrt{n}) \approx 1+\frac{t^2}{2n}
\end{align}

- 아무튼 
\begin{align}
mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t)=\big(mgf_{(X_1-\mu)/\sigma}(t/\sqrt{n})\big)^n=\big(m(t/\sqrt{n})\big)^n
\end{align}
이라고 하였는데 $m(t/\sqrt{n})\approx 1+\frac{t^2}{2n}$이라고 쓸 수 있으므로 아래와 같이 쓸 수 있다. 
\begin{align}
mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t)\approx \bigg(1+\frac{t^2}{2n} \bigg)^n
\end{align}
따라서 
\begin{align}
\log mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t) \approx n \log \bigg(1+\frac{t^2}{2n}\bigg) 
\end{align}

- 그런데 
\begin{align}
\log\bigg(1+\frac{t^2}{2n}\bigg)\approx \frac{t^2}{2n}
\end{align}
이 성립한다. 왜냐하면 
\begin{align}
\log(1+x) =x-\frac{x^2}{2}+\frac{x^3}{3}+\dots
\end{align}
와 같은 표현이 가능하기 때문이다. 

- 따라서 
\begin{align}
\log mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t) \approx n \log \bigg(1+\frac{t^2}{2n}\bigg) \approx \frac{t^2}{2} 
\end{align}
가 된다. 따라서 
\begin{align}
e^{\log mgf_{\sqrt{n}(\bar{X}-\mu)/\sigma }(t)} \approx 
e^{n log(1+\frac{t^2}{2n})} 
\approx e^{t^2/2}
\end{align}
첫번째 물결은 $t/\sqrt{n}$이 $0$으로 갈때 성립하고 두번째 물결은 $t^2/2n$이 $0$으로 갈때 성립하므로 $n\to\infty$일때 두 물결이 모두 등호가 된다. (두번째 물결이 첫번째 물결보다 빠르게 등호로 된다.)

--- 

### 중심극한 정리의 좀 더 엄밀한 증명 (잉여항의 처리)

***테일러전개에 대한 간단한 추가설명*** 

- $f(x)$를 $x=a$에서 테일러전개하면 아래와 같다. 
\begin{align}
f(x)=f(a)+(x-a)\times f^{(1)}(a)+\frac{(x-a)^2}{2!}\times f^{(2)}(a) + \dots
\end{align}

- 위의 식은 아래와 같이 생겼다. 
\begin{align}
f(x)&=f(a)+\mbox{1차미분항}+\dots \\\\ \\
&=f(a)+\mbox{[1차미분항의다항식부분]}\times\mbox{[1차미분계수]}+\dots
\end{align}

- 우리의 문제는 $f$대신에 $m$을 대입하고 $a$대신에 $0$을 대입하면 된다. 그러면 아래와 같이 된다. 
\begin{align}
m(x)=m(0)+(x-0)\times m^{(1)}(0)+\frac{(x-0)^2}{2!}\times m^{(2)}(0) + \dots
\end{align}

- 0차미분항을 제외하고 나머지는 모두 $x\to 0$일때 $0$으로 가까워진다. 그리고 이론적으로 고차항일수록 $x\to 0$ 일때 더욱 더 빠르게 가까워진다. 예를들어서 
\begin{align}
(x-0)\times m^{(1)}(0)
\end{align}
보다 
\begin{align}
\frac{(x-0)^2}{2!}\times m^{(2)}(0)
\end{align}
이 더욱 빠르게 가까워진다. 

- 위의 결과는 자명하진 않다. 기본적으로 <br/><br/>
(1) [미분항의다항식부분]은 고차항으로 갈수록 빠르게 $0$으로 되는것이  자명하다. 즉 $(x-0)$보다 $\frac{(x-0)^2}{2!}$이 더욱 빠르게 $0$으로 수렴 <br/><br/>
함은 자명하다. <br/><br/>
(2) 하지만 [미분항]이 오차항으로 갈수록 빠르게 수렴하는것은 자명하지 않다. 왜냐하면 [미분계수]의 값이 얼마가 될지 모르기 때문이다. 즉 $(x-0)\times m^{(1)}(0)$보다 $\frac{(x-0)^2}{2!}\times m^{(2)}(0)$이 더욱 빠르게 $0$으로 수렴 <br/><br/>
함은 자명하지 않다. 왜냐하면 $m^{(2)}(0)$등이 값자기 무한대가 되어버릴수도 있기 때문이다. 

- 따라서 테일러 전개가 가능하려면 $m(x)$를 $x=0$에서 반복적으로 미분하였을때 [미분계수]가 갑자기 무한대로 터지는 경우는 제외해야 한다. 이를 수학적으로는 **"$m(x)$가 $x=a$에서 무한번 미분가능하다."** 라고 표현한다. 

- 결론적으로 고차[미분항]일수록 $x \to 0$으로 갈때 더욱 빠르게 $0$로 수렴한다. 그 이유는 이 과정에선 설명할 수 없으니 해석학교재를 참고하길 바란다. 

- 얼마나 빠르게 $0$으로 수렴하는지 잴 수 있을까? 편의상 [미분항]의 수렴속도는 [미분계수]가 아니라 [미분항의 다항식부분]에만 의존한다고 하자. 즉 [미분계수] $m^{(1)}(0),m^{(2)}(0),\dots$ 등은 대세에 영향을 미치지 못하는 항이라고 생각하자. (실제로 그러하다. 왜냐하면 우리는 테일러 전개가 가능한 함수를 생각하므로.) 즉 얼마나 빠르게 $0$으로 수렴하는지는 오로지 각 [미분항의 다항식 부분], 즉 
\begin{align}
(x-0),\frac{(x-0)^2}{2!},\frac{(x-0)^3}{3!},\dots
\end{align}
등에 의해서만 결정된다고 가정하자. 

- 먼저 $x\to 0$일 경우 얼마나 빠르게 수렴하는지 체크하기 위해서 각 항을 $(x-0)$으로 나누어보자.
\begin{align}
1,\frac{(x-0)}{2!},\frac{(x-0)^2}{3!},\dots
\end{align}
[1차미분항의 다항식 부분]은 $x\to 0 $ 일 경우 $0$으로 수렴하지 않고 나머지항목들은 여전히 수렴한다. 왜냐하면 [1차미분항의 다항식부분]은 $(x-0)$과 똑같은 속도로 $0$으로 향해 갔는데 [2차미분항의 다항식부분]은 $(x-0)$보다 더 빠른 속도로 $0$으로 향했으며 [3차미분항의 다항식부분]은 더 빠르게 $0$으로 향해갔기 때문이다. 

- 느낌을 이해하는게 중요한데 대충 아래의 느낌이다. <br/><br/>
(1) 테일러 정리에서는 0차미분항을 제외하고 모두 $x \to a$일때 $0$으로 수렴한다. <br/>
(2) 1차미분텀은 가장 느리게 $0$으로 수렴한다. <br/>
(3) 2차미분항은 1차보다 빠르게 $0$으로 수렴한다. <br/>
(4) 3차미분항은 2차보다 빠르게 $0$으로 수렴한다. <br/> 

- 이 논의를 일반화 시키면 각 [$n$차미분항]이 $(x-0)^n$와 같은 속도로 수렴함을 쉽게 유추할 수 있다. 이를 기호로 쓰면 아래와 같다. 
\begin{align}
x =& O(x), \quad as ~ x \to 0 \\\\ \\
\frac{x^2}{2!} =& O(x^2), \quad as ~ x \to 0  \\\\ \\
\frac{x^3}{3!} =& O(x^3), \quad as ~ x \to 0 \\\\
\dots
\end{align}

- 여기에서 
\begin{align}
& f(x)=O(g(x)), \quad x\to a  \\\\ \\
& \Longleftrightarrow \underset{x\to a}{\operatorname{limsup} }\left\|\frac{f(x)}{g(x)}\right\| <  \infty 
\end{align}

- 즉 임의의 점 $x=a$에서의 테일러 전개는 아래와 같이 쓸 수 있다. 
\begin{align}
m(x)=&m(a)+R(x,a)  \\\\ \\
m(x)=&m(a)+(x-a)m^{(1)}(a)+R^* (x,a) \\\\ \\
m(x)=&m(a)+(x-a)m^{(1)}(a)+\frac{(x-a)^2}{2!}m^{(2)}(a) +\tilde{R}(x,a) \\\\ \\
\dots
\end{align}
이때 나머지항 $R(x,a)$, $R^* (x,a)$, $\tilde{R}(x,a)$는 각각 아래를 만족한다. 
\begin{align}
R(x,a)=O(x-a) \quad as ~ x \to a \\\\ \\
R^* (x,a)=O\big((x-a)^2\big) \quad as ~ x \to a \\\\ \\
\tilde{R}(x,a)=O\big((x-a)^3\big) \quad as ~ x \to a 
\end{align}

- 위를 간략하게 아래와 같이 쓰기도 한다. 
\begin{align}
m(x)=&m(a)+O(x-a), \quad \quad as ~ x \to a \\\\ \\
m(x)=&m(a)+(x-a)m^{(1)}(a)+O\big((x-a)^2\big), \quad \quad as ~ x \to a \\\\ \\
m(x)=&m(a)+(x-a)m^{(1)}(a)+\frac{(x-a)^2}{2!}m^{(2)}(a)+O\big((x-a)^3\big), \quad \quad as ~ x \to a \\\\ \\
\dots
\end{align}

- 아래와 같은 예제들을 관찰하자. 
\begin{align}
\log(1+x) &=x-\frac{x^2}{2}+\frac{x^3}{3}+O(x^4) \\\\ \\
e^x &=1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+O(x^4) \\\\ \\
\cos x &=1-\frac{x^2}{2!}+\frac{x^4}{4!}+O(x^6)
\end{align}

- 따라서 대충 아래와 같은 느낌으로 기억하면 된다. 
\begin{align}
m(x)=&m(a)+ O(\mbox{1차미분항의 다항식}) \\\\ \\
m(x)=&m(a)+\mbox{1차미분항}+ O(\mbox{2차미분항의 다항식}) \\\\ \\
m(x)=&m(a)+\mbox{1차미분항}+ \mbox{2차미분항}+ O(\mbox{3차미분항의 다항식}) \\\\ \\
\dots
\end{align}

- 아무튼 이제 본론으로 돌아와서 
\begin{align}
m(x)=m(0)+x \times m^{(1)}(0)+\frac{x^2}{2!} \times m^{(2)}(0) + O(x^3)
\end{align}
와 같이 된다. $x$대신에 $\frac{t}{\sqrt{n} }$을 대입하면 잉여항은 $O\big(\frac{t^3}{n\sqrt{n} }\big)$와 같이 된다. 따라서 
\begin{align}
m\bigg(\frac{t}{\sqrt{n} }\bigg)=1+\frac{t^2}{2n}+O\bigg(\frac{t^3}{n\sqrt{n} }\bigg)
\end{align}
따라서 
\begin{align}
\log \left[m\bigg(\frac{t}{\sqrt{n} }\bigg)\right]^n=n\log \left[1+\frac{t^2}{2n}+O\bigg(\frac{t^3}{n\sqrt{n} }\bigg)\right]:=n \log(1+A)
\end{align}
여기에서 
\begin{align}
A=\frac{t^2}{2n}+O\bigg(\frac{t^3}{n\sqrt{n} }\bigg), \quad t/\sqrt{n} \to 0 
\end{align}
이다. 

- 그런데 잘 생각해보면 
\begin{align}
A=\frac{t^2}{2n}+O\bigg(\frac{t^3}{n\sqrt{n} }\bigg), \quad t/\sqrt{n} \to 0 
\end{align}
의 수렴속도를 결정하는데 $t$는 하나도 안 중요하다는 것을 알 수 있다. 왜냐하면 $t$는 어차피 $0$근처의 어떠한 수이기 때문이다. (*mgf*의 정의상) 따라서 
\begin{align}
A=\frac{t^2}{2n}+O\bigg(\frac{1}{n\sqrt{n} }\bigg), \quad \frac{1}{\sqrt{n} }\to 0
\end{align}
라고 써도 아무런 이상이 없다. 그리고 동일한 논리로 
\begin{align}
A=\frac{t^2}{2n}+O\bigg(\frac{1}{n\sqrt{n} }\bigg), \quad \sqrt{n} \to \infty
\end{align}
와 같이도 쓸 수 있고 
\begin{align}
A=\frac{t^2}{2n}+O\bigg(\frac{1}{n\sqrt{n} }\bigg), \quad n \to \infty
\end{align}
와 같이도 쓸 수 있다. 정리하면 아래와 같이 쓸 수 있다. 
\begin{align}
A=\frac{t^2}{2n}+O(n^{-3/2}), \quad n \to \infty
\end{align}
이런 경우 $n \to \infty$는 생략하고 아래와 같이 간단하게 쓰기도 한다. 
\begin{align}
A=\frac{t^2}{2n}+O(n^{-3/2})
\end{align}


- (풀이1) $f(A)=\log(1+A)$라고 보고 아래와 같이 $A=0$에서 테일러 전개를 하자. 
\begin{align}
\log(1+A)=A-\frac{A^2}{2!}+O(A^3)
\end{align}
따라서 
\begin{align}
n\log(1+A)=nA-n\frac{A^2}{2!}+nO(A^3)
\end{align}
이다.  
\begin{align}
A^2=\bigg(\frac{t^2}{2n}\bigg)^2+2\bigg(\frac{t^2}{2n}\bigg)O(n^{-3/2})+\bigg(O(n^{-3/2})\bigg)^2
\end{align}
이므로 
\begin{align}
nA^2=n\bigg(\frac{t^2}{2n}\bigg)^2+2n\bigg(\frac{t^2}{2n}\bigg)O(n^{-3/2})+n\bigg(O(n^{-3/2})\bigg)^2
\end{align}
이 되고 따라서 명백하게 
\begin{align}
nA^2 \to 0, \quad as~ n \to \infty
\end{align}
이다. 2차-미분항이 $n\to\infty$ 일때 통째로 $0$으로 되므로 3차미분항 이상도 $n\to \infty$ 일때 통째로 $0$이 된다. 마지막으로 
\begin{align}
nA \to \frac{t^2}{2}, \quad as~ n \to \infty
\end{align}
임은 자명하다. 따라서 
\begin{align}
n\log(1+A)=nA-n\frac{A^2}{2!}+nO(A^3) \to \frac{t^2}{2} \quad as~ n\to \infty
\end{align}
이다. 

- (풀이2) $f(A)=\log(1+A)$라고 보고 아래와 같이 $A=0$에서 테일러 전개를 하자. 
\begin{align}
\log(1+A)=A+O(A^2)
\end{align}
따라서 
\begin{align}
n\log(1+A)=nA+nO(A^2)
\end{align}
그런데 $O(A)=O(n^{-1})$이므로 $O(A^2)=O(n^{-2})$이다. 따라서 $nO(A^2)$의 항은 $n\to\infty$에서 $0$으로 소멸한다. 나머지는 (풀이1)과 같다. 

### 간결하고 엄밀하며 빠른증명 

- $m(t/\sqrt{n})$은 아래와 같이 쓸 수 있다. 
\begin{align}
m\Big(\frac{t}{\sqrt{n} }\Big)=1+\frac{t^2}{2n}+\dots
\end{align}
여기에서 $\dots$ 을 $R(t/\sqrt{n})$이라고 하자. 

- 주장: 아래가 성립한다. 
\begin{align}
\lim_{n\to\infty}nR(t/\sqrt{n})=0
\end{align}

- 직관적 유추: 사실 테일러정리를 Big-$O$ 노테이션으로 기억하면 당연하다. 
\begin{align}
R(t/\sqrt{n})=O\bigg(\frac{t^3}{n\sqrt{n} }\bigg), \quad t/\sqrt{n} \to 0 
\end{align}
이고 이것의 수렴속도를 결정하는데 $t$는 하나도 안중요하니까 
\begin{align}
R(t/\sqrt{n})=O\big(n^{-3/2}\big), \quad n \to \infty
\end{align}
이다. 따라서 $\lim_{n\to\infty}nR(t/\sqrt{n})=0$이 성립함. 

- 증명: 테일러정리에 따라서 고정된 $t\neq0$에 대하여 
\begin{align}
\lim_{n\to\infty}\frac{R(t/\sqrt{n})}{(t/\sqrt{n})^2}=0
\end{align}
이 성립한다. $t$는 fixed이므로 (그러니까 $t$를 엄청 큰 실수로 생각하자) 아래가 성립한다. 
\begin{align}
\lim_{n\to\infty}nR(t/\sqrt{n})=0
\end{align}
그런데 위의식은 $t=0$이더라도 성립한다. 따라서 위의식은 임의의 고정된 $t$에 대하여 성립한다. 

- 따라서 아래와 같이 쓸 수 있다. 
\begin{align}
\lim_{n\to\infty} \Big(m(t/\sqrt{n})\Big)^n 
=& \lim_{n\to\infty}\left[1+\frac{t^2}{2n}+R(t/\sqrt{n})\right]^n \\\\ \\
=& \lim_{n\to\infty}\left[1+\frac{1}{n}\Big(\frac{t^2}{2n}+nR(t/\sqrt{n})\Big)\right]^n \\\\ \\
=& e^{t^2/2}
\end{align}
마지막 등호는 아래의 레마에 의해서 성립한다. 


- ***(Lemma 2.3.14, in casella)*** $a_n\to a$ as $n\to \infty$ 라고 하자. 그러면 아래가 성립한다. 
\begin{align}
\lim_{n\to\infty}\Big(1+\frac{a_n}{n}\Big)^n=e^a
\end{align}
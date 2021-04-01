---
layout: post
title: (정리) back fitting 
---

### About this doc 

- 통계공부

- 대학원 1-2학년 수준 

- 여기에서는 Backfitting에 대한 내용을 다룬다. 본 내용은 임요한 교수님의 응용통계 강의노트를 요약한 것이다. (챕터 6-(7) 직교화) 

### Back fitting 

- 실제모형이 아래와 같다고 하자. 
\begin{align}
{\bf y}= {\bf X_1} {\boldsymbol \beta_1} + {\bf X_2} {\boldsymbol \beta_2} + {\boldsymbol \epsilon} 
\end{align}
보통 이럴때는 아래와 같이 회귀계수를 구하면 된다. 
\begin{align}
\hat{\boldsymbol\beta}= \left({\bf X}'{\bf X}\right)^{-1}{\bf X}'{\bf y}
\end{align}
여기에서 ${\bf X}=cbind({\bf X_1}, {\bf X_2})$ 이고, ${\boldsymbol \beta}=rbind(\boldsymbol{\beta_1},\boldsymbol{\beta_2})$ 이다. 

- 잘 알겠지만 $\hat{\boldsymbol\beta_2}$ 을 구하고 싶다면 $\hat{\boldsymbol\beta}$ 에서 두번째 원소를 취하면 된다. 강의노트에서는 $\hat{\boldsymbol\beta_2}$ 와 아래의 방법으로 구한 $\tilde{\boldsymbol\beta_2}$ 가 같음을 증명하였다. <br/><br/>
**(1)** $\bf y$ 를 $\bf X_1$ 로 적합함. 그리고 잔차를 ${\bf e}_ {\bf y | \bf X_1}$ 이라 정의함. <br/>
**(2)** $\bf X_2$ 를 $\bf X_1$ 로 적합함. 그리고 잔차를 ${\bf e}_ {\bf X_2 | \bf X_1}$ 이라 정의함. <br/>
**(3)** (1) 의 잔차를 (2) 의 잔차로 적합함. 즉
\begin{align}
{\bf e}_ {\bf y | \bf X_1} \sim {\bf e}_ {\bf X_2 | \bf X_1}
\end{align}
을 수행함. 그리고 리그레션에서 ${\bf e}_ {\bf X_2 | \bf X_1}$ 에 대응하는 coef 를 $\tilde{\boldsymbol\beta_2}$라고 함. 

- 그리고 이 예제에 한정하여 아래와 같이 $\tilde{\boldsymbol\beta_2}$ 를 구하여도 상관없다. <br/><br/>
**(1)** $\bf X_2$ 를 $\bf X_1$ 로 적합함. 그리고 잔차를 ${\bf e}_ {\bf X_2 | \bf X_1}$ 이라 정의함. <br/>
**(2)** ${\bf y}$ 를 ${\bf e}_ {\bf X_2 | \bf X_1}$로 적합함. 이때 ${\bf e}_ {\bf X_2 | \bf X_1}$ 에 대응하는 coef 를 $\tilde{\boldsymbol\beta_2}$라고 함. 

- **(proof)** 증명은 그렇게 어렵지 않다. **우선 언급된 첫번째 방법과 두번째 방법이 같음을 보이는 것은 너무 쉽다.** 두번째 방법으로 구한 $\tilde{\boldsymbol\beta_2}$는 아래와 같이 표현가능하다. 
\begin{align}
\tilde{\boldsymbol\beta_2}=\bf{({X_2'(I-H_1})X_2)^{-1}X_2'(I-H_1)y}
\end{align}
이때 ${\bf y}$ 대신에 $\bf (I-H_1)y$를 대입하면 첫번째 방법으로 구한 $\tilde{\boldsymbol\beta_2}$가 되는데 
\begin{align}
\bf (I-H_1)^2=(I-H_1)
\end{align}
이 성립하므로 **언급된 첫번째 방법과 두번째 방법은 같은 방법이다.** 이제 $\tilde{\boldsymbol\beta_2}=\hat{\boldsymbol\beta_2}$임을 보이자. 즉 $\hat{\boldsymbol\beta_2}$는 아래임을 보이자. 
\begin{align}
\hat{\boldsymbol\beta_2}=\bf(X_2'(I-H_1)X_2)^{-1}X_2'(I-H_1)y
\end{align}
이걸 보이기 위해서는 아래를 보여도 충분하다. 
\begin{align}
\bf{(X_2'(I-H_1)X_2)}\hat{\boldsymbol\beta_2}=\bf{X_2'(I-H_1)y} 
\end{align}
본디 $rbind(\hat{\boldsymbol\beta_1},\hat{\boldsymbol\beta_2})$는 아래의 해 
\begin{align}
\begin{bmatrix} \bf X_2'X_2 & \bf X_2'X_1 \\\\ \bf X_1'X_2 & \bf X_1'X_1 \end{bmatrix} \begin{bmatrix} \boldsymbol{\hat\beta_2} \\\\ \boldsymbol{\hat\beta_1} \end{bmatrix} = \begin{bmatrix} \bf X_2' y \\\\ \bf X_1' y \end{bmatrix}
\end{align}
임을 상기하자. 위의 식의 양변에 $\begin{bmatrix} \bf I & \bf -X_2'X_1(X_1'X_1)^{-1} \\\\ \bf 0 & \bf I \end{bmatrix} $ 을 곱하여보자. 곱하여지는 매트릭스에서 특이한점은 $(1,2)$-th 원소, 즉 
\begin{align}
\bf -X_2'X_1(X_1'X_1)^{-1}
\end{align}
인데 이것을 잘 관찰하면 과정 (2) 에서 구해지는 coef 에서 transpose 를 취한 뒤 $-$ 를 붙였다는 것을 알 수 있다. 굳이 이런 term을 생각한것은 **$\bf X_1$과 과정 (2) 에서의 잔차 $\bf e_{X_2|X_1}$이 직교**한다는 사실, 즉 
\begin{align}
\bf X_1'(I-H_1)X_2 =0
\end{align}
을 이용하기 위해서다. 아무튼 $\bf X_1'(I-H_1)X_2 =0$를 잘 이용하면 위의 매트릭스는 아래와 같이 정리가능하다. 
\begin{align}
\begin{bmatrix} \bf X_2'(I-H_1)X_2 & \bf 0 \\\\ \bf X_1'X_2 & \bf X_1'X_1 \end{bmatrix} 
\begin{bmatrix} \hat{\boldsymbol\beta_2} \\\\ \hat{\boldsymbol\beta_1} \end{bmatrix} 
= \begin{bmatrix} \bf X_2'(I-H_1)y \\\\ \bf X_1'y \end{bmatrix}
\end{align}
따라서 증명이 끝난다. 


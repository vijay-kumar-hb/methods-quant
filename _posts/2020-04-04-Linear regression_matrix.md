---
layout: post
title: Linear regression
mathjax: true
tikz: yes
comments: true  
categories: methods, linear regression
---

<div style="display:none">
\(
  \def\<#1>{\left<#1\right>}
  \newcommand{\ddx}[2]{\frac{#1}{#2}}
  \newcommand{\CC}{\mathbf{C}}
  \newcommand{\bld}[1]{\boldsymbol{#1}}
  \newcommand{\hbld}[1]{\hat{\boldsymbol{#1}}}
  \newcommand{\textbf}[1]{\mathbf{#1}}
\)



# Introduction

We define a linear system where the output of the system is dependent linearly on some inputs. Let's consider the following system, 
here $x_1,x_2,...x_n$ are the inputs and $y$ is the output.
In a linear system, we know that the output is linearly dependent on the inputs, which implies that the inputs are scaled by some numbers and then results in an output. Hence in mathematical form, we can write the linear system as, 

$$\begin{eqnarray}
y(t) = \beta_0 + \beta_1 x_1(t) + \beta_2 x_2(t) + \cdots + \beta_k x_k(t) + \epsilon
\end{eqnarray}$$ 

where $\epsilon$ is the random noise that either the system or any other source related to the system generates, and $(t)$ signifies the time, which means the output at time $t$ depends on the inputs $i.e.$ $x_i$ at time $t$.  
Now the next challenge is to identify $\beta_i$ to know about the system, and we do this by $\textit{linear regression}$.  
# Formal representation
To start with, we formalize the notations to be used further.
As we have time dependent output $y(t)$, to present the $n$ instances of the outputs for given $n$ instances of each inputs $x_i$, we use the following matrix notation. 

$$\begin{eqnarray}
\textbf{y} = \begin{bmatrix}
y_1\\
y_2\\
\cdots\\
y_n\\
\end{bmatrix}, \textbf{X} = \begin{bmatrix}
\textbf{x}_1^T\\
\textbf{x}_2^T\\
\cdots\\
\textbf{x}_n^T\\
\end{bmatrix} = 
\begin{bmatrix}
1	&	x_{11}	&	x_{12}	&	\cdots	&	x_{1k}\\	
1	&	x_{21}	&	x_{22}	&	\cdots	&	x_{2k}\\	
1	&	\cdots	&	\cdots		&	\cdots	&	\cdots\\	
1	&	x_{n1}	&	x_{n2}	&	\cdots	&	x_{nk}\\	
\end{bmatrix}, \boldsymbol{\epsilon} = \begin{bmatrix}
\epsilon_1\\
\epsilon_2\\
\cdots\\
\epsilon_n
\end{bmatrix}, \beta = \begin{bmatrix}
\beta_0\\
\beta_1\\
\cdots\\
\beta_n\\
\end{bmatrix}
\end{eqnarray}$$ 

Hence, we can write the linear system as, 

$$\begin{eqnarray}\label{eq:regression}
\textbf{y} = \textbf{X}\boldsymbol{\beta} + \bld{\epsilon}
\end{eqnarray}$$  


# Regression parameter estimation

As it is not possible for us to know the regression parameters $\beta$ for the system, so to estimate these parameters we take some another variable $\hat{\beta}$ , and replace it with $\beta$  in Eq. \ref{eq:regression} and predict the output $\hat{\textbf{y}}$, i.e., 

$$\begin{eqnarray}\label{eq:y_hat}
\hbld{y} = \textbf{X} \hbld{\beta}
\end{eqnarray}$$ 

To approximate the regression parameters of unknown system, we have fix $\hat{\beta}$ such that the predicted $\hat{\textbf{y}}$ is closest to actual $\textbf{y}$. In order to do so, we define a term $\textbf{\textbf{e}}$ which is known residual term and mathematically written as, 

$$\begin{eqnarray}
\label{eq:residual}
\textbf{e} = \textbf{y} - \hat{\textbf{y}} 
\end{eqnarray}$$

So now the problem can identified as adjusting  $\hat{\boldsymbol{\beta}}$ that tries make $\textbf{e}$ zero or towards zero. Alternately we can define it as adjusting  $\hat{\boldsymbol{\beta}}$ such that  $\vert\vert\textbf{e}\vert\vert^2$ minimizes. $\vert\vert\cdot\vert\vert^2$ signifies the square of each element of $\bld{e}$. 

The values of $\hat{\boldsymbol{\beta}}$ that minimizes $\vert\vert\textbf{e}\vert\vert^2$ can be obtained by finding minima by differentiation. i.e.,

$$\begin{eqnarray}
\frac{\partial \vert\vert\textbf{e}\vert\vert^2}{\partial \hat{\boldsymbol{\beta}}} = \frac{\partial \textbf{e}^T \textbf{e}}{\partial \hat{\boldsymbol{\beta}}} = \frac{\partial (\textbf{y} - \hat{\textbf{y}})^T (\textbf{y} - \hat{\textbf{y}})}{\partial \hat{\boldsymbol{\beta}}} = 2 (\textbf{y} - \hat{\textbf{y}})^T \frac{\partial \hat{\textbf{y}}}{\partial \hat{\boldsymbol{\beta}}}
\end{eqnarray}$$

Further we know that, 

$$\begin{eqnarray}
\frac{\partial \hat{\textbf{y}}}{\partial \hat{\boldsymbol{\beta}}} = \frac{\partial \textbf{X} \hat{\boldsymbol{\beta}}}{\partial \hat{\boldsymbol{\beta}}} = -\textbf{X}
\end{eqnarray}$$

Hence we can further write, 

$$\begin{eqnarray}
\frac{\partial \vert\vert\textbf{e}\vert\vert^2}{\partial \hat{\boldsymbol{\beta}}} = -2 (\textbf{y} - \hat{\textbf{y}})^T \textbf{X}
\end{eqnarray}$$ 


We calculate the optimum value of $\bld{\beta}$ by taking first and second derivative of $\vert\vert\textbf{e}\vert\vert^2$ with respect to $\hbld{\beta}$, as shown below, 

$$\begin{eqnarray}
\frac{\partial}{\partial \hbld{\beta}} \frac{\partial \vert\vert\textbf{e}\vert\vert^2}{\partial \hbld{\beta}} = \textbf{X}^T \textbf{X}
\end{eqnarray}$$ 


As the second derivative will always be positive, hence we confirm that the value of $\hbld{\beta}$ obtain from first derivative would result in minimization of $\vert\vert\textbf{e}\vert\vert$.

Hence we can find $\hat{\boldsymbol{\beta}}$ that minimize $\vert\vert\textbf{e}\vert\vert^2$ as,

$$\begin{eqnarray}
& &-2 (\textbf{y} - \hat{\textbf{y}})^T \textbf{X} = 0 \nonumber \\
\Rightarrow & &
-2 (\textbf{y} - \textbf{X}\hat{\boldsymbol{\beta}})^T \textbf{X} = 0\nonumber \\
\Rightarrow & & \textbf{y}^T X =  \hat{\boldsymbol{\beta}}^T \textbf{X}^T \textbf{X}  \nonumber \\
\end{eqnarray}$$


Taking transpose of both sides and with little manipulation, we have, 

$$\begin{eqnarray}
\textbf{X}^T \textbf{X}  \hbld{\beta}  &= \textbf{X}^T\textbf{y} \nonumber \\ 
\Rightarrow \hbld{\beta}  &= (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T\textbf{y}  \nonumber \\
\end{eqnarray}$$


Now we can predict the values using the calculated parameter $\hbld{\beta}$ as, 

$$\begin{eqnarray}
\hat{\textbf{y}} &= \textbf{X}\hbld{\beta} \nonumber \\
&= \textbf{X} (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T\textbf{y}  \nonumber \\
&= \textbf{H} \textbf{y} 
\end{eqnarray}$$

where, $\textbf{H} = \textbf{X} (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T $

Further we can easily derive that $H = \textbf{H} \textbf{H}^T = \textbf{H}^T \textbf{H} $


Now the question is, does the above expression really tell us the actual values i.e. $\bld{\beta}$ ?

Let's find this. We plug Eq. \ref{eq:regression} into the above equation, 

$$\begin{eqnarray}
  \hat{\boldsymbol{\beta}}  = (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T(\textbf{X}\bld{\beta} + \bld{\epsilon})  = (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \textbf{X}\beta + (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \bld{\epsilon}
\end{eqnarray}$$

Or simply, 

$$\begin{eqnarray}
\hat{\boldsymbol{\beta}}  = \boldsymbol{\beta} + (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \bld{\epsilon}
\end{eqnarray}$$




This means that how close $\hat{\boldsymbol{\beta}}$ is to $\boldsymbol{\beta}$ depends on the noise $\bld{\epsilon}$. \\
It is interesting to note that the noise $\bld{\epsilon}$ is independent and identical or $\textit{i.i.d.}$ and follows normal distribution with certain variance \[how do we know thia ? well, we assume so!\]. Therefore any once element of noise vector i.e. $\epsilon_i$ can be written as,\\

$$\begin{eqnarray}
\epsilon_i \sim \mathcal{N}(0, \sigma^2)
\end{eqnarray}$$ 

Similarly $\bld{\epsilon}$ can be written in the form of multivariate normal distribution as,\\

$$\begin{eqnarray}
\bld{\epsilon} = \mathcal{N}(0, \sigma^2 \textbf{I})
\end{eqnarray}$$

Thus, since $\bld{\epsilon}$ follows a distribution, the  parameter $\hbld{\beta}$ must also follow the distribution. We must also note that we cannot directly measure $\bld{\epsilon}$ instead we can measure residual $\textbf{e}$ which can be calculated using Eq. \ref{eq:residual}. Nonetheless we can learn about $\bld{\epsilon}$ from $\textbf{e}$ as explained in the next section.

# Features of residual


Let's approximate it from error term or residuals, i.e. $\textbf{e}$. Let's write sum of squared of residual first in the following form, 

$$\begin{eqnarray}
\textbf{SSR} = \textbf{e}^T\textbf{e} &=& (\textbf{y} - \hat{\textbf{y}})^T (\textbf{y} - \hat{\textbf{y}}) \nonumber \\
&=& (\textbf{y} - \textbf{Hy})^T (\textbf{y} - \textbf{Hy}) \nonumber \\
& =& \textbf{y}^T \textbf{y} - \textbf{y}^T  \textbf{Hy} - \textbf{y}^T \textbf{H}^T \textbf{y} + \textbf{y}^T \textbf{H}^T \textbf{Hy} \nonumber
\end{eqnarray}$$

Since $\textbf{H}^T\textbf{H} = \textbf{H}$, thus we have, 

$$\begin{eqnarray}
\textbf{SSR} &=& \textbf{y}^T \textbf{y} - \textbf{y}^T  \textbf{Hy} - \textbf{y}^T \textbf{H}^T \textbf{y} + \textbf{y}^T  \textbf{Hy} \nonumber \\
&=& \textbf{y}^T(I-H)\textbf{y}   \nonumber \\
&=& (\textbf{X}\bld{\beta}+\bld{\epsilon})^T\textbf{M}(\textbf{X}\bld{\beta}+\bld{\epsilon}) \nonumber \\
&=& (\textbf{X}\bld{\beta}+\bld{\epsilon})^T\textbf{M}(\textbf{X}\bld{\beta}+\bld{\epsilon}) \nonumber \\
&=& (\bld{\beta}^T \textbf{X}^T+\bld{\epsilon}^T)\textbf{M}(\textbf{X}\bld{\beta}+\bld{\epsilon}) \nonumber \\
&=& (\bld{\beta}^T \textbf{X}^T \textbf{M}+\bld{\epsilon}^T \textbf{M})(\textbf{X}\bld{\beta}+\bld{\epsilon}) \nonumber \\
&=& \bld{\beta}^T \textbf{X}^T \textbf{M} \textbf{X}\bld{\beta} +\bld{\epsilon}^T \textbf{M} \textbf{X}\bld{\beta} + \bld{\beta}^T \textbf{X}^T \textbf{M} \bld{\epsilon} +\bld{\epsilon}^T \textbf{M} \bld{\epsilon} \nonumber
\end{eqnarray}$$

Further, it must be noted that 
$$\begin{eqnarray}
\textbf{M}\textbf{X} = \textbf{X} - \textbf{H}\textbf{X} = 0
\end{eqnarray}$$ 

Thus we can write, 
$$\begin{eqnarray}
\textbf{SSR} = \bld{\epsilon}^T \textbf{M} \bld{\epsilon}
\end{eqnarray}$$


Now we calculate the expected value of $\textbf{SSR}$ as,

$$\begin{eqnarray}
\mathtt{E}[\textbf{SSR}]=\mathtt{E}[\bld{\epsilon}^T \textbf{M} \bld{\epsilon}] = \mathtt{E}[\text{tr}(\bld{\epsilon}^T \textbf{M} \bld{\epsilon})] = \mathtt{E}[\text{tr}( \textbf{M} \bld{\epsilon} \bld{\epsilon}^T)] = \text{tr}( \textbf{M} \mathtt{E}[\bld{\epsilon} \bld{\epsilon}^T])
\end{eqnarray}$$

Since we know that $\mathtt{E}[\bld{\epsilon} \bld{\epsilon}^T)] = \sigma^2 \textbf{I} $ 

$$\begin{eqnarray}
\mathtt{E}[\textbf{SSR}] = \sigma^2 \text{tr}( \textbf{M})
\end{eqnarray}$$

Little maths tells us that $\text{tr}( \textbf{M}) = n-p$
Thus finally we have, 

$$\begin{eqnarray}
\mathtt{E}[\textbf{SSR}] = (n-p)\sigma^2  \nonumber
\end{eqnarray}$$ 
Hence we can say that, 
$$\begin{eqnarray}
\sigma^2 = \frac{\textbf{e}^T \textbf{e}}{n-p} =  \frac{\textbf{e}^T \textbf{e}}{n-p} = \frac{\textbf{SSR}}{n-p} \nonumber
\end{eqnarray}$$

Further we also write, 

$$\begin{eqnarray}\label{eq:sigm_hat}
\hat{\sigma}^2 = \frac{\textbf{SSR}}{n} = \frac{1}{n}\bld{\epsilon}^T \textbf{M} \bld{\epsilon}
\end{eqnarray}$$

Going back to the original problem, we can estimate $\Sigma$ from $\textbf{SSR}$ as shown below, 

$$\begin{eqnarray}
\Sigma = \sigma^2 (\textbf{X}^T \textbf{X})^{-1} = \frac{\textbf{SSR}}{n-k} (\textbf{X}^T \textbf{X})^{-1} = \frac{n\hat{\sigma}^2}{n-k} (\textbf{X}^T \textbf{X})^{-1} \nonumber
\end{eqnarray}$$



Further, with a little manipulation in Eq. \ref{eq:sigm_hat} and dividing both sides by $\sigma^2$ we have, 

$$\begin{eqnarray}
\frac{n\hat{\sigma}^2}{\sigma^2} = \bigg(\frac{\bld{\epsilon}}{\sigma} \bigg)^T \textbf{M} \bigg(\frac{\bld{\epsilon}}{\sigma}\bigg) \sim Z^T \textbf{M} Z = \chi^2_{n-p} \nonumber
\end{eqnarray}$$

where $Z$ is a standard normal distribution.


# Distribution of $\hat{\boldsymbol{\beta}}$

In order to represent the $\hbld{\beta}$ in distribution form, we calculate the two main parameters first i.e. mean and variance. 

## Expected value of $\hbld{\beta}$, $\mathtt{E}(\hat{\boldsymbol{\beta}})$


 $$\begin{eqnarray}
E[\hbld{\beta}] = E[\bld{\beta} + \textbf{H} \bld{\epsilon}] = E[\bld{\beta}] + E[\textbf{H} \bld{\epsilon}]
\end{eqnarray}$$ 
nointen
As we know, $E[\boldsymbol{\beta} ] = \boldsymbol{\beta}$, and $E[\textbf{H} \boldsymbol{\epsilon}] = \textbf{X}^T \textbf{X})^{-1} \textbf{X}^T E[\boldsymbol{\epsilon}] = 0$ 

## Variance of $\hat{\boldsymbol{\beta}}$

We calculate the variance from second moment as, 

$$\begin{eqnarray}
\mathtt{E}[\hat{\boldsymbol{\beta}} - \mathtt{E}[\boldsymbol{\beta} ]]^2 = \mathtt{E}[\hat{\boldsymbol{\beta}} - \boldsymbol{\beta}]^2 = \mathtt{E}[\textbf{H} \epsilon]^2
\end{eqnarray}$$

we can write it further as,

$$\begin{eqnarray}
\mathtt{E}[\textbf{H} \bld{\epsilon}]^2 &= \mathtt{E}[(\textbf{H} \bld{\epsilon})(\textbf{H} \bld{\epsilon})^T] \nonumber \\
& =  \mathtt{E}[\textbf{H} \bld{\epsilon} \bld{\epsilon}^T \textbf{H}^T] \nonumber \\
& = \textbf{H} \mathtt{E}[\bld{\epsilon} \bld{\epsilon}^T] \textbf{H}^T \nonumber \\
& = \textbf{H} \sigma^2 \textbf{I} \textbf{H}^T \nonumber \\
& = \sigma^2 \textbf{H} \textbf{H}^T \nonumber \\
&=\sigma^2 (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \textbf{X} (\textbf{X}^T \textbf{X})^{-1} \nonumber \\
\end{eqnarray}$$

Hence we have, 

 $$\begin{eqnarray}
\text{Var}(\hbld{\beta}) =  \sigma^2 (\textbf{X}^T \textbf{X})^{-1}
\end{eqnarray}$$ 


Thus we can write the distribution of $\hbld{\beta}$ as, 
 $$\begin{eqnarray}\label{eq:beta_hat}
\hbld{\beta} = \bld{\beta} + \textbf{H}\bld{\epsilon} \sim \mathcal{N}\big(\bld{\beta}, \sigma^2 (\textbf{X}^T \textbf{X})^{-1}\big)
\end{eqnarray}$$ 

#Hypothesis testing
From Eq. \ref{eq:beta_hat} we know that calculated parameter $\hbld{\beta}$ follows a distribution. But we want to know how probable is that the calculated parameter i.e. $\hbld{\beta}$ is close to actual parameter $\bld{\beta}$. 

Before doing so, let's do some maths magic. Let's write Eq. \ref{eq:beta_hat} as follows, 

$$\begin{eqnarray}
\hbld{\beta} \sim \mathcal{N} (\bld{\beta}, \Sigma)
\end{eqnarray}$$ 
where, $\Sigma = \sigma^2 (\textbf{X}^T \textbf{X})^{-1}$

We can transform the above distribution to zero mean as, 

 $$\begin{eqnarray}\label{eq:beta_hat_beta}
\hbld{\beta} - \bld{\beta} \sim \mathcal{N} (0, \Sigma)
\end{eqnarray}$$ 
Further we can standardize the distribution to unit variance as, 

$$\begin{eqnarray}
\Sigma^{-1/2}(\hbld{\beta} - \bld{\beta}) \sim \Sigma^{-1/2} \mathcal{N} (0, \Sigma) = \mathcal{N} (0, \Sigma^{-T/2} \Sigma \Sigma^{-1/2} ) = \mathcal{N} (0, \textbf{I} )
\end{eqnarray}$$
However, it must be noted that we still have a parameter unknown i.e. $\sigma^2$ in $\Sigma$. 

Since we know that estimated standard error for a single component $\beta_i$ can be written as, 
$$\begin{eqnarray}
\text{SE}_{\hat{\beta_i}}= \sqrt{\frac{n\hat{\sigma}^2}{n-k} (\textbf{X}^T \textbf{X})^{-1}_{ii}}
\end{eqnarray}$$

And we can write the distribution of individual $\beta_i$ parameter as,
$$\begin{eqnarray}
\hat{\beta_i} \sim \mathcal{N}\bigg(\beta_i, \sigma^2 (\textbf{X}^T \textbf{X})^{-1}_{ii} \bigg)
\end{eqnarray}$$

Further we can write it as, 
$$\begin{eqnarray}
\frac{\hat{\beta}_i- \beta_i}{\text{SE}_{\hat{\beta_i}}} = \frac{\frac{\hat{\beta}_i- \beta_i}{\sqrt{\sigma^2 (\textbf{X}^T\textbf{X})^{-1}_{ii}}}}{\frac{\text{SE}_{\hat{\beta_i}}}{\sqrt{\sigma^2 (\textbf{X}^T\textbf{X})^{-1}_{ii}}}}
\end{eqnarray}$$

Since we know that, 
$$\begin{eqnarray}
\frac{\hat{\beta}_i- \beta_i}{\sqrt{\sigma^2 (\textbf{X}^T\textbf{X})^{-1}_{ii}}} \sim \mathcal{N} (0, 1)
\end{eqnarray}$$
So we have,

$$\begin{eqnarray}
\frac{\hat{\beta}_i- \beta_i}{\text{SE}_{\hat{\beta_i}}} &\sim \frac{\mathcal{N}(0,1)}{\frac{\sqrt{\frac{n\hat{\sigma}^2}{n-k} (\textbf{X}^T \textbf{X})^{-1}_{ii}}}{\sqrt{\sigma^2 (\textbf{X}^T\textbf{X})^{-1}_{ii}}}} \nonumber \\
&\sim \frac{\mathcal{N}(0,1)}{\sqrt{\frac{n\hat{\sigma}^2}{\sigma^2}\frac{1}{n-k} }} \nonumber \\
&\sim \frac{\mathcal{N}(0,1)}{\sqrt{\frac{\chi^2_{n-k}}{n-k} }} \nonumber \\
& \sim \mathtt{t}_{n-k} \nonumber \\
\end{ eqnarray } $$


where $\mathtt{t}_{n-k}$ is the $\mathtt{t}$ distribution with $n-k$ degree of freedom.\\
Thus we conclude that $\mathtt{t}_{n-k}$  tells us the probability of obtaining different values of $\frac{\hat{\beta}_i- \beta_i}{\text{SE}_{\hat{\beta_i}}}$. Intuitively, $\mathtt{t}_{n-k}$ values tells us that what is the probability that the given value of $\hat{\beta}_i$ belongs to a distribution which is generated from system that has a regression parameter $\beta_i$. 
<br />

In this context, we formulate the following hypotheses, 

[$\textbf{H0}$] The regression parameter $\beta_i = 0$. Also known as $\textit{null}$ hypothesis. Intuitively, we state that the regression parameter that we have approximated i.e. $\hat{\beta}_i$ belongs to a population or system which as a regression parameter $\beta_i$ and $\beta_i=0$.

[$\textbf{H1}$] The regression parameter $\beta_i \neq 0$. Also known as $\textit{alternate}$ hypothesis. Intuitively, we state that the regression parameter that we have approximated i.e. $\hat{\beta_i}$ belongs to a population or system which as a regression parameter $\beta_i$ and $\beta_i \neq 0$.<br />
 
In our analysis, we try to prove null hypothesis. If we succeed in doing so, we conclude that the regression parameter is zero. Otherwise, we conclude that the regression parameter is $\textit{not}$ zero.  A line of precaution here. As mentioned previously, $\mathtt{t}$ distribution tells the probability of $\hat{\beta}_i$ to belong to a system which has a regression parameter $\beta_i$, and since it is composed of normal distribution and $\chi^2$ distribution, there will always be certain non-zero probability that $\hat{\beta}_i$ belongs to $\beta_i$. So we can never conclude that any possible value of $\beta_i$ is does not belong to a population of system which has regression parameter $\beta_i$, which is $0$ in case of null hypothesis. Therefore, to avoid such situation, we restrict our analysis to a given probability $\alpha$ i.e. if there is probability of $\hat{\beta}_i$ to belong to $\beta_i$ is more than $\alpha$, then $\textit{null}$ hypothesis is true, otherwise if the probability is lower than $\alpha$, we reject the null hypothesis and accept the alternate hypothesis i.e. $\beta_i \neq 0$. In management literature the most used level of $\alpha$ is 0.95. Therefore if $\frac{\hat{\beta}_i- \beta_i}{\text{SE}_{\hat{\beta}_i}}$ is less than the critical value of $\mathtt{t}_{n-p}$ for $\alpha=0.95$, then we accept the null hypothesis. Otherwise we accept the alternate hypothesis. 

#Predictions
In the previous section we concluded that the regression parameters $\hbld{\beta}$ follows some distributions. As we predict the output using $\hbld{\beta}$ i.e. using Eq. \ref{eq:beta_hat}, the predictions should also some distribution.    Hence the predicted values $\hat{\textbf{y}}$ are not fixed, rather follow a distribution. Let's consider that we want to predict the values for $\textbf{X}^*$, as given below, 

 $$\begin{eqnarray}
\hat{\textbf{y}}(\textbf{X}^*) &= \textbf{X}^* \hat{\boldsymbol{\beta}} \nonumber \\
& =  \textbf{X}^* (\bld{\beta} + \textbf{H}\bld{\epsilon}) \nonumber \\
& = \textbf{X}^* \bld{\beta} + \textbf{X}^*\textbf{H}\bld{\epsilon} \nonumber \\
\end{eqnarray}$$ 

Now we calculate the expected value of $\hat{\textbf{y}}(\textbf{X}^*)$ as,
 $$\begin{eqnarray}
\mathtt{E}[\hat{\textbf{y}}(\textbf{X}^*)] = \mathtt{E}[\textbf{X}^*\bld{\beta}] + \mathtt{E}[\textbf{X}^*\textbf{H}\bld{\epsilon}] = \textbf{X}^*\bld{\beta} + \textbf{X}^*\textbf{H}\mathtt{E}[\bld{\epsilon}]  = \textbf{X}^*\bld{\beta}
\end{eqnarray}$$ 
This is because  $\mathtt{E}(\bld{\epsilon}) = 0$

Further we calculate the variance as,
 $$\begin{eqnarray}
\text{Var}(\hat{y}(\textbf{X}^*)) = \mathtt{E}[\hat{y}(\textbf{X}^*) - \mathtt{E}[\hat{y}(\textbf{X}^*)]]^2 = \mathtt{E}[\textbf{X}^* \boldsymbol{\beta} + \textbf{X}^* \textbf{H} \epsilon - \textbf{X}^*  \boldsymbol{\beta}]^2
\end{eqnarray}$$ 


Thus we can write the variance in simplified form as, 
 $$\begin{eqnarray}
\text{Var}(\hat{y}(\textbf{X}^*)) &=  \mathtt{E}[ \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \bld{\epsilon} ]^2 \nonumber \\
 &=  \textbf{E}[ \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \epsilon (\textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \epsilon)^T ] \nonumber \\
& =  \textbf{E}[ \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \epsilon \epsilon^T \textbf{X}  (\textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^{*T}]   \nonumber \\
\end{ eqnarray } $$


 $$\begin{eqnarray}
\text{Var}(\hat{y}(\textbf{X}^*)) =  \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^T \textbf{E}[ \epsilon \epsilon^T] \textbf{X}  ( (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^{*T}
\end{eqnarray}$$ 

Since $\textbf{E}( \bld{\epsilon} \bld{\epsilon}^T) = \sigma^2 \textbf{I}$,

 $$\begin{eqnarray}
\text{Var}(\hat{y}(\textbf{X}^*)) =  \sigma^2 \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^{*T}
\end{eqnarray}$$ 

Thus we can write the distribution of predicted values as, 

 $$\begin{eqnarray}
\hat{y}(\textbf{X}^*) \sim \mathcal{N}\big( \textbf{X}^* \bld{\beta}, \sigma^2 \textbf{X}^* (\textbf{X}^T \textbf{X})^{-1} \textbf{X}^{*T} \big)
\end{eqnarray}$$ 


We can easily calculate that, 

 $$\begin{eqnarray}
\frac{\hat{y}(\textbf{x}_i^{T*}) - \textbf{x}_i^{T*}\beta}{\text{SE}_{\hat{y}}} \sim \mathtt{t}_{n-p}
\end{eqnarray}$$ 

where $\text{SE}_{\hat{y}} = \hat{\sigma} \sqrt{\textbf{x}_i^{T*} (\textbf{X}^T \textbf{X})^{-1}\textbf{x}_i^{*}}$

From $\mathtt{t}$ distribution, we can easily calculate the range that there is a certain probability that $\hat{y}(\textbf{x}_i^{*T})$ belongs to the distribution which has mean of $ \textbf{x}_i^{T*}\beta$. Let's say $(\pm) \gamma$ is the range for which $\hat{y}(\textbf{x}_i^{*T})$ can vary on given probability level. Then we can calculate the actual range as, 
 $$\begin{eqnarray}
\hat{y}(\textbf{x}_i^{*T}) -\gamma \text{SE}_{\hat{y}} \leq \hat{y} \leq  \hat{y}(\textbf{x}_i^{*T}) +\gamma \text{SE}_{\hat{y}} 
\end{eqnarray}$$   

In other words, 

$$\begin{eqnarray}
\hat{y}(\textbf{x}_i^{*T}) -\gamma \hat{\sigma} \sqrt{\textbf{x}_i^{T*} (\textbf{X}^T \textbf{X})^{-1}\textbf{x}_i^{*}} \leq \hat{y} \leq  \hat{y}(\textbf{x}_i^{*T}) +\gamma \hat{\sigma} \sqrt{\textbf{x}_i^{T*} (\textbf{X}^T \textbf{X})^{-1}\textbf{x}_i^{*}} 
\end{eqnarray}$$ 

# Example
<br />
Consider an example of a supermarket, where we want to understand the consumer spending with respect to the time that the consumers spend in the supermarket and their education level. We have the data shown in <a href="#table_1">Table 1</a>. 


\begin{array}{|l|l|l|l|}
\hline
\textbf{Sr. no. }	& 	\textbf{Time spent}	&	\textbf{Year of education}	&	\textbf{Spending }\\
\hline
1 & 80 & 20 & 1260 \\
2 & 83 & 13 & 1275 \\
3 & 83 & 8 & 1275 \\
4 & 119 & 11 & 1875 \\
5 & 89 & 19 & 1395 \\
6 & 99 & 11 & 1515 \\
7 & 101 & 15 & 1545 \\
8 & 116 & 17 & 1770 \\
9 & 103 & 11 & 1575 \\
10 & 86 & 13 & 1320 \\
11 & 104 & 10 & 1590 \\
12 & 104 & 12 & 1620 \\
13 & 92 & 15 & 1410 \\
14 & 81 & 14 & 1245 \\
15 & 118 & 16 & 1800 \\
16 & 119 & 16 & 1815 \\
17 & 103 & 20 & 1605 \\
18 & 104 & 18 & 1590 \\
19 & 97 & 9 & 1485 \\
20 & 117 & 14 & 1785 \\
\hline
\textbf{mean}	&	99.9 & 14.1	&	1537.5\\
\end{array}
<a name="#table_1">Table 1</a> Supermarket data (fictitious).



We can write the data shown in <a href="#table_1">Table 1</a> in the following form.
 \begin{equation*}
\textbf{X} = \begin{bmatrix}
1 & 80 & 20 \\
1 & 83 & 13 \\
1 & 83 & 8 \\
1 & 119 & 11 \\
1 & 89 & 19 \\
1 & 99 & 11 \\
1 & 101 & 15 \\
1 & 116 & 17 \\
1 & 103 & 11 \\
1 & 86 & 13 \\
1 & 104 & 10 \\
1 & 104 & 12 \\
1 & 92 & 15 \\
1 & 81 & 14 \\
1 & 118 & 16 \\
1 & 119 & 16 \\
1 & 103 & 20 \\
1 & 104 & 18 \\
1 & 97 & 9 \\
1 & 117 & 14 \\
\end{bmatrix}, \textbf{y} = \begin{bmatrix}
1260 \\
1275 \\
1275 \\
1875 \\
1395 \\
1515 \\
1545 \\
1770 \\
1575 \\
1320 \\
1590 \\
1620 \\
1410 \\
1245 \\
1800 \\
1815 \\
1605 \\
1590 \\
1485 \\
1785 \\
\end{bmatrix}, \textbf{X}^T\textbf{X} = \begin{bmatrix}
20 & 1998 & 282\\
1998 & 202988 & 28207\\
282 & 28207 & 4218\\
\end{bmatrix}
\end{equation*} 

 \begin{equation*}
(\textbf{X}^T\textbf{X})^{-1} = 
\begin{bmatrix}
  3.70e+00 &  -2.89e-02 &  -5.41e-02 \\
 -2.89e-02 &   2.96e-04 &  -4.30e-05 \\
 -5.41e-02 &  -4.30e-05 &   4.14e-03 \\
 \end{bmatrix}
\end{equation*} 

Now we calculate $\hbld{\beta}$ as, 

 $$\begin{eqnarray}
\hbld{\beta} = (\textbf{X}^T\textbf{X})^{-1}\textbf{X}^T \textbf{y} = \begin{bmatrix}
12.70 \\
15.12 \\
1.02 \\
\end{bmatrix}
\end{eqnarray}$$ 

\begin{array}{|r|r|r|r|r|r|}
\hline
\textbf{Sr. no.}	&	\textbf{AS} (y_i)	&	\textbf{PS} (\hat{y_i})	&	\textbf{Residual} (e_i)	&	CI(-95\%)	&	CI(+95\%)\\
\hline
1 & 1260.00 & 1242.69 & 17.31 & 1239.85 & 1280.15 \\
2 & 1275.00 & 1280.87 & -5.87 & 1261.80 & 1288.20 \\
3 & 1275.00 & 1275.74 & -0.74 & 1256.20 & 1293.80 \\
4 & 1875.00 & 1823.09 & 51.91 & 1858.99 & 1891.01 \\
5 & 1395.00 & 1377.73 & 17.27 & 1379.54 & 1410.46 \\
6 & 1515.00 & 1520.72 & -5.72 & 1504.35 & 1525.65 \\
7 & 1545.00 & 1555.05 & -10.05 & 1536.77 & 1553.23 \\
8 & 1770.00 & 1783.88 & -13.88 & 1755.89 & 1784.11 \\
9 & 1575.00 & 1581.19 & -6.19 & 1564.13 & 1585.87 \\
10 & 1320.00 & 1326.22 & -6.22 & 1308.17 & 1331.83 \\
11 & 1590.00 & 1595.28 & -5.28 & 1577.38 & 1602.62 \\
12 & 1620.00 & 1597.33 & 22.67 & 1610.33 & 1629.67 \\
13 & 1410.00 & 1418.99 & -8.99 & 1400.43 & 1419.57 \\
14 & 1245.00 & 1251.66 & -6.66 & 1230.98 & 1259.02 \\
15 & 1800.00 & 1813.09 & -13.09 & 1785.83 & 1814.17 \\
16 & 1815.00 & 1828.21 & -13.21 & 1800.36 & 1829.64 \\
17 & 1605.00 & 1590.41 & 14.59 & 1589.28 & 1620.72 \\
18 & 1590.00 & 1603.48 & -13.48 & 1577.86 & 1602.14 \\
19 & 1485.00 & 1488.43 & -3.43 & 1470.83 & 1499.17 \\
20 & 1785.00 & 1795.93 & -10.93 & 1771.86 & 1798.14 \\
\hline
\end{array}
<a name="#table_2">Table 2</a> Actual and predicted outputs. (AS: Actual spending, PS: Predicted spending).


Based on $\hbld{\beta}$ we predict the output using Eq. \ref{eq:beta_hat} as shown in Table \ref{table:table_2}. 
Now we calculate $\hat{\sigma}^2$ using the data from  <a href="#table_2">Table 2</a>  as shown below, 

 $$\begin{eqnarray}
\hat{\sigma}^2 = \frac{1}{20} \textbf{e}^T\textbf{e} = 263.48 \nonumber \\
\end{eqnarray}$$ 

and 
 \begin{eqnarray}
& &\sqrt{\frac{n}{n-p}\hat{\sigma}^2 (\textbf{X}^T\textbf{X})^{-1}} = \sqrt{\frac{20}{20-3} \times 263.48 \times (\textbf{X}^T\textbf{X})^{-1}} \nonumber \\
&=&\sqrt{\frac{20}{20-3} \times 263.48 \times \begin{bmatrix}
  3.70e+00 &  -2.89e-02 &  -5.41e-02 \\
 -2.89e-02 &   2.96e-04 &  -4.30e-05 \\
 -5.41e-02 &  -4.30e-05 &   4.14e-03 \\
\end{bmatrix}} \nonumber \\
\end{eqnarray} 


So we have 
 \begin{equation*}
\text{SE}_{\hat{\beta}_0} = \sqrt{\frac{20}{20-3} \times 263.48 \times (\textbf{X}^T\textbf{X})^{-1}_{00}} = 33.88
\end{equation*} 
 \begin{equation*}
\text{SE}_{\hat{\beta}_1} = \sqrt{\frac{20}{20-3} \times 263.48 \times (\textbf{X}^T\textbf{X})^{-1}_{11}} = 0.30
\end{equation*} 

 \begin{equation*}
\text{SE}_{\hat{\beta}_2} = \sqrt{\frac{20}{20-3} \times 263.48 \times (\textbf{X}^T\textbf{X})^{-1}_{22}} = 1.13
\end{equation*} 

So finally following the null hypothesis i.e. $\beta_i=0$ we have, 
 \begin{equation*}
\frac{\hat{\beta}_0-\beta_0}{\text{SE}_{\hat{\beta_0}}} = \frac{\hat{\beta}_0}{\text{SE}_{\hat{\beta}_0}} = \frac{12.90}{33.88} = 0.37
\end{equation*} 
Similarly we can derive, 

$$\begin{eqnarray}
\frac{\hat{\beta}_1}{\text{SE}_{\hat{\beta}_1}} = \frac{15.12}{0.30} &= 49.94 \nonumber \\
\frac{\hat{\beta}_2}{\text{SE}_{\hat{\beta}_2}} = \frac{1.02}{1.13} &= 0.90 \nonumber \\
\end{eqnarray}$$ 


From standard $\mathtt{t}$ table, the critical value for $\alpha=0.95$ is $2.1098$. Since $\frac{\hat{\beta}_0}{\text{SE}_{\hat{\beta}_0}} < \alpha$ and $\frac{\hat{\beta}_2}{\text{SE}_{\hat{\beta}_2}} <\alpha$ we accept the null hypothesis for $\beta_0$ and $\beta_2$ and conclude that $\beta_0 = \beta_1 = 0$. On the other hand,  $\frac{\hat{\beta}_1}{\text{SE}_{\hat{\beta}_1}} > \alpha$, thus we fail to accept the null hypothesis, and conclude that $\beta_1\neq 0$.\\
Furthermore, the confidence interval of predicted values are shown in Table \ref{table:table_2}. \\
Interested readers can also find out the confidence interval for regression parameter as well.

$\mathbf{t}$

\end{document}

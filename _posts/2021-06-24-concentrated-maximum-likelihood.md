---
layout: post
title: Concentrated Maximum Likelihood
date: 2021-06-24 21:13:45 PDT
description: Concentrating the log-likelihood function with respect to one of the parameters.
---

<br> 

Usually, the maximum likelihood (ML) estimator for the population parameters $$\beta$$ and $$\sigma^2$$,  in the classical linear regression model($$Y_i = X_i\beta + \varepsilon_i$$), are derived directly. Alternatively, the ML estimators can be obtained by first “concentrating” the log-likelihood function with respect to one of the parameters. For example, concentrating the function with respect to $$\sigma^2$$ – this is a convenient approach for problems that contain variance terms. This means differentiating the log-likelihood function with respect to $$\sigma^2$$, solving the resulting first-order condition for $$\sigma^2$$ as a function of the data and the remaining parameters, and then substituting the result back into the original log-likelihood function. This yields the concentrated log-likelihood function. The ML estimator for $$\beta$$ can then be found my maximizing the concentrated log-likelihood function with respect to $$\beta$$. Here, I will demonstrate this process.

<br> 

* Deriving the ML estimator for $$\sigma^2$$ as a function of the data and the remaining parameters.
  
|           The probability density function[^1]  for the classical linear regression model, 
|           assuming $$Y_i \sim N(X_i\beta, \sigma^2)$$, is:
  
$$f(Y_i|X_i,\theta)=\frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{1}{2}\frac{(Y_i-X_i\beta)^2}{\sigma^2}}$$

|           From there I proceed to set up the (log) likelihood equation:

$$L(\theta|Y_N,X)=\prod_{i=1}^{N}f(Y_i|X_i,\theta)$$

$$ln[L(\theta|Y_N,X)]=\sum_{i=1}^Nln\left[f(Y_i|X_i,\theta)\right]$$

$$LL(\theta|Y_N,X)=\sum_{i=1}^Nln\left[\frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{1}{2}\frac{(Y_i-X_i\beta)^2}{\sigma^2}}\right]$$

$$LL(\theta|Y_N,X)=\sum_{i=1}^Nln\left(\frac{1}{\sqrt{2\pi\sigma^2}}\right)+\sum_{i=1}^Nln\left(e^{-\frac{1}{2}\frac{(Y_i-X_i\beta)^2}{\sigma^2}}\right)$$

$$LL(\theta|Y_N,X)=Nln\left(\frac{1}{\sqrt{2\pi\sigma^2}}\right)-\frac{1}{2}\frac{\sum_{i=1}^N(Y_i-X_i\beta)^2}{\sigma^2}$$

$$LL(\theta|Y_N,X)=Nln(1)-Nln\left(\sqrt{2\pi\sigma^2}\right)-\frac{1}{2\sigma^2}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\sigma^2\right)-\frac{1}{2\sigma^2}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

|           Now, I take a derivative of the log-likelihood function with respect to $$\sigma^2$$:

$$\frac{\partial LL}{\partial \sigma^2}=-\frac{N}{2}\frac{1}{\sigma^2}+\frac{1}{2\sigma^2\sigma^2}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

|           Finally, setting the derivative to zero and solving for $$\sigma^2$$:

$$-\frac{N}{2}\frac{1}{\sigma^2}+\frac{1}{2\sigma^2\sigma^2}\sum_{i=1}^N(Y_i-X_i\beta)^2=0$$

$$\frac{-\sigma^2N+\sum_{i=1}^N(Y_i-X_i\beta)^2}{2\sigma^2\sigma^2}=0$$

$$-\sigma^2N=-\sum_{i=1}^N(Y_i-X_i\beta)^2$$

$$\sigma^2=\frac{1}{N}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

<br> 

* Using the result from previous part, I will derive the concentrated log-likelihood function. 

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\sigma^2\right)-\frac{1}{2\sigma^2}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

|           Substituting in the result for $$\sigma^2$$:

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\frac{1}{N}\sum_{i=1}^N(Y_i-X_i\beta)^2\right)-\frac{1}{\frac{2}{N}\sum_{i=1}^N(Y_i-X_i\beta)^2}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\frac{1}{N}\sum_{i=1}^N(Y_i-X_i\beta)^2\right)-\frac{N}{2}$$

|           Switching to matrix form:

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left[\frac{1}{N}(Y_N-X\beta)^T(Y_N-X\beta)\right]-\frac{N}{2}$$

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left[\frac{1}{N}\left(Y_N^TY_N-2\beta^TX^TY_N+\beta^TX^TX\beta\right)\right]-\frac{N}{2}$$

<br> 

* Using the concentrated log-likelihood I derive the ML estimator for $$\beta$$.

|           First, I take a derivative of the log-likelihood function with respect to $$\beta$$:

$$\frac{\partial LL}{\partial \beta}=-\frac{N}{2}\frac{\frac{1}{N}\left(2X^TY_N+2X^TX\beta\right)}{\frac{1}{N}\left(Y_N^TY_N-2\beta^TX^TY_N+\beta^TX^TX\beta\right)}$$

$$\frac{\partial LL}{\partial \beta}=\frac{-N\left(X^TY_N+X^TX\beta\right)}{Y_N^TY_N-2\beta^TX^TY_N+\beta^TX^TX\beta}$$

|           Then, I set the derivative to zero and solve for $$\beta$$.

$$\frac{-N\left(X^TY_N+X^TX\beta\right)}{Y_N^TY_N-2\beta^TX^TY_N+\beta^TX^TX\beta}=0$$

$$X^TY_N+X^TX\beta\ = 0$$

$$X^TX\beta=X^TY_N$$

$$\widehat{\beta}_{MLE}=(X^TX)^{-1}X^TY_N$$

<br> 

* Using $$\widehat{\beta}$$ to adjust the ML estimator for $$\sigma^2$$ (from part a)).

$$\sigma^2=\frac{1}{N}\sum_{i=1}^N(Y_i-X_i\beta)^2$$

$$\sigma^2=\frac{1}{N}\left(Y_N-X\beta\right)^T\left(Y_N-X\beta\right)$$

$$\sigma^2=\frac{1}{N}\left(Y_N^TY_N-2\beta^TX^TY_N+\beta^TX^TX\beta\right)$$

|           Substituting in the answer for $$\beta$$:

$$\sigma^2=\frac{1}{N}\left[Y_N^TY_N-2\left((X^TX)^{-1}X^TY_N\right)^TX^TY_N+\left((X^TX)^{-1}X^TY_N\right)^TX^TX\left((X^TX)^{-1}X^TY_N\right)\right]$$

$$\sigma^2=\frac{1}{N}\left[Y_N^TY_N-2Y_N^TX\left((X^TX)^{-1}\right)^TX^TY_N+Y_N^TX\left((X^TX)^{-1}\right)^TX^TY_N\right]$$

$$\sigma^2=\frac{1}{N}\left[Y_N^TY_N-Y_N^TX\left((X^TX)^{-1}\right)^TX^TY_N\right]$$

|           Considering that $$\left(A^{-1}\right)^T = \left(A^T\right)^{-1}$$,

$$\widehat{\sigma^2}_{MLE}=\frac{1}{N}\left[Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N\right]$$

<br> 

* Now, I demonstrate that the order did not matter. That is, I show that the ML estimators of $$\sigma^2$$ and $$\beta$$ can be obtained by first concentrating with respect to $$\beta$$ and then maximizing the concentrated log-likelihood thereby obtained, with respect to $$\sigma^2$$.
  
$$\widehat{\beta}_{MLE}=(X^TX)^{-1}X^TY_N$$

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\sigma^2\right)-\frac{1}{2\sigma^2}\left(Y_N-X\beta\right)^T\left(Y_N-X\beta\right)$$

$$LL(\theta|Y_N,X)=-\frac{N}{2}ln(2\pi)-\frac{N}{2}ln\left(\sigma^2\right)-\frac{1}{2\sigma^2}\left[Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N\right]$$

$$\frac{\partial LL}{\partial \sigma^2}=-\frac{N}{2\sigma^2}+\frac{Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N}{2\sigma^2\sigma^2}$$

$$-\frac{N}{2\sigma^2}+\frac{Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N}{2\sigma^2\sigma^2}=0$$

$$\frac{Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N-\sigma^2N}{2\sigma^2\sigma^2}=0$$

$$Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N=\sigma^2N$$

$$\widehat{\sigma^2}_{MLE}=\frac{1}{N}\left[Y_N^TY_N-Y_N^TX(X^TX)^{-1}X^TY_N\right]$$

<br> 
<br> 

[^1]: the general form: $$f(x)=\frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{1}{2}\frac{(x-\mu)^2}{\sigma^2}}$$

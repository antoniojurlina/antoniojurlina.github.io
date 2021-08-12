---
layout: post
title: Nested Logit Reduction
date: 2021-06-22 14:32:45 PDT
description: Conditions under which Nested Logit reduces to Multinomial Logit.
---

<br> 

Recall that the choice probability under the nested logit model takes the form,

$$P_{ij}=P_{iB_k}\times P_{ij|B_k}$$

where $$P_{iB_k}$$ denotes the probability of person *i* choosing nest *k*

$$P_{iB_k}=\frac{e^{W_{ik}+\lambda_k\Phi_{ik}}}{\sum_{l=1}^{K}e^{W_{il}+\lambda_l\Phi_{il}}}$$

where the *inclusive value* takes the form

$$\Phi_{ik}=ln\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}$$

and

$$P_{ij|B_k}=\frac{e^{\frac{Y_{ij}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}$$

denotes the probability of person *i* choosing alternative *j* conditioned on choosing nest *k*.

<br> 

* Here, I use algebra to demonstrate that the nested logit model reduces to the multinomial logit model if $$\lambda_k=1$$ for all *k* - the alternatives within every nest are independent of each other. We start with the nested logit choice probability:
  
$$P_{ij}=P_{iB_k}\times P_{ij|B_k}$$

$$P_{ij}=\frac{e^{W_{ik}+\lambda_k\Phi_{ik}}}{\sum_{l=1}^{K}e^{W_{il}+\lambda_l\Phi_{il}}}\times\frac{e^{\frac{Y_{ij}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}$$

$$P_{ij}=\frac{e^{W_{ik}+\lambda_kln\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}}{\sum_{l=1}^{K}e^{W_{il}+\lambda_lln\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}}\times\frac{e^{\frac{Y_{ij}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}$$

*Note:* $$e^{x+cln(b)}=e^xe^{cln(b)}=e^xe^{lnb^c}=e^xb^c$$

$$P_{ij}=\frac{e^{W_{ik}}\left[\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}\right]^{\lambda_k}}{\sum_{l=1}^ke^{W_{il}}\left[\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_l}}\right]^{\lambda_l}}\times\frac{e^{\frac{Y_{ij}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{Y_{im}}{\lambda_k}}}\times\frac{e^{\frac{W_{ik}}{\lambda_k}}}{e^{\frac{W_{ik}}{\lambda_k}}}$$

$$P_{ij}=\frac{\left[\sum_{m\epsilon B_k}e^{\frac{W_{ik}+Y_{im}}{\lambda_k}}\right]^{\lambda_k}}{\sum_{l=1}^k\left[\sum_{m\epsilon B_k}e^{\frac{W_{il}+Y_{im}}{\lambda_l}}\right]^{\lambda_l}}\times\frac{e^{\frac{W_{ik}+Y_{ij}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{W_{ik}+Y_{im}}{\lambda_k}}}$$

*Note:* $$W_{ik}+Y_{ij}=V_{ik}$$
  
$$P_{ij}=\frac{\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_k}}\right]^{\lambda_k}}{\sum_{l=1}^k\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_l}}\right]^{\lambda_l}}\times\frac{e^{\frac{V_{ik}}{\lambda_k}}}{\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_k}}}$$

$$P_{ij}=\frac{e^{\frac{V_{ik}}{\lambda_k}}\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_k}}\right]^{\lambda_k-1}}{\sum_{l=1}^k\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_l}}\right]^{\lambda_l}}$$

If we set $$\lambda_k=1$$, we get
  
$$P_{im}=\frac{e^{V_{ik}}}{\sum_me^{V_{im}}}$$

which is the choice probability for the multinomial logit.
  
<br> 

* Then, I show that the nested logit model also reduces to the multinomial logit model if all the nests $$B_k$$ $$(\forall k)$$ are singletons, i.e., each choice alternative is contained in its own nest.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ site.baseurl }}/assets/img/nesting_choices.png">
    </div>
</div>
<div class="caption">
    Figure 1.
</div>

Consider a discrete choice model in which each nest contains one choice (Figure 1). This means that when looking at $$P_{ij}$$ as derived in part a), we can see that the within-nest summation, $$\sum_{m\epsilon B_k}$$, is actually only summing over one variable, rendering the summation symbol unnecessary. That is,
  
$$P_{ij}=\frac{e^{\frac{V_{ik}}{\lambda_k}}\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_k}}\right]^{\lambda_k-1}}{\sum_{l=1}^k\left[\sum_{m\epsilon B_k}e^{\frac{V_{im}}{\lambda_l}}\right]^{\lambda_l}}$$

reduces to
  
$$P_{ij}=\frac{e^{\frac{V_{ik}}{\lambda_k}}\left[e^{\frac{V_{im}}{\lambda_k}}\right]^{\lambda_k-1}}{\sum_{l=1}^k\left[e^{\frac{V_{il}}{\lambda_l}}\right]^{\lambda_l}}$$

$$P_{ij}=\frac{e^{\frac{V_{ik}}{\lambda_k}}\left[e^\frac{V_{ik}\lambda_k-V_{ik}}{\lambda_k}\right]}{\sum_{l=1}^{k}e^{V_{il}}}$$

$$P_{ij}=\frac{e^{\frac{V_{ik}}{\lambda_k}}e^{V_{ik}}e^{-\frac{V_{ik}}{\lambda_k}}}{\sum_{l=1}^{k}e^{V_{il}}}$$

$$P_{ik}=\frac{e^{V_{ik}}}{\sum_{l=1}^{k}e^{V_{il}}}$$

which is the choice probability for the multinomial logit.

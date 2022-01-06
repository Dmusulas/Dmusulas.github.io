---
title: Binomial probability problem solution
categories:
- Statistics
- Probability
layout: post
feature_image: "https://picsum.photos/2560/600?image=872"
---

## Pass exam problem
Let's say we have 50 questions and to pass we need to answer half of them correctly. Each questions has a 4 answers and our agent guesses at random  Let's assume that all guesses are independent events.

$$
\begin{align}
p &= 0.25 \\
N &= 50 \\
X &= 25
\end{align}
$$

Where $p$ is probability to guess correctly, $N$ amount of questions (or trials) and $X$ is how many trials do we need to guess correctly. Then we are trying to calculate:

$$
\begin{gather}
P(X \geq 25) \Rightarrow 1-P(X \leq 24)\\
P(X \geq 25) = 1 - \sum_{i=1}^{24}  \binom{50}{i} * 0.25^i * 0.75^{50-i}
\end{gather}
$$

```python
from scipy.stats import binom 

n = 50
p = 0.25
x = 24
# defining X values
k_values = list(range(n+1))
# obtaining the mean and variance 
mean, var = binom.stats(n, p)
# getting a distribution
dist = [binom.pmf(k, n, p) for k in k_values]
answer = 1 - binom.cdf(24,50, 0.25)

print(f'The probability to correctly guess half of the exam questions are approximately equal to {answer:.6%}')
```

    The probability to correctly guess half of the exam questions are approximately equal to 0.012251%


So we can see that posibility to pass exam by sheer luck is not great. Let's look how Probability mass function looks like.


```python
import matplotlib.pyplot as plt


plt.bar(k_values, dist)
plt.vlines(x, ymin= 0, ymax = 0.13, colors= "red")
plt.xlabel("Number of correct guesses")
plt.ylabel("Probability, p")
plt.show()
```


    
![png](/assets/post_images/Exam_binomial_4_0.png)
    


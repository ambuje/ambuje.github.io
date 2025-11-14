---
title: "Neural Networks and Deep Learning"
date: 2020-07-30
draft: false
summary: "The information in the article is based on the author’s understanding from Andrew Ng Deep learning course(Neural Networks and Deep Learning)."
tags: ["Deep Learning","Artificial Intelligence","Gradient Descent","Backpropagation","Activation Functions"]
categories: ["Machine Learning", "NLP"]
cover:
  alt: "Neural Networks and Deep Learning"
  caption: "Neural Networks and Deep Learning"
---
The information in the article is based on the author’s understanding from Andrew Ng Deep learning course(Neural Networks and Deep Learning).

Logistic Regression as a Neural Network
---------------------------------------

It is a supervised learning classification algorithm which is used to predict the output. Generally, it is a binary classification problem i.e all target values are 0 or 1. For example, classification whether the email is spam or not. There are many more types of logistic regression like multinomial, ordinal. We can think logistic regression as a one-layer neural network.

![Schematic of Logistic Regression as a Classifier](_attachments/1_Ig1Zj8jkneGMnekAkJg_Fg_17631067318934872.png)

Given **X** we want **ŷ** =**P(y→1|X)** (ŷ is the predicted value)
More formally, we want **ŷ** to be the probability of the chance that y is equal to 1 given the input features X.
Weights and biases are the learnable parameters of a machine learning model. If we have an input **X** and learnable parameters W and b how do we compute **ŷ**? One thing we could do is **ŷ =wᵗx + b,** but this would not work in this case. As we have a binary classification we want **ŷ** between 0 and 1. **wᵗ + b** could be much bigger than 1 or it could be negative as well. To tackle this situation we will put a sigmoid function(σ) in front of it.
**σ = 1/(1+e⁻ᶻ)
**Our final output will be **ŷ =σ(wᵗx + b).** The sigmoid function gives values between 0 and 1 which could be seen below

![Sigmoid Function](_attachments/1_xUdZsykcshCgIQjTL_k0-g_1763106731309392.png)

In simple terms, we can define the working of logistic regression as it takes an input, passes through the sigmoid function then returns an output of probability between 0 and 1. Now further we’ll talk about the cost function.

Logistic Regression Cost Function
---------------------------------

> _The loss function computes the error for a single training example; the cost function is the average of the loss function of the entire training set — Andrew Ng_

So why a loss/cost function is used?
**Loss/cost** function is a measure of how good a model is. It quantifies the error between the predicted and the actual value. (Let us suppose **L(loss) =ŷ -y**, ŷ=10, y=5 so our error is 5). To train parameters W and B we need to define the cost function. Our aim is to minimize the cost function to get our predicted value as close as the actual value.

**_L(ŷ,y) = -[ylogŷ + (1-y)log(1-ŷ)]_**

There is always a question that why are we using log loss as our loss function and not mean square error. You could use MSE as the loss function but in logistic regression, people don’t usually do this because when you come to learn the parameters, you find that the optimization problem becomes non-convex. So we end up with a problem of multiple local minima. For better understanding, you can refer to [**_this article_**](https://towardsdatascience.com/why-not-mse-as-a-loss-function-for-logistic-regression-589816b5e03c)**_._**

![Multiple Local minima](_attachments/1_TJbS_iiPjBHbVMmagpS6kQ_1763106732495602.gif)

Now we will define the **cost function** for logistic regression.

![captionless image](_attachments/1_LBuB4-0WXBLmk47LYUD1fA_17631067312852979.png)

Now the question arises how we can reduce the cost? For this, we’ll look into gradient descent which is an optimization algorithm.

Gradient Descent
----------------

The main aim of the gradient descent is to minimize the cost value J(W,b).

> **_By periodically applying the gradient descent to the weights, we will eventually arrive at the optimal weights that minimize the loss function and allow the neural network to make better predictions._**

We initialize W and b randomly and then apply an optimization algorithm until it converges i.e we find the global minima.

```
Repeat {
          w := w - α[dJ(W,b)/dw]
          b := b - α[dJ(W,b)/db] 
       }α is the learning rate
Here the derivative part is partial differentiation. We perofom partial differentiation.
```![Animation how optimization algorithm works](_attachments/1_ylftXlvvAQJwJKZYvSgUZw_1763106733419838.gif)

A lot of time there is confusion **why we compute derivative of cost function?** Instead, we could use-value of the loss function and update weights.
**Explanation:=** We calculate the derivative of the cost function because the derivative gives us the slope and the slope here contains information about the magnitude (and sign) with which we should update the weight parameters to minimise cost.

When learning about Gradient Descent a terms pop in known as Backpropagation and lot of new learner gets confused and spend hours to understand the difference between gradient descent and backpropagation.

> Back-propagation is the process of calculating the derivatives and gradient descent is the process of descending through the gradient, i.e. adjusting the parameters of the model to go down through the loss function

```
w := w - α[dJ(W,b)/dw]
Calculating dJ(W,b)/dw is known as backpropagation.
Backpropagation is a process in Gradient Descent.
```

In gradient descent, one is trying to reach the minimum of the loss function with respect to the parameters using the derivatives calculated in the back-propagation. Now I’ll **summarize** how neural networks work.
1. Input is fed and weights are randomly assigned.
2. The activation function provides the prediction, by using weights
3. The loss is calculated with the help of cost/loss function
4. The optimization functions such as gradient descent use the results of the cost/loss function to minimize the error by updating weights.

![captionless image](_attachments/1_L6zt1u2ucaCHJk581apxVQ_1763106731879819.png)

Hope you are now clear how neural networks work with a basic understanding of the terms mentioned above.

Logistic Regression Gradient Descent
------------------------------------

Here we’ll see how we can compute gradient descent for logistic regression. This part includes mathematics and the reader should have basic knowledge of chain rule and how partial derivative is calculated. The first task to compute the gradient descent is to calculate the derivative term which could be also termed as to calculate backpropagation.

```
**Chain Rule:=**               A B C , we want to calculate dc/da
             dc/da = (dc/db)*(db/da). This is known as chain rule.
```

z = wᵗx + b
ŷ=a=σ(z)
L(a,y)= _-[ylog(a) + (1-y)log(1-a)]_

![Computational Graph](_attachments/1_Wr86peqrx99UOjdjyLM4cQ_1763106731734756.png)

**Do not forget that we do partial derivation while doing back-propagation.**

```
For updation of weight.For w1
d(L(a,y))/dw1 = d(L(a,y)/da * d(a)/d(z) * d(z)/dw1 {Chain Rule}{refer the graph above}
Apply same for w2 and b.
```![Compute d(L(a,y))/dw1](_attachments/1_TpRG1SOoDvpkcH7t0Jf6VQ_1763106733099523.jpeg)

There might be confusion regarding the 3ʳᵈstep, it was not necessary to show the 3ʳᵈ step. To simplify the calculation 3ʳᵈ step has been shown.

After the 4ᵗʰ step, we will perform gradient descent.

```
We got the value of d(L(a,y))/dw1
Now, 
    w1 := w1 - α[dJ(W,b)/dw1] , will be performed. By this way we update the weights.
```

Follow the same procedure for calculating w2 and b.

Activation Function
-------------------

We use an activation function to bring the non-linearity in our model. The non-linearity helps to make the model complex. Some of the famous activation functions are relu, tanh, softmax, sigmoid. One of the popular choices of the activation function within the hidden layer is relu. The downside of both the sigmoid function and the tanh function is that if z is either very large or very small, then the gradient or the derivative or the slope of this function becomes very small. So if z is very large or z is very small, the slope of the function ends up being close to 0. And so this can slow down gradient descent. To know more about activation function one can refer to [**this**](https://towardsdatascience.com/everything-you-need-to-know-about-activation-functions-in-deep-learning-models-84ba9f82c253#:~:text=Simply%20put%2C%20an%20activation%20function,fired%20to%20the%20next%20neuron.) **article**. I found it good and according to me it has an easy understanding of activation function.

```
I will try to explain here the above mentioned downside of sigmoid activation function mathematically.
Sigmoid function = **g(z)=1/(1+e⁻ᶻ)**. When performing back-propogation we have to find derivative(partial differentiation) of this function(I have explained this above). 
**d/dz(g(z)) = g(z)[1-g(z)]** { If you are not fimiliar with differentiation just believe me :P}**g(z)=1/(1+e⁻ᶻ) 
1. If z is very large (Put z value in g(z) and try to imagine)
{
   g(z) = 1(Not equal but very close to 1)
   d/dz(g(z)) = g(z)[1-g(z)]
              = 1(1-1)=0
}****2. If z is very small 
{
   g(z) = 0 (Not equal but very close to 0)
   d/dz(g(z)) = g(z)[1-g(z)]
              = 0(1-0)=0
}**So here we say if z is very large or small, derivate of sigmoid activation function gives the value close to 0 which creates vanishing gradient problem. To read about this refer the article tagged in activation function.
```

Random Initialization of weights
--------------------------------

Weights should always be randomly initialized. If we always initialize weights by 0 in all hidden layer then after weight updation the weight matrix will be identical i.e all the rows will have the same value, which would be of no use. So we should always randomly initialize the weights so that our network could learn properly.

Why deep(big) Neural Networks?
------------------------------

It is often said a neural network should be deep enough so that it could learn properly. Have you wondered why should these be deep enough? In a lot of interviews, this question is asked. For example:
**1.** If we are building a face detector or face recognition system the first layer might act as an edge detector or feature detector. Then as we go deeper then it might detect parts of faces and finally, it detects the face. So intuitively, you can think of the earlier layers of the neural network as detecting simple functions, like edges and then composing them together in the later layers of a neural network so that it can learn more and more complex functions.

Conclusion
----------

In this blog, I have tried to explain the basic terminologies that are associated with neural networks. On top of it in this blog at a few places, I have tried to explain things mathematically so that the reader has a broader understanding of how neural network works.

Thanks for reading :). If it was helpful to you do not forget to give a clap :P
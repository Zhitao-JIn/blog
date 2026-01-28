Perceptron

definition p16,17

​	supervised learning p16

​	element in learning p3

​	function p8,9,13

​	example p4



idea 18,21

learning rule p24,25,27,30

linearly non-separable class p37

solution and alternative p39

## Definition

Perceptron is a classical linear classification supervised learning model. Usually it is combined by 4 elements: training data,

model parameter,cost function,learning rule. At first we prepare some training data with input and output, then the model only know x and the goal is to predict y by learning new patterns. A linear classifier can be realized by a Perceptron, a single formalized neuron.



### Training data

the training data have both input and output. the inputs have M free dimension but the free parameters of the model have always M+1 dimension with a bias more. Then after the prediction,the model produce a value y-bar, which would be compared with the y-true.

### Model

fw(x) is a model function with parameters w. Based on the training data we could get w_opt, which is used to predict the y-bar and we want these parameters are close to the true w. To reach that we usually design a cost function and evaluate the distance between y-true and y-bar.

### Function

the perceptron use
$$
h(x)=\sum_0^M w_jx_j+b 
$$
to calculate the pre-activation value.

Then use
$$
y'=sign(h(x))
$$
to get the result of classification.

Usually we call a plane separating hyperplane when
$$
h(x)=0
$$

### Learning rule

the main goal of learning rule is how to get the optimal w parameter.
$$
w_{opt}=argmin(cost(w))
$$
the cost function is
$$
cost=-\sum_{i\in M}y_ih(x_i) 
$$
M is the set of all wrong index. For the right samples the is no cost.

To realize this we could use Gradient Descent of Stochastic Gradient Descent.

for Gradient Descent we calculated partial derivative at first.
$$
\frac{\partial cost}{\partial w_j}=-\sum_{i \in M} y_ix_{i,j}
$$
then,
$$
w_j\leftarrow w_j+\eta\sum_{i \in M} y_ix_{i,j}
$$
and each time we need consider about all the training data.

But for SGD,we only consider about a little part of data. So it's quiet faster than GD.



### Linearly non-separable class

Think about this situation, the x has two dimensions x1,x2, we calculate the x1|x2 or x1^x2. It is impossible that we get a exact line in 2d. to achieve this goal,we need to rise up the dimensions. Or use basis functions kernel trick or neural networks. 

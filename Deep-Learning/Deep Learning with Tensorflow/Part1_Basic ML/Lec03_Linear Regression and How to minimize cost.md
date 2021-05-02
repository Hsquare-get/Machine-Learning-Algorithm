# Linear Regression and How to minimize cost

## Hypothesis and Cost

- Hypothesis
  $$
  H(x) = Wx + b
  $$

- Cost function
  $$
  cost(W, b) = (\Sigma_i^m(H(x_i) - y_i)^2) / m
  $$

<br/>

## What cost(W) looks like?

- Simplified Hypothesis
  $$
  H(x) = Wx
  $$

<img src="https://user-images.githubusercontent.com/64063767/116806529-92a27180-ab68-11eb-83e8-817912cdb2b1.png" alt="image" style="zoom:50%;" />

<br/>

## Gradient Descent Algorithm

- Minimize cost function
- Gradient Descent is used many minimization problems
- For a given cost function, cost(W, b), it will find W, b to minimize cost
- It can be applied to more general function: cost(w1, w2, ...)

<br/>

## How it works?

<img src="https://user-images.githubusercontent.com/64063767/116806746-ff6a3b80-ab69-11eb-861a-a25d5cc2014b.png" alt="image" style="zoom:50%;" />

| Partial Derivative for Updating Weight                       | Formal Definition                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://user-images.githubusercontent.com/64063767/116807203-d5664880-ab6c-11eb-9c87-0f58279ab737.png" alt="image" style="zoom:50%;" /> | <img src="https://user-images.githubusercontent.com/64063767/116807230-faf35200-ab6c-11eb-90aa-287327b826eb.png" alt="image" style="zoom:50%;" /> |

1. Start with initial guesses

   - Start at 0, 0 (or any other value)

   - Keeping changing W and b a little bit to try and reduce cost(W, b)

2. Each time you change the parameters, you select the gradient which reduces cost(W, b) the most possible
   - **The steeper the slope(gradient), the more it moves**

3. Repeat

4. Do so until you converge to a **local minimum**
5. Has an interesting property
   - Where you start can determine which minimum you end up

<br/>

## Convex Function

- **Depending on how W and b are initially set, it may not be possible to find the lowest in the whole**

  <img src="https://user-images.githubusercontent.com/64063767/116807347-abf9ec80-ab6d-11eb-9a3d-1362e9a4023e.png" alt="image" style="zoom:50%;" />

- **If Cost function is Convex function, Local minimum is equal to Global minimum**

  <img src="https://user-images.githubusercontent.com/64063767/116807543-b5378900-ab6e-11eb-9888-a233527986ac.png" alt="image" style="zoom: 50%;" />


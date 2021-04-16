# Scaling and Normalization

## Topics:
1. Scaling of Data
2. Data Normalization
3. Difference between Scaling and Normalization
4. Min-max scalar and Box-Cox Transformation

![image](https://user-images.githubusercontent.com/58979984/114996418-7215be80-9ebc-11eb-8b8a-d27e753763b4.png)

## Scaling of Data
- Variable scaling requires taking values that span a specific range and representing them in another range.
- The standard method is to scale variables to [0,1]
- This may introduce various distortions or biases into the data but the distribution or shape remains same. 
- Depending on the modeling tool, scaling variable ranges can be beneficial or sometimes even required

One way of doing this is:

### Linear Scaling Transform
- First task in this scaling is to determine the minimum and maximum values of variables.
- Then applying the transform:
<br/> (x - min{x1, xN}) / (max{x1, xN} - min{x1, xN}) <br/>
- This introduces no distortion to the variable distribution.
- Has a one-to-one relationship between the original and scaled values

### Out of Range Values
- In data preparation, the data used is only a sample of the population.
- Therefore, it is not certain that the actual minimum and maximum values of the variable have been discovered when scaling the ranges.
- If some values that turn up later in the mining process are outside of the limits discovered in the sample, they are called out-of-range values

![image](https://user-images.githubusercontent.com/58979984/114997163-30d1de80-9ebd-11eb-8330-6c2b72234e81.png)

### Dealing with Out of Range values
- After range scaling, all variables should be in the range of [0,1].
- Out-of-range values, however, have values like -0.2 or 1.1 which can cause unwanted behavior.

* *Solution 1: Ignore that the range has been exceeded.* *
- Most modeling tools have (at least) some capacity to handle numbers outside the scaling range.
- Important question to ask: Does this affect the quality of the model? 

* *Solution 2: Exclude the out of range instances.* *
- One problem is that reducing the number of instances reduces the confidence that the sample represents the population.
- Another problem: Introduction of bias. Out-of-range values may occur with a certain pattern and ignoring these instances removes samples according to a pattern introducing distortion to the sample.

* *Solution 3: Clip the out of range values* *
- If the value is greater than 1, assign 1 to it. If less than 0, assign 0.
- This approach assumes that out-of-range values are somehow equivalent with range limit values.
- Therefore, the information content on the limits is distorted by projecting multiple values into a single value. 
- This also introduces some bias.

* *Solution 4: Making room for out of range values**
- The linear scaling transform provides an undistorted normalization but suffers from out-of-range values.
- Therefore, we should modify it to somehow include also values that are out of range.
- Most of the population is inside the range so for these values the normalization should be linear.
- The solution is to reserve some part of the range for the out-of-range values.
- Reserved amount of space depends on the confidence level of the sample: 
e.g. - 98% confidence linear part is [0.01, 0.99]

* *Squashing the out of range values* *
- Now the problem reduces to fitting the out-of-range values into the space left for them.
- The greater the difference between a value and the range limit, the less likely any such value is found. 
- Therefore, the transformation should be such that as the distance to the range grows, the smaller the increase towards one or decrease towards zero.
- One possibility is to use functions of the form y =1/x and attach them to the ends of the linear part.

Its difficult to carry out the scaling in pieces depending on the nature of the data point.
We can do all of the above steps using one function called **Softmax scaling**

* *Softmax Scaling –* *
- The extent of the linear part can be controlled by one parameter.
- The space assigned for out-of-range values can be controlled by the level of uncertainty in the sample.
- Non identical values have always different normalized values. 
Softmax scaling is based on the logistic function:
<br/> y = 1 / (1 + e-x) <br/>
Where y is the scaled value and x is the input value.
- The logistic function transforms the original range of 
[-∞,∞] to [0,1] and also has a linear part on the transform

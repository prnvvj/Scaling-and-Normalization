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
          (x - min{x1, xN}) / (max{x1, xN} - min{x1, xN}) 
- This introduces no distortion to the variable distribution.
- Has a one-to-one relationship between the original and scaled values

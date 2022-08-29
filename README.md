# Impact-of-Optimizers
A practical outlook on the most popular optimizers used in deep learning
![image](https://user-images.githubusercontent.com/45424924/187142374-1c163e8c-701c-403b-af68-d52cf0481d40.png)

# Introduction
<p align="justify"> Ever wondered why a DNN fails to perform as high as expected when it comes to accuracy, especially when there are official or unofficial reports of experts and enthusiasts getting some top performance with the same network and on that same dataset you are using? I remember having hard times trying to wrap my head around the thoughts that my models just failed when it was expected to perform well. What causes this? In reality, there are lots of factors with varying levels of potential to impact the performance of your architectures. However, I’ll discuss just one in this article. This factor is “The choice of Optimization algorithm to use”. </p>

<p align="justify"> What is an optimizer? An optimizer is a function, or algorithm that is created and used for neural network attributes modification (i.e., weights, learning rates) for the purpose of speeding up convergence while minimizing loss and maximizing accuracy. DNNs use millions-billions of parameters, and you need the right weights to ensure that your DNN learns well from the given data while generalizing and adapting well for a good performance on unseen related data. </p>

<p align="justify"> Different optimization algorithms have been built over the years and some of these algorithms have advantages over the others, as well as their cons. Therefore, it is imperative to know the basics of these algorithms, as well as understand the problem being worked on so that we can select the best optimizer to work with. </p>

<p align="justify"> Furthermore, I noticed that a lot of researchers use the SGD-M (Stochastic Gradient Descent with Momentum) optimizer, but in the industry, Adam is favoured more. In this article, I will give brief high level descriptions on the most popular optimizers being used in the AI world. Actually, I had to do a number of experiments to see the difference between these optimizers and answer some questions I have about the use of these optimizers, as well as give clues on which optimizer is the best and when/how to use them based on my observations. </p>

# Results
<p align="justify"> For the basic experiments, I used LeNet and AlexNet on the CIFAR-10 dataset. I tried to compare the basic performances of the SGD, SGDM, Adagrad, RMSProp and Adam optimizers. Training the two networks using these optimizers for 50 epochs while using a learning rate of 1e-3 (and a momentum of 0.9 for the SGDM), I got the following results</p>

Loss:
|  Models |  SGD  |  SGDM | Adagrad | RMSProp |  Adam |
|:-------:|:-----:|:-----:|:-------:|:-------:|:-----:|
|  LeNet  | 1.259 | 0.635 |  1.449  |   0.63  | 0.605 |
| AlexNet | 0.926 | 0.016 |  0.005  |  1.174  | 0.116 |

Accuracy:
|  Models |  SGD  |  SGDM | Adagrad | RMSProp |  Adam |
|:-------:|:-----:|:-----:|:-------:|:-------:|:-----:|
|  LeNet  | 54.03 | 69.49 |  48.08  |  65.18  | 67.61 |
| AlexNet | 61.76 | 83.75 |  82.79  |   76.3  | 76.11 |

The full plots for the training and testing for all 50 epochs:

<img src="https://user-images.githubusercontent.com/45424924/187153890-d596b6ce-9aa4-4623-bb8d-f0c13b1c01d1.png" width="500">  <img src="https://user-images.githubusercontent.com/45424924/187153930-f74b5401-f593-45de-b65a-58647ae99f77.png" width="500">  <img src="https://user-images.githubusercontent.com/45424924/187153977-398ee546-cbf1-4041-8a28-937a1cb18e42.png" width="500">  <img src="https://user-images.githubusercontent.com/45424924/187154022-e95b30e4-1483-453e-96da-d9445aac9deb.png" width="500">

<!-- ![image](https://user-images.githubusercontent.com/45424924/187153890-d596b6ce-9aa4-4623-bb8d-f0c13b1c01d1.png)![image](https://user-images.githubusercontent.com/45424924/187153930-f74b5401-f593-45de-b65a-58647ae99f77.png)![image](https://user-images.githubusercontent.com/45424924/187153977-398ee546-cbf1-4041-8a28-937a1cb18e42.png)![image](https://user-images.githubusercontent.com/45424924/187154022-e95b30e4-1483-453e-96da-d9445aac9deb.png) -->

<p align="justify"> From the presented results, I thought that RMSProp and Adam were too poor when used with AlexNet (since RMSProp's loss was all over the place, and though Adam was stable, it wasn't converging). So, I tried decreasing their learning rates to 1e-5 and retrained them, and I got these much better results: </p>

<img src="https://github.com/Ti-Oluwanimi/Impact-of-Optimizers/blob/main/plots/ALEXNET%20-%20RMSPROP%20(1e-3)%20and%20RMSPROP%20(1e-5).png" width="500">  <img src="https://github.com/Ti-Oluwanimi/Impact-of-Optimizers/blob/main/plots/ALEXNET%20-%20RMSPROP%20(1e-3)%20and%20RMSPROP%20(1e-5)%20(1).png" width="500">  <img src="https://github.com/Ti-Oluwanimi/Impact-of-Optimizers/blob/main/plots/AlexNet%20-%20ADAM%20(1e-3)%20and%20ADAM%20(1e-5).png" width="500">  <img src="https://github.com/Ti-Oluwanimi/Impact-of-Optimizers/blob/main/plots/AlexNet%20-%20ADAM%20(1e-3)%20and%20ADAM%20(1e-5)%20(1).png" width="500">

# Conclusion
<p align="justify"> I also carried out more experiments (changed lr for SGD to 1e-1 on LeNet and got a much better result), but these experiments are not enough for standard conclusions. However, my observations from the few conducted experiments are listed below: </p>

<p align="justify"> SGD: Not Recommended! While it is sure to converge, it normally takes its time to learn. What the SGDM or Adam could learn in 50 epochs, the SGD will learn it in about 500 epochs. However, there is a good chance that you can get some decent results when you start with a big learning rate (i.e., 1e-1). You can also use if you have enough time to wait for convergence, else, stay away. </p>

<p align="justify"> SGDM: Recommended! This optimizer has given the best results in the experiments. However, it might not work well if the starting learning rate is low. Otherwise, it is converges fast, and also helps the model’s generalizability. Totally recommended! </p>

<p align="justify"> Adagrad: Recommended! From the experiments, it could be said that this optimizer is the worst to use especially when you are using a small model like LeNet on complex datasets. However, in deeper networks, it could give good results, but optimal performance isn’t guaranteed. </p>

<p align="justify"> RMSProp: Recommended! This optimizer has also given very good performance. When used with a lower learning rate, it could give better performances. Asides the performance, it’s converging speed is high, and we can see the reason why it is being used sometimes in production sectors (industry). </p>

<p align="justify"> Adam: Recommended! According to some experts, Adam learns all patterns including the noise in the train set, and therefore it is fast to converge. However, in the experiments above, we can see that it doesn’t converge as well as the SGDM, but it converges and learns fast. Also, I could bet that its performance on bigger datasets (which would of course contain more noise) will be better than the other optimizers discussed above. </p>

To reach me, or learn more about me, or have a chat, my contact details are listed [here](https://github.com/Ti-Oluwanimi/)

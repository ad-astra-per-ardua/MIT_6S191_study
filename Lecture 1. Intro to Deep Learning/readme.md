## Setting the learning rate.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/e7fe6a4a-c791-4cb3-89ef-3fabf05392b6)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/cec272d5-f4d3-4bb6-995a-1876ebf26cb1)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/3d4a93a9-a39e-4348-a4cf-6ad39b7b9478)

Loss fuction을 최적화 하는데는 필수적이지만, 어려운 작업일수있다. 
2번 사진 (Visualizing the loss landscape of neural nets)과 같이 landscape 자체가 매우 방대하기때문이다.
강의에서 loss값은 

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/f05d8f08-cd37-4590-b65f-73efef5bde78)

Predicted value와 Actual value의 Diff라고 정의했다. Actual vaule는 달라지지않으므로, 가변적인 요소는 Weight뿐이므로, Actual과 가깝게 Predicted 값을 만드는 weight를 찾아야한다.

<img width="364" alt="image" src="https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/00d4904c-175d-4388-8044-009b33a86fd4">

## Gradient Descent algorithm

다음은 Gradient Descent algorithm을 간략하게 시각화하여 optimizing 하는 과정을 나타낸것이다. 

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/3d7dc362-3bf7-41bd-afba-baad98dd82e5)

이를 Algorithm으로 표현하면 다음과 같다.
여기서 4번의 로직을 자세히보면, Computed gradient에 H(ETA)를 곱하여 사용하는데 ETA의 값에 따라 weight가 크게 혹은 작게 바뀔수있다.


![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/cbf2e867-31f1-43cb-aed7-9d5c651c92f4)

**Case 1** 처럼 **ETA를 너무 작게** 설정하면 어떠한 Value로 수렴하는데, 이것이 우리의 goal인 global minima인지, 아니면 단순한 local minima인지 알수없다. 

**On the contrary**, **ETA를 너무 크게** 설정하면 weight 변동폭이 unstable해져서 결국엔 발산(Diverge)하게되어서 
Gradient can actually Explode (실제로 한말) 할수도 있다.

그래서 우리의 목표는 local minima를 피하며, smoothly하게 global minima에 수렴하는 **Stable learning rates** 값을 찾아야한다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/11ae08f3-5729-447b-9c7b-dc87fed3e45d)


![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/b9ddc27f-a5e5-45ef-bfbc-44b1d7f146ec)


![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/599d0806-d104-417f-95c9-a71849df7647)


![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/3b260399-f3ef-4327-ab69-42d67a3133b3)

어떻게?
아이디어 1번 : 굉장히 많은 learning rates를 때려박고 제대로 작동하는 값을 찾을때까지 시도한다. (Brute force)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/1fd74e16-1fd4-4dee-86db-12f5f102b26b)

아이디어 2번 : landscape 상황에 따라 변하는 Adaptive learning rate를 설계한다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/659274b4-3604-4d88-9c18-7524f10e81ab)

Learning rate는 더 이상 fixed된 값이 아니고, 
- Gradiet size
- Learning velocity
- Particular weights
- Etc..
에 따라 변할수있다. 

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/9f50f9da-92d8-424f-a950-1c02af3b78d5)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/1429dde2-5251-464c-abf9-cd79ce596990)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/79af5ef1-7663-45d3-93eb-8e8448422e38)

Gradient Descent는 dataset의 모든부분을 계산하고, 합산하기때문에 computationally intensive to compute 해질수있다. 

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/2e109ffe-d928-4848-9d64-86c895f54ed7)

이에 대한 대안으로 **SGD(확률적 경사 하강법)**이 존재한다. 

전체 Dataset중 data point i를 선택하고
그에대한 gradient를 계산하고 
Weight를 update한다.

GD와 SGD의 loop 한번을 비교하면, 각각 계산된 gradient는 차이가 존재할수밖에 없지만, 계산이 빠르고 true gradient를 계산할때 더 좋다.


![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/aac1ca3a-6217-44bc-b127-c2085abf2936)

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/9632df42-f4c7-4203-85a6-a6d56ef3f79a)

More accurate estimation of gradient는 즉, 수렴을 더 smoother하게 하고, learning rate를 더 크게 만들수있다는것이다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/b86c46c1-8dae-4b8b-87a1-91104d6df375)

또한, 병렬화와 GPU를 이용하여 전체 문제의 해결속도도 눈에띄게 증가한다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/ae613b7f-3d57-4d34-a59d-d1244f7c1d20)

다음은 NN의 학습과정에서 Overfitting, 과적합의 문제에 대해 알아본다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/de9fda55-2b1b-4062-9b12-46e83a78f2a0)

**Underfitting은** model의 complexity가 높지않아, data를 학습하기에, capacity가 부족하다는것이고,

**OVerfitting은** 반대로, complexity가 너무 높아, training data에 대한 오차는 감소하지만, test data에 적용할 경우 오차가 증가한다.

결국 두 경우 모두 test data에 대해 제대로 일반화가 되지않는다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/40fb88b2-75d2-44ee-984c-93096dc5b7dc)

이 문제를 해결하기위해 **Regularization** 방법을 사용한다.

Regularization = Model이 학습때 너무 complex해지는걸 방지하는 training pipeline이다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/805a1bdc-a0fe-48b6-ab20-afd077815907)

이것을 하는이유는 Training data를 넘어, testing data까지 일반화를 하기위해 사용한다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/40f382df-9433-45b4-8586-2e97984f55cb)

Regularization의 첫번째 방법은 Dropout이 있다. 
이는 Training 과정동안, 임의로 50%의 activation neuron을 사용 중지하는것이다. 
이 방법을 사용하면, Neuron Network의 Capcity를 줄일수있고, 하나의 Neuron에 대한 높은 의존성의 문제를 방지할수있다.

![image](https://github.com/ad-astra-per-ardua/MIT_6S191_study/assets/50827253/cf54590b-496e-4a74-aadd-38c68e25fbae)\

두번째 방법은 **Early stopping**이다. 
이 방법은** Overfitting이 발생하기전**에 training을 **강제로 멈추는** 방법이다. 

그래프에서 볼수있듯, training data에 대한 loss는 줄어들지만, Testing data에 대한 loss는 증가하는걸 볼수있고, 이는 model이 Training Data에 **Overfitting** 하고있다는 뜻이된다.

그렇다고 너무 일찍 멈춰버리면, **Underfitting** 문제가 발생하므로 stop하는 chance를 잘 조율해야한다.


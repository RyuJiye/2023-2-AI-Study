DeepLearning Basic
=====================
### DL component
data, model, loss function, optimization and regularization
      
         

### Loss Function
  * Regression Task-> MSE
  * Classification Task->cross entropy
  * Probabilicstic Task -> MLE         
       

### Nonlinear Function   
* Activation Function으로 Nonlinear Function사용   
* Why?  Multi layer에서 신경망의 표현성을 높이기 위해 (선형함수는 아무리 쌓아도 선형함수임)
 
### Generalization
  * 학습된 모델이 새로운 데이터에 관해서도 잘 작동하도록 하는 것(일반화) 

  * Loss function = 0 이라고 해서 학습이 완벽히 되었다고 할 수 없음  
    why? 학습 데이터에 noise가 낀 outlier가 있기 때문   
   


  * 모델이 Train data에 과도하게 fit되어 있으면 일반화 성능이 떨어짐   
    -Train data 에 fitting된 정도: Under-fitting  <  Optimal Balance  < Over-fitting    


  * Generalization Gap = | Test error - Training error |    
  * Cross Validation
    * valid data: 학습이 잘 되고 있는지 확인하기 위해 사용하는 지표
    * 학습 후 Train data의 일부를 valid data로 사용
    * valid data가 편향되어있을 수 있으므로 매 학습 마다 valid data를 다르게 설정
  * Ensamble  
    * 여러 개의 분류 모델을 조합해서 성능을 향상시키는 방법   

    * Bagging: subset을 나누어 학습후 각가의 voting이나 averaging을 구함 (parallel)     

    * Boosting: 학습이 제대로 되지 않은 데이터들을 모아서 새로운 간단한 모델로 재학습(sequential)   
   
 * Regularization
   * 모델의 overfitting을 방지하기 위한 방법   

   * Early stopping    

   * Parameter norm penalty   
   NN의 prarameter가 과도하게 커지는걸 방지 -> 부드러운 함수 생성   

   * Data augmentation   
   -한정된 data로 다양한 data 생성   
   -data 특성에 따라 다른 기법 적용   
   -Mixup, Cutmix, Blur, Crop, Darker...     

   * Noise robustness  
   -이상치나 noise가 들어와도 크게 흔들리지 않음

   * Dropout   
     -NN에서 몇 개의 노드를 제외하고 학습   
     -Train에서만 적용, Test에서는ㄴ drop되는 노드 없이 모든 노드가 참여    

   * Label smoothing   
     -모델이 너무 확신을 가지지 않도록 도와주는 방법  
     -One-Hot Encoding은 과적합 초래   
     ex)  [0, 1, 0, 0] -> [0.025, 0.9, 0.025, 0.025]

### CNN

* CNN은 이미지의 공간 정보를 유지하며 학습   
  -width * height * depth(R,G,B)

* FNN은 인접 픽셀간의 상관관계가 무시되어 이미지를 벡터화하는 과정에서 정보손실 발생

* { Conv -> Activation function -> pooling } * n  -> FNN
* pooling   
  -network의 parameter 개수나 연산량을 줄이기 위해 input 공간정보를 유지하며 down sampling으로 size감소  
  -Max pooling, Average pooling

* convolution  
  -depth 차원을 변경하면서 NN를 깊게 쌓기   
  -filter depth = input  channel depth   
  -filter 개수 = output channel depth   
  -bias 개수 = filter 개수

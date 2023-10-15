# __Semantic Segmentaion__

## __Segmentaion__
 * 이미지의 픽셀 수준에서 각 픽셀이 어떤 의미를 갖는지 파악하는 task     
 * 자율주행, 의료 영상, 배경 블러 처리
 * 꼭 object가 아니더라도 class가 될 수 있음(ex. 인도, 하늘)     
 * 같은 class에 속하는 instance들을 구분하지 않음        
 * Instance Segmentation는 같은 class에 속하더라도 다른 instance면 다르게 분류       

    </br>

 ## __Fully Convoulution Network__ 
 * VGG16을 backbone으로 사용   [img](image.png)  
   * block = Conv*N + Max Pooling    
   * pretrained된 네트워크를 그대로 사용 가능   

 * VGG 네트워크의 FC Layer인 nn.Linear 부분을 Convolution으로 변경     
   * 위치 정보 보존
   * 임의의 입력 값에도 상관 없이 학습 가능(학습시 이미지의 H,W 가 달라져도 됨)       
      
 * Transposed Convolution을 이용해 Pixel Wise Prediction 수행
   * VGG16에서 max pooling을 5번 시행하여 사이즈가 작아짐   
     --> output을 input과 같은 크기로 늘려줘야함   
    
</br>

## __Upsampling__

* Unpooling [img](image-1.png)    

* Bilinear Interpolation
  * 1차원 선형보간 [img](image-2.png)  
  * 2차원 선형보간 [img](image-3.png)    

* __Transposed Convolution__  [img](https://docs-assets.developer.apple.com/published/42f58a063f/rendered2x-1591868569.png)
  * 원래의 input과 똑같은 resolution으로 unpsamling하는 것이 목적     

</br>   
   
## __FCN 성능 향상__
* Skip Connection  
  * VGG에서 convolution과 maxpooling을 여러번 거치면서 feature map 이 지나치게 coarse 해짐   
  * n개의 block을 skip 하여 output의 detail을 높임   



* DeconvNet [img](https://epos.myesr.org/posterimage/esr/ecr2020/154362/media/846024)
    * FCN의 한계   
      * 객체의 크기가 크거나 작은 경우에 예측을 잘 하지 못하는 문제
      * Object의 디테일한 모습이 사라지는 문제
    * 해결책 
      * DeconvNet 추가
      * Decoder는 Unpooling과 Transpose Convolution block을 반복    
</br>  
## Segmentation 평가 지표   
   * Pixel Accuracy [img](https://miro.medium.com/v2/resize:fit:1400/1*SBbNyohcD0ctm1Ita2TZJg.png)
   * Mean IOU: class별 IOU의 평균 
   * Frequency Weighted IOU: class별 분포를 고려하여 중요한 class에 높은 가중치를 둠   
   
     
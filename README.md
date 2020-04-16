# Instace Segmentation with Mask R-CNN

<img src="https://i.imgur.com/mjdas1m.png" width="100%"> 우리가 다룰 주제는 Instance Segmentation에서 탁월한 성능을 보인 Mask R-CNN이다.

<img src="https://i.imgur.com/uKB5l1D.png" width="100%"> 선정 배경은 Segmentation 분야에서 좋은 성능을 가지고 있는 모델을 찾아보다가 이 모델이 Object Detection과 Segmentation 에서 모두 좋은 성능을 보이고 있기 때문에 선정하게 되었다. 다뤄볼 순서는 다음과 같다. 먼저 Mask R-CNN이 무슨 모델인지, 그리고 문제점은 무엇인지 알아볼 것이다. 이후 U-net을 사용하여 Mask R-CNN의 변형된 모델을 제시할 것이다. 마지막으로 프로젝트에 대한 결론을 얘기하겠다.

<img src="https://i.imgur.com/m6FCCI0.png" width="100%"> 이 모델을 직관적으로 다음과 같이 이해할 수 있겠다. 우리가 해결하고자 하는 문제는 오른쪽 그림에 해당하는 Instance Segmentation으로써, 모든 객체를 다르게 인식하고 segmentation 또한 할 수 있어야 한다. 이를 해결하기 위한 접근은 다음과 같다. 단순하게 생각해서 기존 Faster R-CNN이 객체가 있을만한 곳의 BBox를 잡아서 해당 BBox내의 객체를 각각 Segmentation한다면? 이것이 바로 Mask R-CNN의 컨셉이다. 즉 Faster R-CNN의 'Can Separate'와 FCN의 'Can Segment'를 합친다면 그것이 바로 Mask R-CNN이다.

<img src="https://i.imgur.com/g8Cq3aV.png" width="100%"> Mask R-CNN의 구조를 구체적으로 살펴보자면 위의 그림과 같다. Mask R-CNN을 쉽게 정의하자면 Faster R-CNN + Binary Mask Prediction + FCN + RoI Align 이라고 할 수 있겠다. 주요한 개념들을 구체적으로 확인하고 싶다면 동일 repository 내의 [Mask R-CNN Report.ipynb](https://github.com/YoonSungLee/Mask-R-CNN-Project_AI-Innovation-Square/blob/master/Mask%20R-CNN%20Report.ipynb)을 참고하면 된다. 먼저 Backbone은 ConvNet 구조로써 Image를 input으로 받아서 feature map을 출력하는 역할을 하며, 흔히 ResNet101를 사용한다. 출력된 feature map을 RPN에 입력시키는데, RPN은 Region Proposal Network로써 BBox를 추출하는 역할을 Neural Network로 구성한 모델이다. 흔히 우리는 추출한 BBox를 RoI라고 한다. RoI의 full-name은 Region of Interest로써, 우리가 관심있어하는 영역 즉, 물체가 존재하는 영역을 의미한다. RPN에서 뽑아낸 RoI의 사이즈는 모두 다르기에 RoI Align을 통해 동일한 사이즈로 풀링시켜준다. RoI Align은 MaxPooling과 비슷한 개념이라고 생각하면 되는데, 기존의 RoI Pooling의 정보손실을 막기 위해 binary interpolation 기법을 사용한 방법이라고만 얘기해두겠다. 이후 RoI Align을 통과한 고정된 사이즈의 feature map을 가지고 Bbox Regression, Classification, Binary Mask Prediction을 수행한다. Bbox Regression은 Bounding Box를 잘 잡아주는 역할을 하고, Classification은 물체를 잘 분류시켜주는 역할을 하며, Binary Mask Prediction은 Bbox 내의 물체가 존재하는 부분만 segmentation을 해주는 역할을 한다. 이러한 end-to-end 모델을 통해 이미지를 학습하고 결과를 출력한다. 이제 다시 한 번 Mask R-CNN을 쉽게 정의해보겠다. 기존 Faster R-CNN에 FCN을 이용하여 Binary Mask Prediction을 수행하고, RoI Align으로 기존의 풀링방법보다 정보손실을 줄인 모델. 이것이 Mask R-CNN이다.

<img src="https://i.imgur.com/Iig45tj.png" width="100%">

<img src="https://i.imgur.com/COjGWvG.png" width="100%">

<img src="https://i.imgur.com/pupcT7Z.png" width="100%">

<img src="https://i.imgur.com/AnB9PfL.png" width="100%">

<img src="https://i.imgur.com/UpMNHmm.png" width="100%">

<img src="https://i.imgur.com/AdZiT9O.png" width="100%">

<img src="https://i.imgur.com/cuFfR6n.png" width="100%">

<img src="https://i.imgur.com/dUCmEmz.png" width="100%">

<img src="https://i.imgur.com/tRiHM77.png" width="100%">

<img src="https://i.imgur.com/n9yDMsV.png" width="100%">

<img src="https://i.imgur.com/ifuntaS.png" width="100%">

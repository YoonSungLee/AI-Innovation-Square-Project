# Instace Segmentation with Mask R-CNN

<img src="https://i.imgur.com/mjdas1m.png" width="100%"> 우리가 다룰 주제는 Instance Segmentation에서 탁월한 성능을 보인 Mask R-CNN이다.

<img src="https://i.imgur.com/uKB5l1D.png" width="100%"> 선정 배경은 Segmentation 분야에서 좋은 성능을 가지고 있는 모델을 찾아보다가 이 모델이 Object Detection과 Segmentation 에서 모두 좋은 성능을 보이고 있기 때문에 선정하게 되었다. 다뤄볼 순서는 다음과 같다. 먼저 Mask R-CNN이 무슨 모델인지, 그리고 문제점은 무엇인지 알아볼 것이다. 이후 U-net을 사용하여 Mask R-CNN의 변형된 모델을 제시할 것이다. 마지막으로 프로젝트에 대한 결론을 얘기하겠다.

<img src="https://i.imgur.com/m6FCCI0.png" width="100%"> 이 모델을 직관적으로 다음과 같이 이해할 수 있겠다. 우리가 해결하고자 하는 문제는 오른쪽 그림에 해당하는 Instance Segmentation으로써, 모든 객체를 다르게 인식하고 segmentation 또한 할 수 있어야 한다. 이를 해결하기 위한 접근은 다음과 같다. 단순하게 생각해서 기존 Faster R-CNN이 객체가 있을만한 곳의 BBox를 잡아서 해당 BBox내의 객체를 각각 Segmentation한다면? 이것이 바로 Mask R-CNN의 컨셉이다. 즉 Faster R-CNN의 'Can Separate'와 FCN의 'Can Segment'를 합친다면 그것이 바로 Mask R-CNN이다.

<img src="https://i.imgur.com/g8Cq3aV.png" width="100%"> Mask R-CNN의 구조를 구체적으로 살펴보자면 위의 그림과 같다. Mask R-CNN을 쉽게 정의하자면 Faster R-CNN + Binary Mask Prediction + FCN + RoI Align 이라고 할 수 있겠다. 주요한 개념들을 구체적으로 확인하고 싶다면 동일 repository 내의 [Mask R-CNN Report.ipynb](https://github.com/YoonSungLee/Mask-R-CNN-Project_AI-Innovation-Square/blob/master/Mask%20R-CNN%20Report.ipynb)을 참고하면 된다. 먼저 Backbone은 ConvNet 구조로써 Image를 input으로 받아서 feature map을 출력하는 역할을 하며, 흔히 ResNet101를 사용한다. 출력된 feature map을 RPN에 입력시키는데, RPN은 Region Proposal Network로써 BBox를 추출하는 역할을 Neural Network로 구성한 모델이다. 흔히 우리는 추출한 BBox를 RoI라고 한다. RoI의 full-name은 Region of Interest로써, 우리가 관심있어하는 영역 즉, 물체가 존재하는 영역을 의미한다. RPN에서 뽑아낸 RoI의 사이즈는 모두 다르기에 RoI Align을 통해 동일한 사이즈로 풀링시켜준다. RoI Align은 MaxPooling과 비슷한 개념이라고 생각하면 되는데, 기존의 RoI Pooling의 정보손실을 막기 위해 binary interpolation 기법을 사용한 방법이라고만 얘기해두겠다. 이후 RoI Align을 통과한 고정된 사이즈의 feature map을 가지고 Bbox Regression, Classification, Binary Mask Prediction을 수행한다. Bbox Regression은 Bounding Box를 잘 잡아주는 역할을 하고, Classification은 물체를 잘 분류시켜주는 역할을 하며, Binary Mask Prediction은 Bbox 내의 물체가 존재하는 부분만 segmentation을 해주는 역할을 한다. 이러한 end-to-end 모델을 통해 이미지를 학습하고 결과를 출력한다. 이제 다시 한 번 Mask R-CNN을 쉽게 정의해보겠다. 기존 Faster R-CNN에 FCN을 이용하여 Binary Mask Prediction을 수행하고, RoI Align으로 기존의 풀링방법보다 정보손실을 줄인 모델. 이것이 Mask R-CNN이다.

<img src="https://i.imgur.com/Iig45tj.png" width="100%"> 우리는 앞서 소개한 Mask R-CNN 모델을 직접 활용해보고 실제 데이터에 직접 적용시켜보기로 했다. 따라서 우리는 Github에서 matterport가 공개한 오픈소스를 활용하여 모델을 사용해보았다. 해당 모델은 ResNet101으로 backbone을, FPN으로 mask branch를 구성하였고, Image dataset으로 유명한 COCO dataset으로 pre-train되어있다. COCO dataset은 도로 위에서 볼 수 있는 물체(person, bicycle, car, bus, truck, stop sign), 동물(bird, cat, dog, horse, sheep), 음식(banana, apple, sandwich, pizza, cake), 식기류(bottle, wine glass, cup, fork, spoon), 집 안 가구(chair, couch, bed, TV, laptop, keyboard) 등 일상생활에서 볼 수 있는 80여 종의 물체들을 Bbox, Segmentation Masking 해 놓은 데이터셋이다. Object Detection와 Segmentation 분야에서 인기 있는 데이터셋이라 할 수 있겠다. 우리 팀이 할당받은 GPU는 GeForce RTX 2080 ti로써 메뉴얼에 맞게 해당 NVIDIA drive와 Anaconda, CUDA, CuDNN 등을 설치했다. 실습하면서 알게된 내용이 있는데, Anaconda prompt를 이용해서 tensorflow-gpu를 설치할 때에는 CUDA와 CuDNN이 이미 세팅되어있기 때문에 따로 설치할 필요가 없다. 이후 conda prompt에 접속해 가상환경을 만들어 준 다음 tensorflow,-gpu, keras 등 모델이 돌아가기 위한 여러 라이브러리들을 설치해줬는데, 이는 requirements.txt에 명시되어있으므로 이를 참고할 수 있다. 특히 이번기회에 가상환경이 무엇이고 왜 필요한지에 대해서 대략적으로 알 수 있었다. 추가적으로 경로 설정 및 환경 설정 등 코드를 돌리기 위한 조건들을 재설정해주었는데 이는 Youtube에 올라온 tutorial을 참고하면서 해결했다. 

<img src="https://i.imgur.com/COjGWvG.png" width="100%"> 이미 matterport의 repository 안에는 다른 임의의 테스트용 이미지들이 있어서 그것들을 통해 결과를 확인할 수 있다. 하지만 우리가 가지고 있는 데이터에 대하여 제대로 작동하는지 확인하기 위해 휴대폰 갤러리에 있는 사진을 모델에 집어넣어봤다. 그 결과는 위의 두 사진과 같다. Mask R-CNN은 각 객체에 대하여 Bounding Box를 잡아내고, 그 BBox 내에 어떤 물체가 있는지 분류해주며, 물체와 배경을 구분하여 Masking 해준다. 대강 확인해봤을때는 꽤 좋은 결과를 얻은 것처럼 보인다. 하지만 왼쪽 이미지에서 맨 왼쪽 사람의 Segmentation이 잘 되지 않는 현상, 오른쪽 이미지에서 우산을 연으로 잘못 분류하는 현상 등 아직까지는 최상의 결과를 보여주지는 못하고 있다는 것을 확인했다.

<img src="https://i.imgur.com/pupcT7Z.png" width="100%"> Mask R-CNN은 기존 R-CNN, Fast R-CNN이 사용하던 Selective Search 대신에 RPN을 사용하여 속도를 굉장히 많이 끌어올린 모델이다. 따라서 이 모델을 Real-time으로 적용이 가능한지 확인하기 위해 동영상도 모델에 넣어보았다. 해당 동영상은 내가 개인적으로 심심할 때 시청하는 '코기TV지훈' 유튜버의 영상이다. 일상생활에서 볼 수 있는 소재가 영상에 담겨 있어 이 영상을 선택해서 모델에 집어넣어보았고 결과는 다음과 같다. 이 영상의 원본 링크는 다음과 같다.<br>
[코기TV지훈](https://www.youtube.com/watch?v=yf4hcoMZZbw)

<img src="https://i.imgur.com/AnB9PfL.png" width="100%">

<img src="https://i.imgur.com/UpMNHmm.png" width="100%">

<img src="https://i.imgur.com/AdZiT9O.png" width="100%">

<img src="https://i.imgur.com/cuFfR6n.png" width="100%">

<img src="https://i.imgur.com/dUCmEmz.png" width="100%">

<img src="https://i.imgur.com/tRiHM77.png" width="100%">

<img src="https://i.imgur.com/n9yDMsV.png" width="100%">

<img src="https://i.imgur.com/ifuntaS.png" width="100%">

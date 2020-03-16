# Question

1. segmentation을 주제로 U-Net, M-Net, SegNet, DeepLab을 구현, 변형하고 모델의 성능을 비교하는 식의 프로젝트 진행에 대해서 어떻게 생각하시나요?

2. 모델에 학습시킬 input data의 shape이 모두 다른 상태입니다. ImagaDataGenerator를 통해 shape을 변형시켜 학습시킨다면 output data의 shape이 기존 input data의 shape과 다를것입니다. 그럼 input data와 (segmentation을 진행한) output data를 출력해보면 사이즈가 다른 그림이 출력될텐데 같은 사이즈로 보여줄 수 있는 방법은 무엇인가요?

3. 모델에 학습시킬 train set에는 총 80개의 instance가 존재합니다(한 장의 image당 3~4개의 instance 존재). U-net으로 모델링을 한다면 마지막 layer의 units을 배경 포함 81로 설정하는 것이 올바른 방법인가요?

4. 프로젝트를 진행하면서 Object Detection에 관한 개념이 필요할 수도 있을 것 같습니다. 혹시 이를 학습할 수 있을만한 자료나 경로를 알 수 있을까요?

# ToDo
**Goal: U-Net, M-Net, SegNet, DeepLab, 10Net(모델 변형) 구현 및 성능 비교**

1. U-Net, M-Net 구현

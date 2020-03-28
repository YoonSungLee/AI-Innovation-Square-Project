# Question

1. segmentation을 주제로 U-Net, M-Net, SegNet, DeepLab을 구현, 변형하고 모델의 성능을 비교하는 식의 프로젝트 진행에 대해서 어떻게 생각하시나요?

2. 모델에 학습시킬 input data의 shape이 모두 다른 상태입니다. ImagaDataGenerator를 통해 shape을 변형시켜 학습시킨다면 output data의 shape이 기존 input data의 shape과 다를것입니다. 그럼 input data와 (segmentation을 진행한) output data를 출력해보면 사이즈가 다른 그림이 출력될텐데 같은 사이즈로 보여줄 수 있는 방법은 무엇인가요?

3. 모델에 학습시킬 train set에는 총 80개의 instance가 존재합니다(한 장의 image당 3~4개의 instance 존재). U-net으로 모델링을 한다면 마지막 layer의 units을 배경 포함 81로 설정하는 것이 올바른 방법인가요?

4. 프로젝트를 진행하면서 Object Detection에 관한 개념이 필요할 수도 있을 것 같습니다. 혹시 이를 학습할 수 있을만한 자료나 경로를 알 수 있을까요?

# ToDo
**Goal: Mask R-CNN 논문 리뷰 및 구현**

1. Mask R-CNN 논문 리뷰
2. COCO dataset 불러오기

# etc.
1. 가상환경 구축
* 구축 경로로 이동
* conda create -n env_name: 가상환경 구축
* activate env_name: 가상환경 실행
* deactivate: 가상환경 종료
* conda env export > env_name.yaml: .yaml 파일로 저장
* conda env create -f env_name.yaml: .yaml파일로 새로운 가상환경 만들기
* conda env list: conda에 설치된 가상환경 리스트 출력
* conda env remove -n env_name: 가상환경 제거하기<br>
[참고] https://teddylee777.github.io/python/anaconda-%EA%B0%80%EC%83%81%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95-%ED%8C%81-%EA%B0%95%EC%A2%8C

3. GPU check
* tf.test.is_gpu_available()
* from tensorflow.python.client import device_lib<br>
print(device_lib.list_local_devices())

3. GPU install
* conda install -c anaconda tensorflow-gpu==1.14    # CUDA와 CuDNN을 스스로 

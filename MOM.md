# ToDo
**Goal: Mask R-CNN 논문 리뷰 및 구현**

1. Mask R-CNN 논문 리뷰
2. COCO dataset 불러오기
3. Mask R-CNN 구현

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

2. GPU check
* tf.test.is_gpu_available()
* from tensorflow.python.client import device_lib<br>
print(device_lib.list_local_devices())

3. GPU install
* conda install -c anaconda tensorflow-gpu==1.14    # CUDA와 CuDNN을 스스로 

4. conda prompt에서 가상환경 구축 시 유의점
* 가상환경 내에 conda install jupyter를 따로 해줘야한다. 설치하지 않아도 jupyter notebook을 실행할 수 있지만, tensorflow-gpu를 설치한 상태라도 GPU를 감지하지 못하는 사태 등 가상환경 내의 라이브러리들을 사용하지 못하는 현상이 발생할 수 있다. 따라서 가상환경 내에서 jupyter notebook을 따로 설치해주고, 그 외에 필요한 라이브러리들도 따로 설치해준다.

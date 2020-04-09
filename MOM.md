# ToDo
**Goal: Mask R-CNN 논문 리뷰 및 구현**

1. Mask R-CNN 논문 리뷰
2. COCO dataset 불러오기
3. Mask R-CNN 구현



# Reference Sites
[Object Detection] 1. Object Detection 논문 흐름 및 리뷰
* https://nuggy875.tistory.com/20

[Object Detection] 2. R-CNN : 딥러닝을 이용한 첫 2-stage Detector
* https://nuggy875.tistory.com/21

[Object Detection] 3. Fast R-CNN & Faster R-CNN 논문 리뷰
* https://nuggy875.tistory.com/33

[Machine Learning Academy_part V. Best CNN Architecture] 8. ResNet [5], Faster-RCNN
* https://blog.naver.com/PostView.nhn?blogId=laonple&logNo=220782324594

양우식 - Fast R-CNN & Faster R-CNN
* https://www.youtube.com/watch?v=Jo32zrxr6l8&list=WL&index=7&t=0s

PR-012: Faster R-CNN : Towards Real-Time Object Detection with Region Proposal Networks
* https://www.youtube.com/watch?v=kcPAGIgBGRs&list=WL&index=8&t=0s

PR-057: Mask R-CNN
https://www.youtube.com/watch?v=RtSZALC9DlU&list=WL&index=9&t=0s

Incredible.AI Faster R-CNN
* http://incredible.ai/deep-learning/2018/03/17/Faster-R-CNN/

(논문리뷰&재구현) Mask R-CNN 설명 및 정리
* https://ganghee-lee.tistory.com/40

What is Faster R-CNN?
* https://dacon.io/competitions/open/235560/codeshare/613/



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
* anaconda prompt를 사용한다면 가능하면 conda를 이용하여 라이브러리를 설치하도록 한다. 그래도 문제가 발생한다면 pip를 이용하여 라이브러리를 설치하는게 좋다. 그 이유는 아직 잘 모른다.

5. No module named 'pycocotools'
* 웬만한 라이브러리 오류들은 conda install이나 pip install을 이용하면 쉽게 설치되는데 해당 라이브러리는 잘 설치되지 않는다. 아래 사이트를 참고하여 문제를 해결할 수 있다.
[참고] http://blog.naver.com/PostView.nhn?blogId=tip9004&logNo=221270291955

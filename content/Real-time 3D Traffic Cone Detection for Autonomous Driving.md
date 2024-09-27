**Abstract** - 단안 카메라를 이용한 도로 장면의 의미론적 이해에 상당한 진전이 있었습니다. 그러나 이는 주로 자동차, 자전거 이용자, 보행자와 같은 특정 클래스에 초점을 맞추고 있습니다. 본 연구는 자율주행 차량의 맥락에서 교통 통제에 중요한 물체 범주인 교통 콘을 조사합니다. 단안 카메라의 이미지를 사용한 3D 물체 감지는 본질적으로 불량 설정 문제입니다. 본 연구에서는 교통 콘의 독특한 구조를 활용하고 이 문제를 해결하기 위한 파이프라인 접근 방식을 제안합니다. 구체적으로, 우리는 먼저 수정된 2D 물체 감지기로 이미지에서 콘을 감지합니다. 이어서 우리의 심층 구조 회귀 네트워크의 도움으로 교통 콘의 키포인트를 인식하는데, 여기서 교차비가 투영 불변이라는 사실이 네트워크 정규화에 활용됩니다. 마지막으로, 키포인트 회귀에서 얻은 대응을 사용하여 고전적인 원근 n-점 알고리즘을 통해 콘의 3D 위치를 복원합니다. 광범위한 실험을 통해 우리의 접근 방식이 실시간으로 교통 콘을 정확하게 감지하고 3D 세계에서의 위치를 추정할 수 있음을 보여줍니다. 제안된 방법은 실시간 자율 시스템에도 배포되었습니다. 저전력 Jetson TX2에서 효율적으로 실행되어 정확한 3D 위치 추정을 제공하며, 레이스카가 교통 콘으로 표시된 보이지 않는 트랙을 매핑하고 자율 주행할 수 있게 합니다. 강력하고 정확한 인식의 도움으로, 우리의 레이스카는 2018년 이탈리아와 독일에서 열린 두 Formula Student 대회에서 모두 우승했으며, "gotthard driverless" 무인 플랫폼에서 최고 속도 54km/h로 주행했습니다 (https://youtu.be/HegmIXASKow?t=11694). 전체 파이프라인, 매핑 및 내비게이션의 시각화는 우리의 프로젝트 페이지 http://people.ee.ethz.ch/˜tracezuerich/TrafficCone/에서 확인할 수 있습니다.

<br>

### I. Introdution

자율주행은 컴퓨터 비전, 로봇공학, 그리고 기계학습 커뮤니티가 공동으로 해결해야 할 가장 흥미로운 문제 중 하나가 되었습니다[^34], [^20], [^15], [^16]. 자율주행 분야를 발전시키기 위해 수많은 연구가 이루어졌고, 이는 몇 년 안에 완전 자동화된 자동차를 약속하는 야심찬 발표로 이어졌습니다. 그러나 악천후와 변화하는 조명 조건에 대한 필요한 견고성[^30], [^6], [^35], 또는 도로 공사와 사고와 같은 일시적이고 예측할 수 없는 상황에 대처할 수 있는 능력[^24]과 같은 중요한 기술적 과제들은 인간 운전자가 자율주행에 자리를 내주기 전에 극복되어야 합니다.

교통 표지판, 신호등, 교통 콘과 같은 교통 통제 장치들은 안전한 운전을 보장하고 도로에서의 사고를 예방하는 데 중요한 역할을 합니다. 최근 몇 년간 교통 표지판[^29], [^23]과 신호등[^17], [^8] 감지에 큰 진전이 있었습니다. 그러나 교통 콘은 아직 적절한 주목을 받지 못했습니다. 교통 콘은 원뿔 모양의 표지물로, 일반적으로 도로나 보도에 배치되며 안전하고 일시적으로 교통을 우회시키거나 특정 구역을 차단하는 데 사용될 수 있습니다. 이들은 종종 도로 공사나 자동차 사고의 경우 교통 차선을 분리하거나 병합하는 데 사용될 수 있습니다. 이러한 상황들은 고해상도(HD) 지도로도 해결할 수 없기 때문에 차량 내 센서로 내부적으로 해결해야 합니다. 교통 콘은 임시적이고 이동 가능하기 때문입니다.

이미지에서 직접 제어 출력(가속과 조향 명령)으로 매핑하는 엔드투엔드 접근 방식을 사용하고 싶을 수 있습니다[15]. 그러나 우리는 해석 가능한 하위 모듈을 가진 부분 기반 접근 방식과 데이터 주도 엔드투엔드 방법의 융합이 더 유망한 방향이라고 믿습니다. 어떤 경우에도 객체 감지는 자율주행 시스템 학습에 여전히 매우 필요합니다.

여기서 흥미로운 점은 이러한 교통 콘들이 그 자체로는 정적 객체이지만, 도시 운전 시나리오에서 자주 교체되고 이동된다는 것입니다. 자동차는 예기치 않게 고장 날 수 있고 새로운 공사 구역이 예상보다 자주 생길 수 있습니다. 건물과 랜드마크는 쉽게 매핑하여 위치 확인에 사용할 수 있지만, 안전한 자동화 운전을 위해서는 이러한 교통 콘을 적극적으로 감지하고 위치를 추정해야 합니다.

LiDAR와 같은 거리 기반 센서는 3D 위치를 정확하게 측정하도록 설계되었지만, LiDAR는 이미지에 비해 희소한 표현을 가지고 있어 작은 물체를 감지하고 색상과 질감과 같은 물리적 특성을 예측하는 것이 큰 과제가 됩니다. 또한, LiDAR 센서는 카메라보다 비용이 더 높아 이러한 플랫폼의 비용을 스펙트럼의 상위 끝으로 밀어 올립니다. 컴퓨터 비전의 발전은 단안 카메라의 이미지만으로도 장면에 무엇이 있는지 뿐만 아니라 3D 세계에서 물리적으로 어디에 있는지도 알 수 있음을 보여줍니다[^12], [^33]. 단안 카메라를 사용하는 또 다른 장점은 다중 카메라 설정이 필요하지 않아 시스템이 더 비용 효율적이고 유지 관리가 용이하다는 것입니다.

이 연구에서 우리는 단일 이미지에서 교통 콘의 3D 위치 추정과 감지를 다룹니다. 우리는 이 작업을 세 단계로 나눕니다: 2D 객체 감지, 랜드마크 키포인트 회귀, 그리고 마지막으로 2D 이미지 공간에서 3D 세계 좌표로의 매핑입니다. 특히, 콘은 이 시나리오에 맞춤화된 기성 2D 객체 감지기에 의해 이미지에서 감지됩니다; 감지된 2D 경계 상자는 우리가 제안한 합성곱 신경망에 입력되어 교통 콘의 7개 랜드마크 키포인트를 회귀하며, 여기서 교차비(Cr)가 투영 불변이라는 사실이 견고성을 위해 활용됩니다. 마지막으로, 콘의 3D 위치는 원근 n-점 알고리즘에 의해 복구됩니다. 우리의 알고리즘을 훈련하고 평가하기 위해, 우리는 교통 콘을 위한 자체 데이터셋을 구축합니다.

광범위한 실험을 통해 우리는 우리의 방법을 사용하여 단일 이미지로 교통 콘을 정확하게 감지할 수 있음을 보여줍니다. 3D 콘 위치 추정은 지상 진실과 비교했을 때 10m 거리에서 0.5m, 16m 거리에서 1m만큼 편차가 있습니다. 우리는 실물 크기의 자율 경주용 자동차 형태의 중요한 실시간 시스템에 우리의 방법을 배치함으로써 그 성능을 더욱 검증합니다. 이 자동차는 교통 콘으로 둘러싸인 트랙에서 최고 속도 54 km/h로 주행할 수 있습니다.

이 논문의 주요 기여는 (1) 단일 이미지를 사용한 실시간 3D 교통 콘 감지를 위한 새로운 방법과 (2) 우리의 파이프라인의 정확도가 최고 속도 54 km/h로 경주용 자동차를 자율적으로 운행하기에 충분함을 보여주는 시스템입니다. 교통 콘으로 둘러싸인 트랙을 통과하는 우리 차량의 영상은 https://youtu.be/HegmIXASKow?t=11694 에서 볼 수 있습니다.

<br>

### II. RELATED WORK

**빠른 객체 탐지**. 객체 탐지는 컴퓨터 비전 분야에서 가장 중요한 문제 중 하나였습니다. 더욱이 로봇 플랫폼에서 특히 실시간, 온라인 성능을 위해서는 속도가 핵심입니다. 초기의 성공적인 빠른 객체 탐지기 중 하나는 Viola-Jones의 얼굴 탐지기[^36]로, 약한 학습기를 사용하여 Haar 기반 특징을 이용해 정확하게 얼굴을 탐지합니다. 다음으로 잘 알려진 객체 탐지기 부류는 합성곱 신경망(CNN) 형태의 딥러닝을 사용합니다. R-CNN[^10], [^27], [^9] 계열은 CNN 기반 특징을 영역 제안 분류에 사용합니다. YOLO[^25]는 객체 탐지를 회귀 작업으로 교묘하게 공식화하여 매우 효율적인 탐지 시스템을 만들었습니다. 단일 샷 방식은 3D 객체 탐지에도 적용되었습니다[^18]. 일반적인 객체 탐지 측면에서 진전이 있었지만, 교통 콘과 같은 소형 객체 클래스에 대한 성능은 추가 개선이 필요합니다.

**교통 장치 탐지**. 교통 표지판[^29], [^23]과 신호등[^17], [^8] 탐지 방향으로 연구가 진행되었습니다. 벤치마킹 노력을 돕기 위해 100,000개의 주석이 달린 교통 표지판 이미지 데이터셋이 공개되었습니다[^38]. Li 등[^21]은 먼 거리의 교통 표지판과 같은 작은 객체 탐지를 개선하기 위해 생성적 적대 신경망(GAN)을 제안합니다. Lee 등[^19]은 교통 표지판을 탐지하고 거친 사각형 형태의 경계 상자 대신 더 정교한 마스크를 출력하는 아이디어를 탐구합니다. 이 연구는 2개의 프레임에 걸쳐 추출된 객체 경계를 사용한 점들의 삼각측량에 대해 간단히 논의하지만, 시뮬레이션에만 국한되어 있습니다. 우리의 연구는 교통 콘 탐지와 단일 이미지만을 사용한 3D 위치 추정에 초점을 맞춥니다.

**키포인트 추정**. 이 연구의 주요 기여 중 하나는 단일 프레임만으로 교통 콘의 3D 포즈를 정확하게 추정할 수 있다는 것입니다. 3D 기하학에 대한 사전 정보를 사용하여 키포인트라고 불리는 매우 특정한 특징점들을 회귀합니다. 이전에 포즈 추정과 키포인트는 다른 연구들[^31], [^12]에서 등장했습니다. Glasner 등[^12]은 투표 SVM 앙상블을 사용하여 자동차가 포함된 이미지의 포즈를 추정합니다. Tulsiani 등[^33]은 특징과 합성곱 신경망을 사용하여 다양한 객체의 시점을 예측합니다. 그들의 연구는 객체의 시점과 특정 객체에 대한 키포인트 간의 상호작용을 포착합니다. PoseCNN[^37]은 딥러닝을 사용하여 6자유도 포즈를 직접 출력합니다. Gkioxari 등[^11]은 k-부분 변형 가능한 부분 모델을 사용하여 사람에 대한 탐지와 키포인트 추출에 대한 통합된 접근 방식을 제시합니다. 우리의 방법은 교통 콘의 독특한 구조, 특히 교차비의 투영 불변 속성을 활용하여 강건한 키포인트 추정을 수행합니다.

<br>

### III. MONOCULAR CAMERA PERCEPTION PIPELINE

#### A. 센서 설정 및 계산 플랫폼

실험 설정은 빠른 움직임으로 인한 이미지 왜곡과 아티팩트를 방지하기 위해 글로벌 셔터가 있는 2메가픽셀 카메라(CMOS 센서 기반)로 구성됩니다. 그림 2는 우리의 카메라 설정을 보여줍니다. 중앙 카메라는 이 연구에서 설명하는 단안 카메라로, 장거리 인식을 위해 12mm 렌즈를 사용합니다. 좌우 카메라는 5.5mm 초점 거리의 렌즈를 사용하며 가까운 콘을 삼각측량하는 스테레오 쌍으로 작동합니다. 카메라들은 맞춤 제작된 3D 프린팅 방수 쉘에 내장되어 있으며, 렌즈 앞에는 편광 필터가 있습니다. 카메라들은 공유 스위치를 통해 이더넷으로 데이터를 전송하여 깔끔한 카메라 하우징을 가능하게 합니다. 카메라들은 하단의 금속판에 나사로 고정되어 있으며, 작동 온도를 유지하기 위해 직접 접촉하고 있습니다. 원시 카메라 데이터는 "gotthard driverless" 온보드의 마스터 PIP-39(Intel i7 탑재)의 슬레이브 역할을 하는 Jetson TX2로 직접 전송됩니다. 이 파이프라인은 10Hz의 속도로 저전력 컴퓨팅에서 완전히 실행될 수 있을 만큼 가볍습니다.

#### B. 파이프라인 개요

단일 이미지에서의 포즈 추정은 잘 정의되지 않은 문제이지만, 관심 대상의 사전 구조 정보를 통해 해결할 수 있습니다. 방대한 양의 데이터와 GPU와 같은 강력한 하드웨어의 가용성으로, 딥 러닝은 고전적이고 수작업으로 만든 접근 방식으로는 해결하기 어려운 작업에 뛰어난 성능을 보여주었습니다. 데이터 기반 기계 학습은 정교한 표현을 학습하는 데 뛰어나며, 수학과 기하학에서 확립된 결과는 강건하고 신뢰할 수 있는 포즈 추정을 제공합니다. 우리의 연구에서는 파이프라인 접근 방식을 통해 성능과 해석 가능성을 모두 중요하게 여기면서 두 세계의 장점을 효율적으로 결합하고자 합니다.

파이프라인의 하위 모듈들은 단일 이미지를 사용하여 관심 대상을 감지하고 그들의 3D 위치를 정확하게 추정할 수 있게 합니다. 파이프라인의 3가지 하위 모듈은 (1) 객체 감지, (2) 키포인트 회귀, (3) 2D-3D 대응을 통한 포즈 추정입니다. 파이프라인의 하위 모듈들은 Robot Operating System (ROS) [^4] 프레임워크를 사용하여 노드로 실행되며, 이는 파이프라인의 다른 부분들 사이와 다른 시스템 간의 데이터(메시지 형태) 통신과 전송을 처리합니다. 자세한 내용은 [[Real-time 3D Traffic Cone Detection for Autonomous Driving#IV. APPROACH|IV]]절에서 더 자세히 설명될 것입니다.

<br>

### IV. APPROACH

#### A. 객체 탐지

단일 이미지에서 여러 객체 인스턴스의 3D 위치를 추정하기 위해서는 먼저 이러한 관심 객체들을 탐지할 수 있어야 합니다. 객체 탐지 작업을 위해 우리는 파이프라인에 YOLOv2[^26] 형태의 기성 객체 탐지기를 사용합니다. YOLOv2는 Formula Student Driverless 이벤트(우리 플랫폼으로 참가한)에서 경주 트랙을 구분하는 주요 랜드마크 역할을 하는 다양한 색상의 콘을 탐지하도록 훈련되었습니다. 오탐지와 오분류를 최소화하기 위해 임계값과 매개변수들이 선택되었습니다. 이 특정 사용 사례에서 YOLOv2는 경주 트랙에서 특정 의미를 가진 노란색, 파란색, 주황색 콘만을 구별하면 되므로 탐지하는 클래스 수를 줄여 커스터마이즈되었습니다.

콘의 경계 상자는 높이 대 너비 비율이 1보다 크기 때문에, 이러한 사전 정보를 활용하여 YOLOv2가 사용하는 앵커 박스를 재계산합니다(자세한 내용은[^26] 참조).

초기화에는 ImageNet[^7] 챌린지를 위해 훈련된 가중치가 사용됩니다. 우리는 원래 연구 [^26]와 유사한 훈련 방식을 따릅니다. 시즌 동안 더 많은 데이터가 수집되고 라벨링되면 탐지기는 미세 조정됩니다. 데이터 수집 및 주석에 대한 자세한 내용은 섹션 [[Real-time 3D Traffic Cone Detection for Autonomous Driving#8bb344|V-A.1]]을 참조하십시오.

#### B. Keypoint Regression

이 섹션에서는 단일 2D 이미지에서의 객체 탐지를 통해 관심 객체의 3D 위치를 추정하는 방법에 대해 논의합니다. 단일 뷰에서 이를 수행하는 것은 스케일로 인한 모호성 때문에 어렵습니다. 그러나 원뿔의 3D 형태, 크기 및 기하학에 대한 사전 정보를 통해 단일 이미지만으로도 탐지된 객체의 3D 포즈를 복원할 수 있습니다. 객체(3D)와 이미지(2D) 사이의 2D-3D 대응점 세트와 카메라의 내부 파라미터가 있다면 객체의 3D 포즈를 추정할 수 있습니다.

이를 위해 우리는 고전적인 컴퓨터 비전에서 영감을 받았지만 기계 학습을 사용하여 데이터로부터 학습하는 특징 추출 방식을 소개합니다.

1. 키포인트 표현: 객체 탐지기의 경계 상자는 원뿔과 직접적으로 대응되지 않습니다. 이를 해결하기 위해 제안된 경계 상자 내에서 원뿔을 대표하는 랜드마크 특징을 추출합니다. 고전적인 컴퓨터 비전의 맥락에서 세 가지 종류의 특징이 있습니다: 평평한 영역, 엣지, 코너입니다. 엣지는 평평한 영역보다 더 흥미롭습니다. 왜냐하면 한 방향(엣지 경계에 수직인)으로 그래디언트가 있지만 조리개 문제[^32]를 겪기 때문입니다. 가장 흥미로운 특징은 코너로, 한 방향이 아닌 두 방향으로 그래디언트가 있어 세 가지 중 가장 구별됩니다.

이전의 특징 추출 작업에는 유명한 Harris 코너 검출기[^13], 강건한 SIFT[^22], SURF[^5] 특징 추출기 및 기술자가 포함됩니다. 이들 중 많은 것들이 가지고 있는 속성은 스케일, 회전, 조명과 같은 변환에 대한 불변성으로, 대부분의 사용 사례에서 매우 바람직합니다. 이들 대부분은 일반적인 특징 검출기로 잘 작동하며 다양한 응용 분야에서 사용될 수 있습니다.

기존의 특징 추출 기술을 사용하는 데 있어 문제점은 이들이 일반적이며 특징점의 기준에 부합하는 모든 종류의 특징을 검출한다는 것입니다. 예를 들어, Harris 코너는 특징점이 원뿔에 있는지 도로의 균열에 있는지 구별하지 않습니다. 이로 인해 관련된 2D 대응점을 추출하고 이를 3D 대응점과 정확히 매칭하기 어렵습니다. 또 다른 문제는 패치의 해상도가 낮을 때 몇 개의 특징만 검출될 수 있어 객체의 3D 포즈를 추정하기에 충분한 정보를 제공하지 못할 수 있다는 것입니다.

2. 키포인트 회귀: 이전에 제안된 작업의 이러한 한계를 염두에 두고, 우리는 이미지 패치가 주어졌을 때 "코너"와 같은 특징을 회귀하는 합성곱 신경망(CNN)을 설계합니다. 일반적인 특징 추출 기술에 비해 주요 장점은 데이터의 도움으로 매우 특정한 특징점을 강건하게 검출하는 법을 학습할 수 있다는 것입니다. 이 작업에서는 특정 객체 클래스인 원뿔에 초점을 맞추지만, 제안된 키포인트 회귀 방식은 다른 유형의 객체에도 쉽게 확장될 수 있습니다. 이러한 특정 특징점에 해당하는 3D 위치(그림 4에 표시된 대로)는 임의의 세계 좌표계 $F_w$에서 3D로 측정될 수 있습니다. 우리의 목적을 위해 이 좌표계를 원뿔의 밑면에 배치합니다.

이러한 키포인트를 해당 위치에 배치하는 데에는 두 가지 이유가 있습니다. 첫째, 키포인트 네트워크는 시각적으로 구별되고 "코너" 특징과 시각적으로 유사하다고 간주될 수 있는 7개의 매우 특정한 특징의 위치를 회귀합니다. 둘째, 더 중요하게는 이 7개의 점은 고정된 세계 좌표계 $F_w$에서 3D로 상대적으로 쉽게 측정할 수 있습니다. 편의상 $F_w$는 3D 원뿔의 밑면으로 선택되어 이 세계 좌표계 $F_w$에서 이 7개 점의 3D 위치 측정을 가능하게 합니다. 7개의 키포인트는 원뿔의 꼭짓점, 원뿔 밑면의 양쪽에 있는 두 점, 중앙 줄무늬와 배경, 상/하부 줄무늬가 만나는 4개의 점입니다.

특정 "코너" 특징을 검출하도록 맞춤 제작된 CNN은 객체 탐지기에 의해 검출된 원뿔을 포함하는 80×80×3 크기의 하위 이미지 패치를 입력으로 받아 $\mathbb{R}^{14}$로 매핑합니다. 공간 차원은 80×80으로 선택되었는데, 이는 검출된 경계 상자의 평균 크기입니다. $\mathbb{R}^{14}$의 출력 벡터는 키포인트의 $(x,y)$ 좌표입니다.

합성곱 신경망의 아키텍처는 ResNet[^14]에서 영감을 받은 기본 잔차 블록으로 구성되며 PyTorch[^3] 프레임워크를 사용하여 구현됩니다.

[^28]에서 분석된 바와 같이, 더 많은 합성곱 층을 사용하면 텐서 볼륨의 채널은 더 많아지지만 반면에 공간 차원이 크게 감소하여 텐서가 특정하고 지역적인 정보보다는 더 전역적이고 고수준의 정보를 포함하게 됩니다. 우리는 결국 키포인트의 위치에 관심이 있는데, 이는 매우 특정하고 지역적입니다. 이러한 아키텍처를 사용하면 키포인트의 위치를 정확하게 예측하는 데 중요한 공간 정보의 손실을 방지할 수 있습니다.

네트워크의 백본은 ResNet과 유사합니다. 네트워크의 첫 번째 블록은 배치 정규화(BN)와 비선형 활성화 함수로 정류된 선형 유닛(ReLU)이 뒤따르는 합성곱 층입니다. 다음 4개의 블록은 그림 5에 묘사된 대로 채널 수가 증가하는 $C \in {64,128,256,512}$ 기본 잔차 블록입니다. 마지막으로 패치 내 키포인트의 $(x,y)$ 위치를 회귀하는 완전 연결 층이 있습니다.

3. 손실 함수: 앞서 언급했듯이, 우리는 이미지(2D)의 키포인트와 물리적 원뿔(3D)의 위치 사이의 2D-3D 대응을 매칭하기 위해 객체 특정 사전 정보를 사용합니다. 또한 키포인트 네트워크는 교차비의 개념을 통해 손실 함수를 통해 객체의 3D 기하학과 외관에 대한 사전 정보를 활용합니다. 알려진 바와 같이, 투영 변환 하에서는 점 사이의 거리나 그 비율이 보존되지 않습니다. 그러나 거리의 비율의 비율인 더 복잡한 개체인 교차비는 불변이며 투영 하에서 보존됩니다. 기하학을 포함하는 고전적인 컴퓨터 비전 접근법에서 사용되었지만, 교차비는 기계 학습의 맥락에서는 거의 사용되지 않았습니다. 우리는 이를 사용하여 키포인트의 위치를 기하학적으로 제약하고 모델의 손실 함수에 직접 통합합니다.

교차비$(Cr)$는 스칼라 양이며 4개의 공선 점 또는 5개 이상의 비공선 점으로 계산할 수 있습니다[^1]. 이는 투영 하에서 불변이며 카메라로 이미지를 획득하는 과정은 본질적으로 투영 변환입니다. 교차비는 장면의 2D 투영(이미지)과 객체가 존재하는 3D 공간 모두에서 보존됩니다.

우리의 경우, 4개의 공선 점 $p_1, p_2, p_3, p_4$를 사용하여 [[Real-time 3D Traffic Cone Detection for Autonomous Driving#^aff134|방정식 1]]에 정의된 대로 교차비를 계산합니다. 3D 점$(D=3)$인지 또는 그들의 투영된 2차원 대응점$(D=2)$인지에 따라 두 점 $p_i$와 $p_j$ 사이의 거리 $\Delta_{ij}$가 정의됩니다. <br><br>

$$
\tag{1}
\begin{align*}
Cr(p_1, p_2, p_3, p_4) = (\Delta_{13}/\Delta_{14})/(\Delta_{23}/\Delta_{24}) \in R \\
\Delta_{ij}=\sqrt{\Sigma^D_{n=1}(X^{(n)}_i-X^{(n)}_j)^2}, D \in {2,3}
\end{align*}
$$

^aff134

<br>정규화 역할을 하는 교차비 외에도, 손실 함수는 각 회귀된 키포인트의 $(x,y)$ 위치에 대한 제곱 오차 항을 포함합니다. 제곱 오차 항은 회귀된 출력이 키포인트의 실제 주석에 최대한 가깝도록 강제합니다. 교차비의 효과는 인자 $\gamma$에 의해 제어되며 0.0001의 값으로 설정됩니다. <br><br>

$$
\tag{2}
\begin{align*}
\Sigma^7_{i=1}(p^{(x)}_i-p^{(x)}_{i\_groundtruth})^2+(p^{(y)}_i-p^{(y)}_{i\_groundtruth})^2 \\
+ \gamma \cdot (Cr(p_1, p_2, p_3, p_4)-Cr_{3D})^2 \\
+ \gamma \cdot (Cr(p_1, p_5, p_6, p_7)-Cr_{3D})^2
\end{align*}
$$

^1c64ca

<br>두 번째와 세 번째 항은 3D에서 측정된 교차비$(Cr_{3D})$와 키포인트 회귀기의 출력을 기반으로 2D에서 계산된 교차비 사이의 오차를 최소화하여 간접적으로 CNN이 출력하는 위치에 영향을 미칩니다. [[Real-time 3D Traffic Cone Detection for Autonomous Driving#^1c64ca|방정식 2]]의 두 번째 항은 원뿔의 왼쪽 팔을 나타내고 세 번째 항은 오른쪽 팔을 나타냅니다(그림 6 참조). 교차비에 대해, 우리는 이미 알려진 3D 추정치$(Cr_{3D} = 1.39408, \textsf{ 실제 원뿔에서})$와 그 2D 대응치 사이의 제곱 오차 항을 최소화하기로 선택합니다. [[Real-time 3D Traffic Cone Detection for Autonomous Driving#^1c64ca|방정식 2]]는 키포인트 회귀기를 훈련하는 동안 최소화되는 손실 함수를 나타냅니다. 훈련 방식은 다음 섹션에서 설명됩니다.

4. 훈련: 모델을 훈련시키기 위해 확률적 경사 하강법(SGD)이 최적화에 사용되며, 학습률 = 0.0001, 모멘텀 = 0.9, 배치 크기는 128입니다. 학습률은 75 및 100 에폭 후에 0.1배로 조정됩니다. 네트워크는 250 에폭 동안 훈련됩니다. 키포인트 회귀기는 PyTorch로 구현되어 "gotthard driverless"에서 ROS를 통해 사용됩니다. 데이터셋에 대한 자세한 정보는 섹션 [[Real-time 3D Traffic Cone Detection for Autonomous Driving#^c42048|V-A.2]]를 참조하십시오.

C. 2D에서 3D로의 대응

키포인트 네트워크는 관심 객체의 특정 특징, 즉 키포인트의 위치를 제공합니다. 우리는 관심 객체(이 경우 원뿔)의 형태, 크기, 외관 및 3D 기하학과 같은 사전 정보를 사용하여 2D-3D 대응 매칭을 수행합니다. 카메라의 내부 파라미터를 사용할 수 있고 키포인트 네트워크가 2D-3D 대응을 제공합니다. 이러한 정보를 사용하여 단일 이미지만으로도 해당 객체의 3D 포즈를 추정할 수 있습니다. 우리는 Perspective n-Point (PnP) 알고리즘을 사용하여 이러한 정보를 결합합니다.

카메라 프레임을 $F_c$로, 세계 프레임을 $F_w$로 정의합니다. $F_w$는 임의로 선택될 수 있지만, 우리의 경우 키포인트의 3D 위치$(F_w \textsf{에 대해})$를 쉽게 측정하고 변환을 계산하여 최종적으로 원뿔 위치를 편리하게 계산할 수 있도록 모든 검출된 원뿔의 밑면에 $F_w$를 선택합니다.

우리는 Perspective n-Point를 사용하여 검출된 모든 원뿔의 포즈를 추정합니다. 이는 카메라 좌표계 $F_c$와 세계 좌표계 $F_w$ 사이의 변환 $^cT_w$를 추정함으로써 작동합니다. 우리는 $F_c$와 $F_w$ 사이의 변환에만 관심이 있으며, 이는 우리가 추정하고자 하는 카메라 프레임에 대한 원뿔의 위치와 정확히 일치하므로, 우리의 경우 방향은 무시합니다.

원뿔의 위치를 정확하게 추정하기 위해, 우리는 OpenCV[^2]에 구현된 비선형 PnP를 사용하며, 이는 Levenberg-Marquardt를 사용하여 변환을 얻습니다. 또한, 노이즈가 있는 대응을 처리하기 위해 일반 PnP 대신 RANSAC PnP를 사용합니다. RANSAC PnP는 각 검출된 원뿔에 대한 2D-3D 대응 세트에 대해 수행됩니다. 즉, 패치를 키포인트 회귀기에 통과시켜 키포인트를 추출하고 미리 계산된 3D 대응을 사용하여 3D 위치를 추정합니다. 카메라 프레임과 자차 프레임 사이의 변환을 통해 각 원뿔의 자동차 프레임에서의 위치를 얻을 수 있습니다.

<br>

### V. DATA COLLECTION AND EXPERIMENTS

#### A. 데이터셋 수집 및 주석

제안된 파이프라인의 객체 탐지 및 키포인트 회귀를 위한 데이터를 훈련하고 평가하기 위해 데이터를 수집하고 수동으로 라벨링했습니다. 단일 이미지를 사용한 제안 방법의 위치 추정 정확도를 분석하기 위해 LiDAR의 도움을 받아 3D 실측 데이터를 수집했습니다.

1. <span id="8bb344">교통 콘 탐지: 객체 탐지기는 획득한 데이터셋의 90%(약 2,700개의 수동 주석 이미지)로 훈련되었으며, 성능은 데이터의 10%(약 300개의 미확인 이미지)로 평가되었습니다.</span>
2. 콘 패치의 키포인트: 전체 이미지에서 900개의 콘 패치를 추출하여 자체 개발한 주석 도구를 사용하여 수동으로 라벨링했습니다. ^c42048

**데이터 증강**. 데이터셋은 20개의 무작위 변환을 통해 이미지를 변형하여 추가로 증강되었습니다. 이는 $[-15\degree,\ +15\degree]$ 사이의 무작위 회전, 0.8배에서 1.5배 사이의 크기 조정, 그리고 최대 50%의 모서리 길이 이동의 조합이었습니다. 훈련 과정 중에는 대비, 채도, 밝기 형태로 데이터가 실시간으로 추가 증강됩니다. 최종 증강된 주석 데이터셋은 16,000개의 콘 패치를 훈련용으로, 나머지 2,000개의 콘 패치를 테스트용으로 분할했습니다.

3. LiDAR의 3D 실측 데이터: 3D 위치 추정의 정확도를 테스트하기 위해 LiDAR로 측정한 해당 객체 위치를 실측 데이터로 취급했습니다. 이는 4m에서 18m까지 다양한 거리에 있는 104개의 물리적 콘에 대해 수행되었습니다. 추정치는 그림 9에서 비교되며 섹션 [[Real-time 3D Traffic Cone Detection for Autonomous Driving#D. 3D 위치 정확도|V-D]]에 요약되어 있습니다.

이 섹션에서는 단안 인식 파이프라인의 결과를 분석하고 논의하며, 특히 키포인트 네트워크의 견고성과 단일 이미지를 사용한 제안 방식의 3D 위치 추정 정확도에 주목합니다. 키포인트 네트워크는 Jetson TX2에서 파이프라인의 다른 하위 모듈을 실행하고 1 Gb/s의 원시 이미지 데이터를 처리하면서 0.06초 내에 단일 프레임에서 여러 콘 패치를 처리할 수 있어 초당 15-16 프레임으로 작동합니다.

#### B. 콘 탐지

표 II는 콘 탐지 하위 모듈의 성능 평가를 요약합니다. 시스템은 높은 재현율을 가지며 예상되는 대부분의 경계 상자를 검색할 수 있습니다. 높은 정밀도로 인해 오탐지에 대해 회피적이며, 이는 경주용 자동차를 트랙 한계 내에 유지하는 데 가장 중요합니다. 그림 3은 다양한 날씨와 조명 조건에서 콘 탐지 파이프라인의 견고성을 보여줍니다. 색상이 있는 콘 탐지는 각각의 색상으로 된 경계 상자로 표시됩니다. 자율 주행 차량을 성공적으로 운전하는 핵심은 오탐지가 최소화되거나 없는 인식 시스템을 설계하는 것입니다. 오탐지는 콘(장애물) 환각을 유발하여 차량을 코스 이탈로 이끌 수 있습니다. 콘 탐지 모듈은 약 18-20m 깊이까지 콘을 탐지할 수 있지만, 작은 크기로 인해 더 멀리 있는 콘에 대해 더 일관성 있게 작동합니다.

#### C. 키포인트 회귀

그림 7은 YOLOv2에 의해 탐지된 후 키포인트에 대해 회귀된 10개의 샘플 패치 몽타주를 보여줍니다. 상단 행의 왼쪽에서 두 번째 콘은 이미지의 오른쪽 가장자리에서 탐지되어 부분적으로만 보이며 검은색 픽셀로 패딩되었습니다. 픽셀이 누락되고 콘의 일부에 대한 정보가 없어도 제안된 회귀기는 키포인트를 예측합니다. 이는 기하학과 한 키포인트와 다른 키포인트 간의 상대적 위치를 학습합니다. 콘을 부분적으로만 관찰하더라도 완전한 이미지의 경우 키포인트가 어디에 있었을지 근사합니다. 예시를 통해 데이터를 통해 키포인트의 공간 배열과 기하학을 이해할 수 있음을 알 수 있습니다. 하단 행의 왼쪽에서 두 번째 콘의 경우 배경에 다른 콘이 있지만 키포인트 네트워크는 더 두드러진 콘으로 회귀할 수 있습니다. 경계 상자의 크기가 작아질수록 하위 이미지의 해상도가 낮아져 정확한 회귀가 더 어려워진다는 점에 주목해야 합니다. 이는 첫 번째 행의 마지막 두 콘 샘플에서 볼 수 있습니다.

우리는 교차비 항을 평균 제곱 항에 추가한 식 2)의 손실을 사용하여 모델을 훈련합니다. 키포인트 회귀기의 성능은 평균 제곱 오차를 사용하여 평가합니다. 최종 키포인트 회귀 모델의 훈련 및 테스트 분할에 대한 성능은 표 III에 요약되어 있습니다. 예측과 실측 데이터 간의 평균 제곱 오차로 측정된 경험적 성능은 훈련과 테스트 분할 간에 매우 유사하여 네트워크가 콘 패치가 주어졌을 때 키포인트를 정확하게 지역화하는 방법을 학습했으며 과적합되지 않았음을 의미합니다.

그림 7은 키포인트 회귀기의 견고성과 정확도를 보여주지만, 이는 키포인트 네트워크 하위 모듈의 내부 성능만을 나타냅니다. 다음 하위 섹션에서는 중간 하위 모듈의 출력이 3D 콘 위치에 어떤 영향을 미치는지 분석합니다. 또한 특정 하위 모듈의 출력 변동성이 파이프라인을 통해 어떻게 파급되어 최종 위치 추정에 영향을 미치는지 보여줍니다.

#### D. 3D 위치 정확도

실시간 자율 주행 자동차에 배포되므로 가장 중요한 측면 중 하나는 추정된 3D 위치의 정확도입니다. 우리는 파이프라인의 정확도를 실측 데이터로 취급되는 LiDAR의 3D 추정치와 비교합니다. 그림 9는 2개의 다른 테스트 트랙에서 얻은 데이터를 보여줍니다. $x\,$축은 물리적 콘의 깊이(미터)를 나타내고, $y\,$축은 LiDAR 추정치의 3D 위치와 단안 카메라 파이프라인의 3D 위치 간의 유클리드 거리를 나타냅니다. 이 그래프는 104개의 물리적 콘을 데이터 포인트로 포함합니다. 또한 데이터에 2차 곡선이 맞춰졌으며, 이는 대부분 선형 성분을 가집니다. 평균적으로 자아 차량에서 10m 떨어진 거리에서 차이는 약 0.5m이고 16m 거리에서는 약 1m입니다. 5m에서 콘 위치는 거리의 $\pm\,5.00\%$ 오차가 있고, 16m에서는 거리의 $\pm\,6.25\%$ 오차만 있습니다. 이 오차는 자율 주행 자동차가 50 km/h 이상의 속도로 콘으로 둘러싸인 트랙을 주행하기에 충분히 작습니다.

#### E. 확장된 인식 범위

이 방법의 목표 중 하나는 인식 범위를 확장하는 것입니다. 그림 10에서는 단안 및 스테레오 파이프라인의 범위 차이를 비교합니다. 단안 카메라를 사용한 우리의 제안 작업은 스테레오 카메라 기반의 표준 삼각측량 솔루션보다 더 큰 인식 범위를 가집니다. 또한 단안 카메라는 스테레오 카메라보다 더 긴 초점 거리를 가집니다. 스테레오 쌍도 더 긴 초점 거리를 가진다면 시야가 줄어들어 스테레오 카메라가 삼각측량할 수 없는 사각지대가 생깁니다.

#### F. 2D 경계 상자가 3D 추정에 미치는 영향

앞서 언급했듯이, 하위 모듈이 최종 3D 위치 추정에 어떤 영향을 미치는지 살펴보고자 합니다. 여기서는 한 단계 뒤로 물러나 객체 탐지 하위 모듈의 출력 변동성(부정확한 경계 상자)이 3D 위치에 어떤 영향을 미치는지 분석합니다. 이 실험에서는 경계 상자의 모서리를 각 방향의 높이와 너비에 비례하는 양만큼 무작위로 교란합니다. 센서의 본질적 특성으로 인해 카메라의 원시 데이터를 사용하여 깊이를 추정하는 것이 가장 어렵습니다. 그림 11은 단일 이미지에 대해 상자를 특정 양$(\pm\,1\%,\ \pm5\%,\ \pm10\% \textsf{ 및 } \pm20\%$)만큼 교란시키면 깊이 추정의 분산에 어떤 영향을 미치는지 보여줍니다. 예상대로 교란의 양이 클수록 깊이 추정의 분산이 더 크게 관찰됩니다. 그러나 $\pm\,20\%$ 교란에 대해서도 15m에서 분산은 약 1 m²입니다. 그림 11은 부정확하고 변동하는 경계 상자에도 불구하고 콘의 깊이가 일관되며 낮은 분산을 가짐을 보여줍니다.

탐지, 회귀, 3D 위치 추정, 매핑 및 최종 내비게이션에 대한 추가 시각화는 프로젝트 페이지 http://people.ee.ethz.ch/˜tracezuerich/TrafficCone/를 방문하십시오.

<br>

### CONCLUSION

정확하고 실시간으로 이루어지는 3D 포즈 추정은 증강 현실부터 자율 주행에 이르기까지 다양한 응용 분야에서 활용될 수 있습니다. 우리는 교차비(cross-ratio) 손실 항을 활용한 기하학적 형태를 통해 특정 특징점을 추출하는 새로운 키포인트 회귀 방식을 소개합니다. 이 접근 방식은 단안 카메라로부터 3D 포즈를 추정하고 객체의 구조적 사전 정보를 활용하여 다양한 객체로 확장될 수 있습니다. 우리는 네트워크가 키포인트의 공간적 배열을 학습하고 도전적인 상황에서도 강건한 회귀를 수행할 수 있는 능력을 보여줍니다. 제안된 파이프라인의 효과성과 정확성을 입증하기 위해 자율 주행 경주용 자동차에 배포되었습니다. 제안된 네트워크는 실시간으로 작동하며, 16m 거리에서 3D 위치 오차가 단 1m에 불과합니다. 감사의 말. AMZ Driverless의 지원에 감사드립니다. 이 연구는 또한 TRACE-Zurich 프로젝트를 통해 Toyota Motor Europe의 지원을 받았습니다.

<br>

[^1]: Cross ratio. http://robotics.stanford.edu/˜birch/projective/node10.html.

[^2]: OpenCV calibration and 3d reconstruction. https://docs.opencv.org/2.4/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html#solvepnp.

[^3]: PyTorch. https://pytorch.org/.

[^4]: ROS: Robot Operating System. https://ros.org/.

[^5]: H. Bay, T. Tuytelaars, and L. Van Gool. Surf: Speeded up robust features. In European conference on computer vision, pages 404–417. Springer, 2006.

[^6]: D. Dai and L. Van Gool. Dark model adaptation: Semantic image segmentation from daytime to nighttime. In IEEE International Conference on Intelligent Transportation Systems, 2018.

[^7]: J. Deng, W. Dong, R. Socher, L.-J. Li, K. Li, and L. Fei-Fei. Imagenet: A large-scale hierarchical image database. In Computer Vision and Pattern Recognition, 2009. CVPR 2009. IEEE Conference on, pages 248–255. Ieee, 2009.

[^8]: A. Fregin, J. Mller, and K. Dietmayer. Three ways of using stereo vision for traffic light recognition. In IEEE Intelligent Vehicles Symposium (IV), 2017.

[^9]: R. Girshick. Fast r-cnn. In Proceedings of the IEEE international conference on computer vision, pages 1440–1448, 2015.

[^10]: R. Girshick, J. Donahue, T. Darrell, and J. Malik. Rich feature hierarchies for accurate object detection and semantic segmentation. In Proceedings of the IEEE conference on computer vision and pattern recognition, pages 580–587, 2014.

[^11]: G. Gkioxari, B. Hariharan, R. Girshick, and J. Malik. Using k-poselets for detecting people and localizing their keypoints. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 3582–3589, 2014.

[^12]: D. Glasner, M. Galun, S. Alpert, R. Basri, and G. Shakhnarovich. aware object detection and continuous pose estimation. Image and Vision Computing, 30(12):923–933, 2012.

[^13]: C. Harris and M. Stephens. A combined corner and edge detector. Citeseer, 1988.

[^14]: K. He, X. Zhang, S. Ren, and J. Sun. Deep residual learning for image recognition. In Proceedings of the IEEE conference on computer vision and pattern recognition, pages 770–778, 2016.

[^15]: S. Hecker, D. Dai, and L. Van Gool. End-to-end learning of driving models with surround-view cameras and route planners. In European Conference on Computer Vision (ECCV), 2018.

[^16]: S. Hecker, D. Dai, and L. Van Gool. Learning accurate, comfortable and human-like driving. In arXiv-1903.10995, 2019.

[^17]: M. B. Jensen, M. P. Philipsen, A. Mgelmose, T. B. Moeslund, and M. M. Trivedi. Vision for looking at traffic lights: Issues, survey, and perspectives. IEEE Transactions on Intelligent Transportation Systems, 17(7):1800–1815, 2016.

[^18]: W. Kehl, F. Manhardt, F. Tombari, S. Ilic, and N. Navab. Ssd-6d: Making rgb-based 3d detection and 6d pose estimation great again. In The IEEE International Conference on Computer Vision (ICCV), Oct 2017.

[^19]: W. Kehl, F. Manhardt, F. Tombari, S. Ilic, and N. Navab. Ssd-6d: Making rgb-based 3d detection and 6d pose estimation great again. In The IEEE International Conference on Computer Vision (ICCV), Oct 2017.

[^20]: J. Levinson, J. Askeland, S. Thrun, and et al. Towards fully autonomous driving: Systems and algorithms. In IEEE Intelligent Vehicles Symposium (IV), 2011.

[^21]: J. Li, X. Liang, Y. Wei, T. Xu, J. Feng, and S. Yan. Perceptual generative adversarial networks for small object detection.

[^22]: D. G. Lowe. Distinctive image features from scale-invariant keypoints. International journal of computer vision, 60(2):91–110, 2004.

[^23]: M. Mathias, R. Timofte, R. Benenson, and L. V. Gool. Traffic sign recognition how far are we from the solution? In International Joint Conference on Neural Networks (IJCNN), 2013.

[^24]: R. McAllister, Y. Gal, A. Kendall, M. Van Der Wilk, A. Shah, R. Cipolla, and A. Weller. Concrete problems for autonomous vehicle safety: Advantages of bayesian deep learning. In International Joint Conference on Artificial Intelligence, 2017.

[^25]: J. Redmon, S. Divvala, R. Girshick, and A. Farhadi. You only look once: Unified, real-time object detection. In Proceedings of the IEEE conference on computer vision and pattern recognition, pages 779–788, 2016.

[^26]: J. Redmon and A. Farhadi. YOLO9000: better, faster, stronger. CoRR, abs/1612.08242, 2016.

[^27]: S. Ren, K. He, R. Girshick, and J. Sun. Faster r-cnn: Towards real-time object detection with region proposal networks. In Advances in neural information processing systems, pages 91–99, 2015.

[^28]: O. Ronneberger, P. Fischer, and T. Brox. U-net: Convolutional networks for biomedical image segmentation. CoRR, abs/1505.04597, 2015.

[^29]: A. Ruta, F. Porikli, S. Watanabe, and Y. Li. In-vehicle camera traffic sign detection and recognition. Machine Vision and Applications, 22(2):359–375, Mar 2011.

[^30]: C. Sakaridis, D. Dai, and L. Van Gool. Semantic foggy scene understanding with synthetic data. International Journal of Computer Vision, 2018.

[^31]: S. Savarese and L. Fei-Fei. 3d generic object categorization, localiza-tion and pose estimation. 2007.

[^32]: R. Szeliski. Computer vision: algorithms and applications. Springer Science & Business Media, 2010.

[^33]: S. Tulsiani and J. Malik. Viewpoints and keypoints. CoRR, abs/1411.6067, 2014.

[^34]: C. Urmson, J. Anhalt, H. Bae, J. A. D. Bagnell, and et al. Autonomous driving in urban environments: Boss and the urban challenge. Journal of Field Robotics Special Issue on the 2007 DARPA Urban Challenge, Part I, 25(8):425–466, June2008.

[^35]: A. Valada, J. Vertens, A. Dhall, and W. Burgard. Adapnet: Adap-tive semantic segmentation in adverse environmental conditions. In Robotics and Automation (ICRA), 2017 IEEE International Conference on, pages 4644–4651. IEEE, 2017.

[^36]: P. Viola and M. Jones. Rapid object detection using a boosted cascade of simple features. In Computer Vision and Pattern Recognition, 2001. CVPR 2001. Proceedings of the 2001 IEEE Computer Society Conference on, volume 1, pages I–I. IEEE, 2001.

[^37]: Y. Xiang, T. Schmidt, V. Narayanan, and D. Fox. Posecnn: A convolutional neural network for 6d object pose estimation in cluttered scenes. CoRR, abs/1711.00199, 2017.

[^38]: Z. Zhu, D. Liang, S. Zhang, X. Huang, B. Li, and S. Hu. Traffic-sign detection and classification in the wild. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2016.

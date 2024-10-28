---
title: Decision Making And Hybrid-Based Trajectory Planning for AutonomousVehicle In Various Highway Scenarios
aliases: 
tags:
  - Paper
type: 
cssclasses:
  - width-100
  - width-80
---

 > [!abstract]-
> 
> 자율주행 차량에 대한 관심이 높아짐에 따라 안전하고 편안한 주행을 보장하는 알고리즘의 중요성이 부각되고 있습니다. 지속적으로 변화하는 동적 환경에 대응하면서 실시간으로 올바른 의사결정을 하는 것은 매우 도전적인 과제입니다. 특히 구조화된 도로에서 주행이 이루어지는 고속도로와 같은 환경에서는 자차와 주변 차량의 높은 속도로 인해 더욱 정확하고 신속한 의사결정이 요구됩니다. 이러한 시나리오에서 안전성이 최우선 순위가 될 수 있습니다.
> 
> 하지만 주행에서 안전성만을 고려하는 것은 주변 교통 환경과 다소 괴리가 있습니다. 다시 말해, 안전성과 주행 성능은 상충관계에 있습니다. 따라서 이러한 관계를 제어하고, 그에 따른 결정에 맞는 궤적을 계획하는 것이 매우 중요합니다. 본 연구는 이를 해결하기 위한 알고리즘을 제안합니다. 실시간 연산 능력을 향상시키기 위해 전술적 의사결정(TDM)과 궤적 생성(TG) 모듈이 계층적으로 작동합니다. TDM 모델은 주변 환경을 예측하여 시공간적 안전 간격을 기반으로 최적의 결정을 선택합니다. 그런 다음 TG 모듈이 TDM 모듈에서 나온 결정을 실행하기 위해 작동합니다.
> 
> TG 모듈 내에서 전통적인 경로 계획 방법의 장점을 통합하기 위해 하이브리드 방식이 제안됩니다. 또한, 본 연구는 종방향과 횡방향 궤적을 별도로 계획함으로써 계산 비용을 줄이는 것을 목표로 합니다. 두 궤적은 다항식으로 생성되며, 횡방향의 경계 조건은 차선 변경 결정에 의해 결정되고, 종방향은 주변 교통 상황에 따라 설정됩니다. 이러한 접근 방식은 계산 비용을 효율적으로 관리할 수 있게 하여, 급격히 변화하는 환경에서 효율성을 향상시킬 것으로 기대됩니다.
> 
> > [!tip]- Keyword 
> > 
> > 전술적 의사결정(TDM), 궤적 생성기(TG), 하이브리드 기반 방법 

<p style='margin-top: 2em; margin-bottom: 2em'></p>

## Introdution
> [!summary]- 
> 
> 자율주행차량(AVs)은 운송 산업에서 중요한 역할을 합니다. 특히 대부분의 자율주행차량이 고속도로에서 많은 시간을 보내기 때문에, 이러한 환경에서의 자율주행차량에 관한 많은 연구가 진행되고 있습니다. 고속도로 시나리오는 몇 가지 특징을 가지고 있습니다. 첫째, 구조화된 도로와 단순한 도로 규정을 가지고 있습니다. 존재하는 것은 속도 제한뿐입니다. 도심과 달리 갑작스러운 보행자나 신호등이 없습니다. 둘째, 매우 빠르게 변화하는 장면들이 있습니다. 교통 체증이 없는 경우, 주변 차량의 평균 속도는 80~110km/h이거나 그 이상입니다. 이러한 특성들을 고려할 때, 상당한 안전 위험이 수반되므로 의사결정은 다소 보수적이어야 합니다. 또한, 빠르게 변화하는 환경에 대응하기 위해서는 신속한 TDM과 TG가 필요합니다. 이러한 요구사항들을 해결하기 위해서는 단순한 도로 구조와 고속도로 상황의 특성을 효과적으로 활용해야 할 것입니다. 종방향과 횡방향 궤적은 TDM이 생성한 행동 유형을 경계 조건으로 사용하여 생성됩니다. 이러한 계층적 구조는 더욱 효율적인 작업 흐름으로 이어집니다.

TG 모듈은 일반적으로 두 가지 고전적인 방법을 활용합니다:

> [!list]- 1\. 샘플링 기반 방법
> 
> 제약 없이 노드를 생성하는 무작위 샘플링 접근법과 여러 제약 조건과 탐색 방향이 미리 정의된 결정론적 샘플링 방법이 있습니다[^4]. 전자의 방법은 최적 궤적을 생성할 확률이 낮아 시간 비용이 무시할 수 없는 수준입니다. 또한, 이동 차량의 동역학이나 운동학이 전혀 고려되지 않아 샘플링된 궤적의 실현 불가능성 위험이 있습니다. 결정론적 샘플링이 전자 방법의 첫 번째 단점을 어느 정도 해결하지만, 후속 문제는 여전히 존재합니다.

> [!list]- 2\. 최적화 기반 방법
> 
> 샘플링 방법과 달리, 이 접근법은 모델 기반 계획을 가능하게 하고 동적 및 운동학적 제약을 고려하면서 알고리즘적으로 최적 경로를 계산함으로써 실현 가능성 문제를 해결하고 전역 최적값을 찾을 가능성을 크게 높입니다. 더욱이 MPC(Model Predictive Control)와 같은 방법은 최적 안내뿐만 아니라 그 정책을 구현하는 제어 입력도 계산할 수 있습니다. 그러나 수많은 제약 조건과 복잡한 알고리즘의 많은 반복으로 인해 계산 비용이 매우 높아[^4] 고속도로에서의 실시간 처리에는 적합하지 않습니다.

> [!note]- 3\. 하이브리드 방법
> 
> 따라서 두 접근 방식의 장점을 통합하기 위해 하이브리드 방법이 구현되었습니다. 이전 연구[^1]의 일정 속도 모델의 한계를 극복하기 위해 교통 상황을 반영하는 종방향 속도에 대한 경계 조건이 생성되었습니다. 본 연구에서는 제어기가 이상적이라고 가정하여, 생성된 궤적이 정확하게 따라갈 수 있다고 보았습니다. 또한, 이러한 방법들은 주변 환경의 불확실성에 적절히 대응하지 못하는 공통적인 약점을 가지고 있습니다[^4]. 본 보고서에서는 이 문제를 다루지 않지만, 이를 해결하기 위한 방법 개발을 향후 연구 과제로 고려하고 있습니다.

<p style='margin-top: 2em; margin-bottom: 2em'></p>

## Methodology
> [!summary]- 개요
> 
> 우리 시스템의 블록 다이어그램은 [[Decision Making And Hybrid-Based Trajectory Planning for AutonomousVehicle In Various Highway Scenarios#^a40c6d|Fig.1]]에 나와 있습니다. 각 섹션은 그림에 표시된 블록 다이어그램의 흐름과 동일한 순서로 구분되어 있습니다. 환경(시공간적 안전 간격), 전술적 의사결정, 궤적 생성기, 그리고 다른 차량과의 충돌과 같은 실현 불가능성 검사 등이 포함됩니다.

> [!fig]- Fig. 1. 
> 
> ![The overall structure of the control module for Avs.<br>we focus on TDM and Trajectory Planning mod-ule in this review.](https://i.imgur.com/K7tCBi2.png)

^a40c6d

> [!fig]- Fig. 2. 
> 
> ![Example illustration for sampling method for lane change and lane keeping maneuver](https://i.imgur.com/E7H5qOI.png)

> [!fig]- Fig. 3.
> 
> ![Example illustration for optimization based trajec-tory in specific scene.](https://i.imgur.com/PmgaYrn.png)


<p style='margin-top: 2em; margin-bottom: 2em'></p>

> [!think]- 환경 및 가정
> 
> > [!list]- a) 프레넷 상태(Frenet States)
> > 
> > 궤적 모델링의 단순화를 위해, Fig.4 (a)에 표시된 것처럼 프레넷 좌표계를 사용하여 각 방향을 독립적으로 고려합니다. 이 좌표계에서 자차(ego vehicle)는 $(s,d)$로 표현됩니다. $s$는 종방향을 나타내고 $d$는 도로 중심으로부터의 횡방향 오프셋을 나타냅니다. 따라서 전체 계획 작업은 이 좌표계에서 상대적 검사를 통해 구현됩니다. 이전 연구[^1]와 같이 적용됩니다.
> 
> > [!list]- b) 시공간적 안전 간격(Spatio-Temporal Safety Gap)
> > 
> > 주변 차량의 궤적은 지속 시간 $T$동안 등속도 가정으로 예측됩니다. 예측 정보와 제시된 좌표계의 도로 네트워크를 통해, 상대 운동 좌표계(Relative Motion Coordinate, RMC)[^1]라고 불리는 결정론적 장면을 만들 수 있습니다. 그런 다음, Fig.(5)에 표시된 것처럼 이들의 궤적이 없는 영역이 시공간적 안전 간격으로 정의됩니다.
> 
> > [!list]- c) 최중요 객체(Most Important Object, MIO)
> > 
> > 자차 궤적이 적절한 종방향 경계 조건을 받기 때문에, Fig (5)에 표시된 것처럼 가장 중요한(위험한) 객체를 식별합니다. 특정 알고리즘을 사용하여 주변 물체들의 우선순위를 정합니다. 이는 Fig (6)에 나와 있습니다. 이러한 방식으로 TDM과 TG를 위한 환경이 생성됩니다.
> 
> > [!list]- d) 차선 변경 차량
> > 
> > 우리 알고리즘과 관련 연구[^1]의 성능을 비교하기 위해, 차선 변경 시나리오와 같은 더 복잡한 시나리오가 필요합니다. 다른 차량들의 의도는 미리 정의되어 있다고 가정하며, 불확실성도 없다고 가정합니다. 그러나 직선 주행에 비해 이러한 장면에서 많은 영향이 있습니다. 이 주제는 나중에 더 자세히 다룰 예정입니다.

> [!fig]- Fig. 4. 
> 
> ![](https://i.imgur.com/1Xeo753.png)

> [!fig]- Fig. 5. 
> 
> ![](https://i.imgur.com/eMED1cO.png)![](https://i.imgur.com/4MxJIiR.png)

> [!fig]- Fig. 6. 
> 
> 

> [!fig]- Fig. 7.
> 
> 

<p style='margin-top: 2em; margin-bottom: 2em'></p>

> [!note]- 전술적 의사결정(TDM)
> 
> > [!list]- a) 의사결정 위상(Decision Topology)
> > 
> [^1]에서 언급된 것처럼, 도달 가능성으로 알려진 간격들 간의 연결은 다음과 같이 주어집니다:
> > 
> > > [!math]-
> > > 
> > > $$Reach_{\small \textstyle i,j}=\begin{cases} T, & \vert\,Gap_{\small \textstyle i}.s-Gap_{\small \textstyle j}s\,\vert\,< {\small \dfrac{Gap_{\small \textstyle i}l+Gap_{\small \textstyle j}.l}{2}}\\[0.5em] F, & thoerwise \end{cases} \tag{1}$$
> >
> > 이를 통해, 자차가 존재하는 루트 노드에서 시작하는 위상이 형성됩니다. 이 구조는 특정 비용을 효율적으로 계산하는 데 사용되며, 이는 비용 섹션에서 논의될 것입니다.
> 
> > [!list]- b) 비용 함수
> > 
>> 최적 간격을 선택하기 위해, 총 비용 함수와 도로 비용 함수는 다음과 같이 주어집니다:
> >
> > > [!math]- 
> > > 
> > > $$\begin{align} & J^{\small \textstyle i}=C^{\small \textstyle i}_{\small \textstyle road}+C^{\small \textstyle i}_{\small \textstyle traffic}+C^{\small \textstyle i}_{\small \textstyle arrival} \tag{2}\\[1.0em] & C^{\small \textstyle i}_{\small \textstyle road}=1-\frac{Gap^{i}.l}{50 * 2} \tag{3} \end{align}$$
> > 
> > 우리의 상대 프레임 경계는 $\begin{bmatrix} -50,\ -50 \end{bmatrix}$입니다. 따라서 총 경계는 $50*2 = 100$입니다. 도로 비용은 안전 영역의 정도를 나타냅니다. 그리고 교통 비용은 교통 속도와 각 안전 간격으로부터 앞뒤 위치 여부로 구성됩니다. 방정식은 다음과 같습니다:
> > 
> > > [!math]- 
> > > 
> > > $$\begin{align} & C^{\small \textstyle i}_{\small \textstyle traffic,1}+C^{\small \textstyle i}_{\small \textstyle traffic,2} \tag{4}\\[2.0em] & C^{\small \textstyle i}_{\small \textstyle traffic,1}=\begin{cases} \begin{array}{c} 0,\ n_{\small \textstyle car}=0\\ -\\ w_{\small \textstyle car} {\small \dfrac{Gap_{\small \textstyle car}}{n_{\small \textstyle car}}},\ otherwise \end{array} \end{cases} \tag{5}\\[2.0em] & C^{\small \textstyle i}_{\small \textstyle traaffic,2}=\begin{cases} \begin{array}{c} c_{\small \textstyle f} {\small \dfrac{vel_{\small \textstyle ego}}{vel_{\small\ \textstyle ego}}},\ s_{\small \textstyle target} > Gap^{\small \textstyle i}.l\\ -\\ c_{\small \textstyle b} {\small \dfrac{vel_{\small \textstyle target}}{vel_{\small \textstyle ego}}},\ s_{\small \textstyle target} < Gap^{\small \textstyle i}.l \end{array} \end{cases} \tag{6} \end{align}$$
> >
> > [^1]과 비교하여, 우리는 세 가지 추가 사항을 고려했습니다. 첫째, 각 구성원과의 상관관계를 분석했습니다. 다른 비용들과 비교하여, 차량 수와 관련된 비용은 위험 정도와 관계없이 매우 민감합니다. 따라서 이를 줄이기 위해 가중치를 곱했습니다. 둘째, 지배 방정식은 다른 차량의 위치뿐만 아니라 속도도 반영합니다. 셋째, 교통 계수를 통해 위험을 정량화했습니다. 예를 들어, 앞차와의 간격이 $\mathrm{10m}$인 경우는 $\mathrm{30m}$인 경우보다 훨씬 더 위험한 상황입니다. 이 계수는 이러한 차이를 잘 포착합니다. 마지막으로, 도착 비용 함수는 다음과 같이 주어집니다:
> >
> > > [!math]- 
> > > 
> > > $$\begin{align} & C^{\small \textstyle i}_{\small \textstyle AtoB}=C^{\small \textstyle i}_{\small \textstyle long}+C^{\small \textstyle i}_{\small \textstyle lat} \tag{7}\\[2.0em] & C^{\small \textstyle i}_{\small \textstyle long}=1-\frac{\min(\mathrm{A_{\small \textstyle f}, B_{\small \textstyle f}})-\max(A_{\small \textstyle r}, B_{\small \textstyle r})}{Gap^{\small \textstyle A}.l} \tag{8}\\[2.0em] & C^{\small \textstyle i}_{\small \textstyle lat}=\begin{cases} {\small \dfrac{LaneWidth}{10}},  & \!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\! \Delta \mathrm{Idx_{\small \textstyle lane}} \leq 1\\ & \!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\!\! -\\ 2.5, \Delta \mathrm{Idx_{\small \textstyle lane}} > 1 \end{cases} \tag{9} \end{align}$$
> > 
> > 우리는 TDM 모델이 과도한 차선 변경을 선택하는 것을 방지하기 위해 횡방향 비용을 추가했습니다. 종방향 비용은 A에서 B로 이동하는 난이도를 설명합니다. 다시 말해, A와 B 사이의 중첩 영역이 클수록 B로 이동하기가 더 쉽습니다. 따라서 비용이 낮습니다. 그리고 위상 구조에 의해, 비용 평가는 루트 노드에 도달 가능한 간격에 대해서만 구현됩니다. 도달할 수 없는 경우, 이 간격은 최대 도착 비용을 가집니다.
>
> 이러한 절차를 통해, 가중치 매개변수와의 선형 조합으로 각각에 대한 총 비용이 계산됩니다. 그리고 Fig (8)과 같이 가장 낮은 비용을 가진 간격이 최적 간격으로 선택됩니다.

> [!fig]- Fig. 8.

<p style='margin-top: 2em; margin-bottom: 2em'></p>

> [!note]- 2.4 궤적 생성기(TG)
> 
> 우리는 경계 조건을 사용하여 샘플링한 후 각 후보에 비용을 설정하는 하이브리드 방식을 선택했습니다.
> 
> > [!list]- a) 종방향
> > 
> > 일정 속도 모델[^1]의 한계를 극복하기 위해서는 현재 상황에 적합한 경계 조건을 선택하는 것이 중요합니다. 앞서 언급했듯이, 최종 MIO는 우리 알고리즘에 의해 선택되며, 그 속도가 궤적 계획의 경계 조건이 됩니다. 갑작스러운 가속 또는 감속을 검증하기 위해 안전 여유 샘플링이 사용됩니다. 따라서 샘플링 수는 여유 수와 지속 시간에 따라 달라집니다.
> > 
> > > [!math]- 
> > > 
> > > $$\begin{align} & s(t)=a_{0}+a_{1}t+a_{2}t+a_{3}t^{3}+a_{4}t^{4} \tag{10}\\[1.5em] & \begin{cases} s(0)=s_{0}\\ \dot{s}(0)=\dot{s}_{0}\\ \ddot{s}(0)=\ddot{s}_{0} \end{cases} \tag{11}\\[1.5em] & \dot{s}(T)=[  \,v_{\small \textstyle ego},\ v_{\small \textstyle ego}+{\small \frac{1}{2}} v_{\small \textstyle ret},\ v_{\small \textstyle ego}+v_{\small \textstyle ret}\, ] \tag{12}\\ & \ddot{s}(T)=\ddot{s}(T) \tag{13} \end{align}$$
> >
> >식 (11) ~ (14)를 통해 (16)과 같이 선형 대수를 사용하여 다항식 계수를 계산할 수 있습니다.
> >
> > > [!math]- 
> > > 
> > > $$\begin{bmatrix} \dot{s}(T)-\dot{s}(0)-\ddot{s}(0)(T)\\ \ddot{s}(T)-\ddot{s}(0) \end{bmatrix}=\begin{bmatrix} 3T^{2} & 4T^{3}\\ 6T & 12T^{2} \end{bmatrix}\begin{bmatrix} a_{3}\\ a_{4} \end{bmatrix} \tag{14}$$
> 
> > [!list]- b) 횡방향
> > 
> > 고속도로의 단순한 도로 조건과 프레넷 프레임워크는 횡방향 후보의 샘플링을 용이하게 합니다. 횡방향에 하나의 경계 조건이 더 있기 때문에, 횡방향 모델은 다음과 같이 주어집니다:
> > 
> > > [!math]- 
> > > 
> > > $$\begin{align} & d(t)=b_{0}+b_{1}t+b_{2}t^{2}+b_{3}t^{3}+b_{4}t^{4}+b_{5}t^{5} \tag{15}\\[2.0em] & \begin{cases} d(0)=d_{\small \textstyle ego}\\ \dot{d}(0)=\dot{d}_{0}\\ \ddot{d}(0)=\ddot{d}_{0} \end{cases} \tag{16}\\[1.5em] & \begin{cases} d(T)=d_{\small \textstyle tergat}\\ \dot{d}(T)=\dot{d}(T)\\ \ddot{d}(T)=\ddot{d}(T) \end{cases} \tag{17} \end{align}$$
> > 
> > 선형 운동과 마찬가지로, 계수는 (18)에 의해 계산됩니다. 각 결정 기간에서 후보 군집은 지속 시간과 경계 조건에 따라 생성됩니다. 본 연구에서 전자는 3이고 후자는 $\begin{bmatrix} \mathrm{1s},\ \mathrm{2s},\ \mathrm{3s} \end{bmatrix}$입니다. 즉, 후보의 수는 $9$개입니다.
> > 
> > > [!math]- 
> > > 
> > > $$\begin{align} & \begin{bmatrix} d(T)-d_{0}-\dot{d}_{o}T-\ddot{d}_{0}T^{2}\\ \dot{d}(T)-\dot{d}_{0}-\ddot{d}_{0}T\\ \ddot{d}(0)-\ddot{d}(T) \end{bmatrix}\\[0.5em] = & \begin{bmatrix} T^{3} & T^{4} & T^{5}\\ 3T^{2} & 4T^{3} & 5T^{4}\\ 6T & 12T^{2} & 20T^{3} \end{bmatrix} \begin{bmatrix} a_{3}\\ a_{4}\\ a_{5} \end{bmatrix} \tag{18} \end{align}$$
> 
> > [!list]- c) 비용 함수
> > 
> > 최적 궤적을 생성하기 위해서는 실현 가능한 방식으로 후보들의 순위를 매기는 것이 중요합니다. 복잡한 최적화 알고리즘 대신 후보들을 사용합니다. TDM 방법과 유사하게 비용 함수의 조합이 적용됩니다. 이 방법을 통해 계산 비용을 줄이고, 그들 중 가장 최적의 궤적을 선택할 수 있습니다. 공식은 다음과 같습니다:
> > 
> > > [!math]- 
> > > 
> > > $$\begin{align} & J^{\small \textstyle i}=w_{\small \textstyle v}C_{\small \textstyle v}+w_{\small \textstyle a}C_{\small \textstyle a}+w_{\small \textstyle j}C_{\small \textstyle j}+w_{\small \textstyle k}C_{\small \textstyle k}+w_{\small \textstyle ttc}C_{\small \textstyle ttc} \tag{19}\\[2.0em] & C_{\small \textstyle v}=\frac{1}{T} {\large \textstyle \int} \frac{\big(v_{\small \textstyle d}-\dot{s}(t)\big)^{2}}{\Delta v^{2}_{d}}\ dt \tag{20}\\[2.0em] & C_{\small \textstyle a}=\frac{1}{T}{\large \textstyle \int}\frac{\ddot{s}(t)}{a^{2}_{\small \textstyle max}}\ dt \tag{21}\\[2.0em] & C_{\small \textstyle j}=\frac{1}{T}{\large \textstyle \int} \frac{j_{\small \textstyle long}(t)^{2}}{j^{2}_{\small \textstyle max,long}}\ dt + {\large \textstyle \int} \frac{j_{\small \textstyle lat}(t)^{2}}{j^{2}_{\small \textstyle max,lat}}\ dt \tag{22}\\[2.0em] & C_{\small \textstyle k}=\frac{1}{T}{\large \textstyle \int} \frac{k(t)^{2}}{k^{2}_{\small \textstyle max}}\ dt \tag{23}\\[2.0em] & C_{\small \textstyle ttc}=\frac{1}{T}{\large \textstyle \int} \frac{\big(TTC_{\small \textstyle max}-TTC(t)\big)^{2}}{TTC_{(\small \textstyle max}-TTC_{\small \textstyle min})^{2}} \tag{24} \end{align}$$
> >
> > TG 모델이 특정 상황에서 가변 속도 프로파일을 선택할 수 있도록 하기 위해 [^1]에 TTC(충돌 시간) 비용이 추가되었습니다. 이는 Fig (9)에 표시된 대로 정의됩니다. 이를 도입함으로써 몇 가지 이점이 있습니다. 첫째, 안전 관점에서 다른 지표와 구별됩니다. 예를 들어, 교통 체증 시나리오에서는 자율주행차의 감속이 필요합니다. 그러나 TTC 없이는 볼록 공식이 일정한 프로파일보다 총 비용을 증가시키기 때문에 최적 해결책으로 속도 감소 프로파일을 결정하는 것이 불가능합니다.
> 
> > [!list]- d) 실현 불가능성 검사
> > 
> > 궤적 후보를 생성할 때 비모델 기반 샘플링 방법을 적용합니다. 따라서 동적 제약 조건(타이어 동역학...)을 초과하거나 다른 물체와 충돌하는 실현 불가능성의 위험이 있습니다. 첫 번째 위험은 저크, 가속도 비용 함수로 방지됩니다. 하지만 두 번째는 그렇지 않습니다. 각각에 대해 충돌 검사가 필요합니다. 이미 가장 위험한 객체(MIO)에 대한 정보를 가지고 있기 때문에 동일한 시간 단계에서 충돌을 확인할 수 있습니다. 이 알고리즘은 Fig (10)에 나와 있습니다.
> > 
> > RMC에서 TG까지의 전체 프로세스를 통해 최종 최적 궤적이 주어집니다. 이는 전역 좌표계로 변환되어 자율주행차에 전송됩니다.
> > 
> > > [!math]- 
> > > 
> > > $$\begin{bmatrix} s,\ ds,\ dds,\ l,\ dl,\ ddl \end{bmatrix} \to \begin{bmatrix} x,\ y,\ vel,\ acc,\ \psi,\ k \end{bmatrix} \tag{25} $$

> [!fig]- Fig. 9.

<p style='margin-top: 2em; margin-bottom: 2em'></p>

## Simulation results 

> [!check]- 시뮬레이션 설정
> 
> 우리는 주변 차량의 관점에서 선형 운동과 "복잡한 장면"이라고 불리는 차선 변경 운동을 구분했습니다. 초기 설정은 다음과 같습니다: $v_{{\small \textstyle ego},0}=50\text{km/h} \sim 80\text{km/h},\ a_{{\small \textstyle ego},0}=0$. 주변 차량은 등속도를 가정합니다. 차선 변경 시나리오에서 그들의 궤적은 자차와 동일한 방식으로 모델링됩니다. 예측 시간은 3초이며 RMC 경계는 $\begin{bmatrix} -50,\ 50 \end{bmatrix}$입니다. 
> 
> 시뮬레이션은 단일 장면을 위한 MATLAB과 연속적인 장면을 제공하는 Driving scenario Add-on을 사용하는 SIMULINK에서 실행되었습니다. 이러한 시나리오 동안, 우리는 알고리즘의 성능 검증을 위해 속도와 가속도 프로파일, 안전 거리, 선호 차선을 확인했습니다. 가중치 매개변수 튜닝을 위해 다양한 고정 장면에서 먼저 진행한 후, 연속적인 시퀀스를 고려했습니다. 이러한 장면에서의 결과는 등속도를 가정한 이전 모델[^1]과 비교되었습니다.
> 
> 수치적 비용을 정규화하고 각 사례에 대한 영향을 명확하게 제시함으로써 사례 연구를 용이하게 하는 무차원 상수들이 사용되었습니다. 이 상수값은 [^2], [^3], [^5], [^6], [^8], [^9]에서 제시되었습니다. 이러한 연구들로부터 다음과 같은 값들이 도출되었습니다:
> 
> <table>
>   <tr>
>     <th rowspan='2'><span class="math display">a_{\small \textstyle max}</span></th>
>     <th colspan='2'><span class="math display">v</span></th>
>     <th colspan='2'><span class="math display">j</span></th>
>     <th rowspan='2'><span class="math display">k_{\small \textstyle max}</span></th>
>     <th colspan='2'><span class="math display">TTC</span></th>
>   </tr>
>   <tr>
>     <th><span class="math display">max</span></th>
>     <th><span class="math display">min</span></th>
>     <th><span class="math display">max,long</span></th>
>     <th><span class="math display">min,lat</span></th>
>     <th><span class="math display">max</span></th>
>     <th><span class="math display">min</span></th>
>   </tr>
>   <tr>
>     <td><span class="math display">3\mathrm{m}/s^{2}</span></td>
>     <td><span class="math display">110km/\mathrm{h}</span></td>
>     <td><span class="math display">50km/\mathrm{h}</span></td>
>     <td><span class="math display">2.94m/s^{3}</span></td>
>     <td><span class="math display">0.9m/s^{3}</span></td>
>     <td><span class="math display">0.146\,{\small \dfrac{1}{m}}</span></td>
>     <td><span class="math display">5s</span></td>
>     <td><span class="math display">2.2s</span></td>
>   </tr>
> </table>

> [!note]- 빠른 선행 차량 추종
> 
> 주변 교통이 자차보다 빠를 때, 차량은 교통 흐름을 따라가기 위해 가속해야 합니다. 이에 따라, TDM 모듈은 자차보다 높은 경계 조건을 생성하고, 위험한 경로가 아닌 한 TG 모듈이 이를 잘 선택할 수 있습니다. 안정성보다는 목표 속도를 잘 따르도록 설계 매개변수가 설정됩니다.

> [!note]- 선행 차량으로부터의 안전 거리 유지
> 
> 교통 체증 시에는 주행 안전 문제가 부각됩니다. 일정 수준 이상의 안전 거리를 유지하기 위해 자차는 속도를 감소시켜야 합니다. 따라서 선택 작업이 진행될 때 안전과 관련된 가중치 매개변수가 다른 것들보다 가장 큽니다. Fig (12). 환경이 대부분 안정성을 요구하기 때문에 안전 관련 가중치가 강조됩니다.
> 
> > [!math]- 
> > 
> > $$\begin{Bmatrix} w_{\small \textstyle v},\ w_{\small \textstyle a},\ w_{\small \textstyle j},\ w_{\small \textstyle k},\ w_{\small \textstyle ttc} \end{Bmatrix}_{TG}=\begin{Bmatrix} 1,\ 1,\ 1,\ 3,\ 0.5,\ 3.5 \end{Bmatrix}$$

> [!note]- 차선 변경
> 
> 현재 차선보다 더 안전하거나 더 편안하게 주행할 수 있는 차선이 있다면, 자율주행차는 해당 차선으로 이동해야 합니다. 자율주행차는 종종 고속도로 출구로 가거나 특정 경로를 따라가기 위해 주행합니다. 이러한 이유로, 고속도로에서도 차선 변경 작업은 불가피합니다. 고차 다항식 횡방향 궤적 모델 덕분에, Fig (13)에서 보이는 것처럼 전체적인 경로가 부드럽습니다.

> [!note]- 복잡한 시나리오
> 
> 다른 차량들의 차선 변경 상황이 이 범주에 속합니다. 변화된 환경 데이터의 영향은 Figure (14)에서 확인할 수 있습니다. 보이는 바와 같이, 이 장면은 먼저 예측 부분에 영향을 미칩니다. 예측 부분이 MIO 블록 찾기와 안전 간격 블록 만들기와 밀접하게 관련되어 있기 때문에, 이들도 민감하게 반응합니다. 결과적으로 속도 프로파일의 경계 조건 생성, 충돌 검사, TTC 계산과 같이 MIO에 의존하는 블록들이 순차적으로 영향을 받습니다. 마찬가지로, 교통 정보를 직접 사용하는 도로 비용과 교통 비용과 같은 TDM 비용도 영향을 받습니다. 이는 한 블록의 변화가 시스템의 다른 부분에 연쇄적인 영향을 미치는 구조임을 나타냅니다. "예측 궤적"과 "MIO 찾기" 알고리즘의 견고성 덕분에 이러한 복잡한 시나리오를 해결할 수 있습니다. 결과는 Fig(15)에서 확인할 수 있습니다.

> [!note]- 연속 시뮬레이션
> 
> 마지막으로 SIMULINK를 사용하여 연속적인 환경에서 이 알고리즘을 검증합니다. 특히, 이전 연구[^1]와 비교하기 위해 원래의 시나리오에 교통 체증 시나리오가 추가되었습니다. 다양한 프로파일이 Fig. (17)에 표시되어 있습니다. 파란색 선이 과정 중에 끊어진 것을 볼 수 있는데, 이는 시뮬레이션 중 다른 차량과 자차 사이의 충돌이 감지되어 시뮬레이션이 중단된 경우를 나타냅니다. 해당 지점이 충돌 지점입니다.

<p style='margin-top: 2em; margin-bottom: 2em'></p>

## Conclusion and Future work 
> [!summary]- 
> 
> 다양한 시뮬레이션 결과를 통해, 이 알고리즘이 단순한 차선 변경부터 복잡한 가속 또는 감속까지 다양한 작업을 처리할 수 있음을 확인했습니다. 다시 말해, 수정된 TDM & TG 모듈은 차선 변경과 관련된 단일 작업뿐만 아니라 목표 추적과 관련된 다른 작업도 동시에 수행할 수 있습니다.
> 
> 향후 연구에서는, [^7]과 유사하게 다른 비용들과 독립적인 일관성을 이 모듈에 추가함으로써 연속적인 환경에 대해 더욱 견고한 TDM 모델을 개발할 계획입니다. 또한, 실현 불가능성을 완전히 차단하기 위해 동적 모델을 사용하는 마르코프 시퀀스나 MPC(Model Predictive Control)와 같은 최적화 전략과 같은 모델 기반 계획을 도입할 예정입니다.

<p style='margin-top: 2em; margin-bottom: 2em'></p>

## Reference 
[^1]: Z. Feng, W. Song, M. Fu, Y. Yang and M. Wang, "De-cision-Making and Path Planning for Highway Auton-omous Driving Based on Spatio-Temporal Lane-Change Gaps," in _IEEE Systems Journal_, vol. 16, no. 2, pp. 3249-3259, June 2022.

[^2]: Yan, Shengyu & Liu, Chenglong & Cao, Jing. (2021). Comfort-Based Trajectory and Velocity Planning for Automated Vehicles Considering Road Conditions. In-ternational Journal of Automotive Technology. 22. 883-893.

[^3]: Chen, J.; Zhao, C.; Jiang, S.; Zhang, X.; Li, Z.; Du, Y. Safe, Efficient, and Comfortable Autonomous Driving Based on Cooperative Vehicle Infrastructure Sys-tem. _Int. J. Environ. Res. Public Health_ **2023**, _20_, 893.

[^4]: Alipour Sormoli, Mreza & Koufos, Konstantinos & Dianati, Mehrdad & Woodman, Roger. (2024). “A Sur-vey on Hybrid Motion Planning Methods for Auto-mated Driving Systems”.

[^5]: Bae, I.; Moon, J.; Seo, J. Toward a Comfortable Driv-ing Experience for a Self-Driving Shuttle Bus. _Elec-__tronics_ **2019**, _8_, 943.

[^6]: Zhang, Y.; Chen, H.; Waslander, S.L.; Yang, T.; Zhang, S.; Xiong, G.; Liu, K. Toward a More Complete, Flex-ible, and Safer Speed Planning for Autonomous Driv-ing via Convex Optimization. _Sensors_ **2018**, _18_, 2185.

[^7]: Esterle, Klemens & Hart, Patrick & Bernhard, Julian & Knoll, Alois. (2022). Spatiotemporal motion planning with combinatorial reasoning for autonomous driving.

[^8]: [별표 12] 전방충돌경고장치 시험방법 및 평가 방법(자동차 안전도 평가 시험 등에 관한 규정)

[^9]: https://blog.naver.com/jjz0426, “vehicle low speed cornering and Ackerman geometry model”
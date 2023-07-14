# Kubernetes



## Kubernetes cluster

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>kubernetes cluster (from kubernetes.io)</p></figcaption></figure>

쿠버네티스는 **클러스터의 집합**으로 이루어진다.

* **쿠버네티스 클러스터**는 애플리케이션을 실행하는 **(워커)노드**라고 불리는 머신의 집합으로, **모든 쿠버네티스 클러스터는 적어도 하나의 노드**를 가진다.
* **(워커)노드는** 일반적으로 애플리케이션 워크로드의 구성요소 중 하나인 **파드를 호스트**한다.



## Control plane component

컨트롤 플레인은 클러스터에 대한 전반적인 결정(스케쥴링, 스케일링)을 수행한다. 일반적으로, 성능 및 보안 측면에서 이점을 가져가기 위해 워커 노드가 아닌 별도의 노드에서 실행된다.

### kube-apiserver

API 서버는 쿠버네티스 API를 노출하는 쿠버네티스 컨트롤 플레인의 프론트엔드에 해당한다. 쿠버네티스 API로 사용되는 주요 구현은 kube-apiserver이다. kube-apiserver는 scale-out이 가능하며, 이를 통해 인스턴스간의 트래픽을 균형있게 조절할 수 있는 특징을 가지고 있다.

### etcd

모든 클러스터 데이터를 저장하는 쿠버네티스의 백엔드 저장소로, 고가용성 key-value 저장소이다.

### kube-scheduler

노드가 배정되지 않은 신규 파드를 감지하고 실행할 노드를 선택하는 컨트롤 플레인 컴포넌트

### kube-controller-manager

다음의 컨트롤러 프로세스를 실행하는 컴포넌트

* Node controller: 노드가 다운되었을 때, 이를 감지하고 알리는 역할을 한다.
* Job controller: 일회성 작업을 나타내는 Job object를 모니터링하면서, 해당 작업이 완료될 때까지 동작하는 파드를 생성한다.
* EndpointSlice controller: 서비스와 파드간의 링크를 제공하는 EndpointSlice objects를 관리한다.
* ServiceAccount controller: 새로운 네임스페이스에 대한 기본 서비스 어카운트를 생성한다.

### cloud-controller-manager

클라우드별 제어 로직을 가진 컴포넌트로, 쿠버네티스 클러스터와 클라우드 플랫폼의 API를 연결해준다. 해당 클라우드 플랫폼과 상호작용해야하는 컴포넌트와 클러스터 내부에서만 상호작용하는 컴포넌트를 구분할 수 있게 해준다.

구체적으로는 아래와 같은 컨트롤러들이 클라우드 플랫폼에 대해 의존성을 가질 수 있다.

* Node controller: 노드가 응답을 멈춘 후, 클라우드 상에서 삭제되었는지 판별하기 위해 클라우드 플랫폼에 확인하는 것
* Route controller: 클라우드 인프라에 대해 라우팅을 설정 하는 것
* Service controller: 클라우드 플랫폼의 로드밸런서를 생성/수정/삭제하는 것

##

## Node component

노드 컴포넌트는 실행중인 파드를 유지시키고, 쿠버네티스 런타임 환경을 제공하며, 모든 노드상에서 동작한다.

### kubelet

각 노드에서 실행되는 에이전트로, 파드에서 컨테이너가 제대로 실행될 수 있도록 관리한다. 주어진 PodSpec(livenessProbe, readnessProbe 등)에 따라 컨테이너가 제대로 동작하도록 관리한다.

### kube-proxy

클러스터의 각 노드에서 실행되는 네트워크 프록시로, 쿠버네티스의 서비스 개념의 구현부이다. 내부 네트워크 세션이나, 클러스터 외부와의 통신이 가능하도록 파드가 네트워크 통신이 가능하도록 포워딩해준다.

### CRI

CRI는 Container runtime interface로 컨테이너 실행을 담당하는 소프트웨어이다. docker, containered, CRI-O와 같은 소프트웨어들이 이에 해당한다.



## Addon

이어서...



## Reference

* https://kubernetes.io/ko/docs

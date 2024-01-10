# GitOps with ArgoCD

간단한 리액트 앱을 도커 이미지로 빌드 하고 쿠버네티스 클러스터에 배포하는 과정을 자동화 합니다.

## 디렉터리 구조

### /react-app

리액트 앱 소스

### /helm-charts

리액트 앱 헬름 차트

### /gitops

배포를 위한 ArgoCD 차트와 Application 정의

## App of Apps 패턴

- 배포상태를 git으로 관리하기 위해 루트 앱을 선언한 app-of-apps.yaml 파일을 gitops/argo-cd/templates에 포함시킵니다.
- helm으로 ArgoCD를 gitops/argo-cd로 인스톨하면 app-of-apps.yaml의 Application도 함께 생성됩니다.
- argo-cd 자체도 Application으로 등록합니다.

## 실행 방법

쿠버네티스 클러스터가 구성되고, helm이 설치되어 있어야 합니다.

1. 네임스페이스 argocd, react-app 생성

```
kubectl create ns argocd, react-app
```

2. 레포지토리 pull

```
git pull https://github.com/stlee321/gitops-with-argocd.git
```

3. 폴더 내부로 이동

```
cd gitops-with-argocd
```

4. helm으로 argocd 네임스페이스로 클러스터에 ArgoCD 인스톨

```
helm install argocd ./gitops/argo-cd -n argocd
```

5. 리액트 앱 접속하기

```
minikube의 경우 minikube tunnel 실행 후 ingress 접속(localhost)
```

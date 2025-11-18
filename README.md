# ✨ Webstack 프로젝트 ✨

이 프로젝트는 Kubernetes를 사용하여 배포 🚀 되고 Argo CD로 관리 🧮 되는 웹 스택 애플리케이션을 정의합니다.

## 📚 개요 📚

웹 스택은 다음 구성 요소로 구성됩니다 👇 :

*   **nginx**: 웹 서버 🌐 및 리버스 프록시 🔄.
*   **redis**: 인 메모리 데이터 구조 저장소 💾 로, 데이터베이스 🗄️, 캐시 ⚡ 및 메시지 브로커 ✉️ 로 사용됩니다.
*   **cadvisor**: 실행 중인 컨테이너 📦 의 리소스 사용량 📊 및 성능 특성 ⚙️ 을 분석합니다.

## 📁 디렉토리 구조 📁

*   `base`: 각 구성 요소에 대한 기본 구성 ⚙️ 을 포함합니다.
    *   `cadvisor`: (구성 정보가 제공되지 않았습니다 😥. `cadvisor` 디렉토리를 찾아보세요 👀.)
    *   `nginx`: nginx에 대한 기본 배포 🚀 및 서비스 정의 📄를 포함합니다.
        *   `deployment.yaml`: nginx 배포 🚀를 정의합니다.
        *   `service.yaml`: nginx 서비스 🌐를 정의합니다.
        *   `kustomization.yaml`: 리소스 묶고 📦 nginx에 대한 공통 레이블 🏷️ 을 정의합니다.
    *   `redis`: redis에 대한 기본 배포 🚀 및 서비스 정의 📄를 포함합니다.
        *   `deployment.yaml`: redis 배포 🚀를 정의합니다.
        *   `service.yaml`: redis 서비스 🌐를 정의합니다.
        *   `kustomization.yaml`: 리소스 묶고 📦 redis에 대한 공통 레이블 🏷️ 을 정의합니다.
    *   `kustomization.yaml`: 기본 웹 스택을 구성하는 리소스 목록 🧾입니다.
*   `overlays`: 환경별 사용자 정의 🎨 를 포함합니다.
    *   `dev`: 개발 환경 💻 에 특정한 구성을 포함합니다.
        *   `kustomization.yaml`: 기본 구성 ⚙️ 을 포함하고 패치 🩹를 적용합니다.
        *   `patch.yaml`: 개발 환경 💻 에서 cadvisor, nginx 및 redis 배포의 복제본 수를 재정의합니다.
    *   `prod`: 프로덕션 환경 🏭 에 특정한 구성을 포함합니다.
        *   `patch.yaml`: 프로덕션 환경 🏭 에서 cadvisor (1개 복제본), nginx (3개 복제본) 및 redis (1개 복제본) 배포의 복제본 수를 재정의합니다.
*   `argocd`: Argo CD 애플리케이션 정의 📝 를 포함합니다.
    *   `webstack-prod.yaml`: `webstack-prod` 네임스페이스에 웹 스택을 배포하기 위한 Argo CD 애플리케이션을 정의하며, 지정된 Git 리포지토리 📦 의 `webstack/overlays/prod` 경로에서 가져옵니다. 또한 가지치기 ✂️ 및 자가 치유 ⛑️ 가 활성화된 자동 동기화 정책 🔄을 구성합니다.

## 🚀 배포 🚀

이 애플리케이션은 Kubernetes 리소스의 배포 및 관리를 자동화하는 Argo CD를 사용하여 배포됩니다 🚀.

*   `webstack-prod.yaml` 파일은 `webstack/overlays/prod` 디렉토리에 정의된 리소스를 `webstack-prod` 네임스페이스에 배포하는 Argo CD 애플리케이션을 정의합니다.
*   `webstack-prod.yaml`의 `syncPolicy`는 자동 동기화 🔄, 오래된 리소스 정리 🗑️ 및 수동 변경 사항을 되돌리기 위한 자가 치유 ⛑️를 활성화합니다.

## ⚙️ 사용자 정의 ⚙️

`overlays` 디렉토리를 사용하면 기본 구성에 대한 환경별 사용자 정의가 가능합니다 🎨. 각 환경 (예 : `dev`, `prod`)은 복제본 수, 리소스 제한 또는 환경 변수와 같은 설정을 재정의하는 패치 🩹 를 정의 할 수 있습니다. 이러한 패치는 `base` 디렉토리에 정의된 기본 구성 ⚙️ 위에 적용됩니다.

## ℹ️ 추가 정보 ℹ️

자세한 내용은 다음을 참조하십시오 👇 :

*   **Argo CD:** Argo CD 설명서를 참조하십시오 📚.
*   **Kustomize:** Kustomize 설명서를 참조하십시오 📚.
*   **Kubernetes:** Kubernetes 설명서를 참조하십시오 📚.
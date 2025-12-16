# AI-DLC (AI 기반 개발 생명주기)

AI-DLC는 사용자의 요구에 맞게 적응하고, 품질 표준을 유지하며, 프로세스 전반에 걸쳐 제어권을 유지할 수 있는 지능형 소프트웨어 개발 워크플로우입니다. AI-DLC 방법론에 대해 더 자세히 알아보려면 이 [블로그](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)와 해당 블로그에서 참조하는 [방법론 정의 문서](https://prod.d13rzhkk8cj2z0.amplifyapp.com/)를 읽어보세요.

## 빠른 시작

[지원 플랫폼](#사전-요구-사항)의 일부로 AI-DLC 규칙/스티어링 파일을 설정하세요.

이 저장소를 복제합니다:
```bash
git clone <this-repo>
```

새로운 프로젝트(그린필드 애플리케이션)를 시작하는 경우 원하는 이름으로 새 프로젝트 폴더를 생성합니다:
```
mkdir <my-project>
```

프로젝트가 복제된 `aidlc-workflows` 저장소와 동일한 상위 폴더에 있다고 가정하고, 프로젝트 폴더로 디렉토리를 변경합니다:
```bash
cd <my-project>
```

### Amazon Q Developer IDE 플러그인/확장 프로그램

AI-DLC는 [Amazon Q 규칙](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/context-project-rules.html)을 사용하여 지능형 워크플로우를 구현합니다. 프로젝트에서 AI-DLC를 활성화하려면 규칙을 프로젝트 워크스페이스의 `<project-root>/.amazonq` 폴더에 복사하세요.

AI-DLC 워크플로우를 프로젝트 워크스페이스의 `<project-root>/.amazonq` 폴더에 복사합니다:
```
mkdir -p .amazonq/rules
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rules .amazonq/rules/
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rule-details .amazonq/
```

Amazon Q 규칙이 IDE에 올바르게 로드되었는지 확인하려면 다음 단계를 따르세요:

1. Amazon Q 채팅 창에서 오른쪽 하단의 `Rules` 버튼을 찾아 클릭합니다.
2. 표시된 규칙 목록에서 `.amazonq/rules/aws-aidlc-rules` 항목이 있는지 확인합니다.

`aws-aidlc-rules` 규칙이 로드되지 않은 경우, 이전에 `mkdir` 및 `cp` 명령을 실행한 디렉토리를 확인하세요.

![Q Developer IDE의 AI-DLC 규칙](./assets/images/q-ide-aidlc-rules-loaded.png?raw=true "Q Developer의 AI-DLC 규칙")

### Kiro CLI

AI-DLC는 프로젝트 워크스페이스 내의 [Kiro 스티어링 파일](https://kiro.dev/docs/cli/steering/)을 사용하여 지능형 워크플로우를 구현합니다. 프로젝트에서 AI-DLC를 활성화하려면 규칙을 프로젝트 워크스페이스의 `<your-project-root>/.kiro/steering` 폴더에 복사하세요.

AI-DLC 워크플로우를 프로젝트 워크스페이스의 `<project-root>/.kiro` 폴더에 복사합니다:

```bash
mkdir -p .kiro/steering
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rules .kiro/steering/
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rule-details .kiro/
```

AI-DLC 규칙이 Kiro CLI에 올바르게 로드되었는지 확인하려면 다음 단계를 따르세요:

1. Kiro CLI 시작: `kiro-cli`
2. 컨텍스트 내용 확인: `/context show`
3. 표시된 규칙 목록에서 `.kiro/steering/aws-aidlc-rules`의 모든 항목이 있는지 확인합니다.

`aws-aidlc-rules` 규칙이 로드되지 않은 경우, 이전에 `mkdir` 및 `cp` 명령을 실행한 디렉토리를 확인하세요.

![Kiro CLI의 AI-DLC 규칙](./assets/images/kiro-cli-aidlc-rules-loaded.png?raw=true "Kiro CLI의 AI-DLC 규칙")

### 사용 방법

1. 채팅에서 "Using AI-DLC, ..."라는 문구로 시작하여 소프트웨어 개발 프로젝트의 의도를 말합니다.
2. AI-DLC 워크플로우가 자동으로 활성화되어 그곳에서부터 안내합니다.
3. AI-DLC가 묻는 구조화된 질문에 답변합니다.
4. AI가 생성하는 모든 계획을 신중하게 검토합니다. 감독과 검증을 제공하세요.
5. 실행 계획을 검토하여 어떤 단계가 실행될지 확인합니다.
6. 산출물을 신중하게 검토하고 각 단계를 승인하여 제어권을 유지합니다.
7. 모든 산출물은 `aidlc-docs/` 디렉토리에 생성됩니다.

## 3단계 적응형 워크플로우

AI-DLC는 프로젝트의 복잡성에 맞게 적응하는 구조화된 3단계 접근 방식을 따릅니다:

- **🔵 INCEPTION 단계**: **무엇을** 만들고 **왜** 만드는지 결정
  - 요구사항 분석 및 검증
  - 사용자 스토리 작성 (해당되는 경우)
  - 애플리케이션 설계 및 병렬 개발을 위한 작업 단위 생성
  - 리스크 평가 및 복잡성 평가

- **🟢 CONSTRUCTION 단계**: **어떻게** 만들지 결정
  - 상세 컴포넌트 설계
  - 코드 생성 및 구현
  - 빌드 구성 및 테스트 전략
  - 품질 보증 및 검증

- **🟡 OPERATIONS 단계**: 배포 및 모니터링 (향후)
  - 배포 자동화 및 인프라
  - 모니터링 및 관측성 설정
  - 프로덕션 준비 검증

## 주요 기능

- **적응형 지능**: 특정 요청에 가치를 더하는 단계만 실행
- **컨텍스트 인식**: 기존 코드베이스와 복잡성 요구사항 분석
- **리스크 기반**: 복잡한 변경에는 포괄적인 처리, 단순한 변경은 효율적으로 유지
- **질문 중심**: 채팅이 아닌 파일에 구조화된 객관식 질문
- **항상 제어권 유지**: 실행 계획 검토 및 각 단계 승인

## 사전 요구 사항

지원되는 AI 코딩 보조 플랫폼/도구 중 하나를 설치하세요:

- [Kiro CLI](https://kiro.dev/cli/)
- [Amazon Q Developer IDE 플러그인](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/q-in-IDE.html)
- [Kiro IDE](https://kiro.dev/) (출시 예정)

## 보안

자세한 내용은 [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications)을 참조하세요.

## 라이선스

이 라이브러리는 MIT-0 라이선스에 따라 라이선스가 부여됩니다. LICENSE 파일을 참조하세요.

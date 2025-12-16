# 세션 연속성 템플릿

## 재방문 프롬프트 템플릿
사용자가 기존 AI-DLC 프로젝트에서 작업을 계속하기 위해 돌아올 때 이 프롬프트를 표시합니다:

```markdown
**다시 오신 것을 환영합니다! 진행 중인 기존 AI-DLC 프로젝트가 있습니다.**

aidlc-state.md를 기반으로 현재 상태는 다음과 같습니다:
- **프로젝트**: [프로젝트 이름]
- **현재 단계**: [INCEPTION/CONSTRUCTION/OPERATIONS]
- **현재 스테이지**: [스테이지 이름]
- **마지막 완료**: [마지막으로 완료된 단계]
- **다음 단계**: [작업할 다음 단계]

**오늘 무엇을 작업하시겠습니까?**

A) 중단한 곳에서 계속 ([다음 단계 설명])
B) 이전 스테이지 검토 ([사용 가능한 스테이지 표시])

[Answer]:
```

## 필수: 세션 연속성 지침
1. **기존 프로젝트 감지 시 항상 aidlc-state.md를 먼저 읽기**
2. **워크플로우 파일에서 현재 상태를 파싱**하여 프롬프트 채우기
3. **필수: 이전 스테이지 산출물 로드** - 모든 스테이지를 재개하기 전에 이전 스테이지의 모든 관련 산출물을 자동으로 읽기:
   - **역공학**: architecture.md, code-structure.md, api-documentation.md 읽기
   - **요구사항 분석**: requirements.md, requirement-verification-questions.md 읽기
   - **사용자 스토리**: stories.md, personas.md, story-generation-plan.md 읽기
   - **애플리케이션 설계**: 애플리케이션 설계 산출물 읽기 (components.md, component-methods.md, services.md)
   - **설계 (유닛)**: unit-of-work.md, unit-of-work-dependency.md, unit-of-work-story-map.md 읽기
   - **유닛별 설계**: functional-design.md, nfr-requirements.md, nfr-design.md, infrastructure-design.md 읽기
   - **코드 스테이지**: 모든 코드 파일, 계획 및 모든 이전 산출물 읽기
4. **스테이지별 스마트 컨텍스트 로딩**:
   - **초기 스테이지 (워크스페이스 감지, 역공학)**: 워크스페이스 분석 로드
   - **요구사항/스토리**: 역공학 + 요구사항 산출물 로드
   - **설계 스테이지**: 요구사항 + 스토리 + 아키텍처 + 설계 산출물 로드
   - **코드 스테이지**: 모든 산출물 + 기존 코드 파일 로드
5. **아키텍처 선택과 현재 단계에 따라 옵션 조정**
6. **일반적인 설명 대신 구체적인 다음 단계 표시**
7. **연속성 프롬프트를 타임스탬프와 함께 audit.md에 기록**
8. **컨텍스트 요약**: 산출물 로드 후 사용자 인식을 위해 로드된 내용의 간략한 요약 제공
9. **질문하기**: 항상 명확화 또는 사용자 피드백 질문을 .md 파일에 배치하세요. 채팅 세션에서 인라인으로 객관식 질문을 배치하지 마세요.

## 오류 처리
세션 재개 중 산출물이 누락되거나 손상된 경우, 복구 절차에 대한 안내는 [error-handling.md](error-handling.md)를 참조하세요.

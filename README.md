# Multi-LLM Council v3.0

[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blueviolet)](https://github.com/hadamyeedady12-dev/multi-llm-council)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> 다중 LLM CLI를 활용한 집단 지성 협의 시스템

Claude Code가 의장으로서 Gemini CLI, Codex CLI를 조율하여 **추가 API 비용 없이** 통합 협의 프로세스를 진행합니다.

## v3.0 - 단일 명령어 통합

**이전:** `/council`, `/council-quick`, `/council-expert` 3개 분리
**현재:** `/council` 하나로 최대 출력 모드 통합

## 사용법

```
/council <질문>
```

**단 하나의 명령어로 모든 기능을 최대 성능으로 실행합니다.**

## 특징

- **무비용**: 기존 CLI 구독만으로 운영
- **집단 지성**: 3개 LLM의 역할 기반 분석
- **익명 평가**: 편향 없는 교차 검증
- **투명성**: 모든 과정과 근거 공개
- **구조화**: JSON 형식으로 안정적인 파싱
- **최대 출력**: 전문가 분석 + 교차 평가 + 종합 결론

## 설치

### 요구사항

```bash
# Gemini CLI
brew install gemini-cli
gemini auth login

# Codex CLI
npm install -g @openai/codex
codex login

# Claude Code
npm install -g @anthropic-ai/claude-code
```

### 플러그인 설치

#### 방법 1: 마켓플레이스 (권장)

```
/plugin marketplace add https://github.com/hadamyeedady12-dev/multi-llm-council
/plugin install council
```

#### 방법 2: 직접 클론

```bash
cd ~/.claude/plugins
git clone https://github.com/hadamyeedady12-dev/multi-llm-council.git
```

설치 후 Claude Code를 재시작하세요.

## 통합 3단계 프로세스

```
┌─────────────────────────────────────────────┐
│         Multi-LLM Council v3.0               │
│           최대 출력 통합 모드                  │
├─────────────────────────────────────────────┤
│                                             │
│  Stage 1: 역할 기반 병렬 의견 수집             │
│  ├── Gemini (보안/성능) ─┐                   │
│  ├── Codex (구현/실용)  ─┼─ 동시 실행         │
│  └── Claude (UX/아키텍처)─┘                  │
│                                             │
│  Stage 2: 익명 교차 평가                      │
│  ├── 응답 익명화 (A, B, C)                   │
│  ├── 100점 척도 평가                         │
│  └── 순위 집계                               │
│                                             │
│  Stage 3: 최종 종합                          │
│  ├── 역할별 분석 통합                         │
│  ├── 우선순위별 권장사항                      │
│  ├── 신뢰도 계산                             │
│  └── 종합 결론                               │
│                                             │
└─────────────────────────────────────────────┘
```

## 위원 구성

| 위원 | CLI 명령어 | 모델 | 역할 |
|------|-----------|------|------|
| Gemini | `gemini --yolo` | gemini-3-pro-preview | 보안/성능 전문가 |
| Codex | `codex exec` | gpt-5.2-codex | 구현/실용성 전문가 |
| Claude | (내장) | claude-opus-4.5 | UX/아키텍처 전문가 (의장) |

## 평가 기준 (100점 만점)

| 항목 | 비중 | 설명 |
|------|------|------|
| 정확성 | 30% | 사실 정확성, 검증 가능성 |
| 깊이 | 25% | 근본 원인 분석, 다각적 관점 |
| 실용성 | 25% | 적용 가능성, 구체적 예시 |
| 명료성 | 20% | 논리 구조, 간결함 |

## 신뢰도 계산

```
신뢰도 = (합의율 × 0.4) + (평균점수/100 × 0.3) + (근거품질 × 0.3)

합의율:
- 높음 (0.9): 3명 모두 동일 결론
- 중간 (0.6): 2명 동의
- 낮음 (0.3): 모두 다른 의견

등급:
- 0.8+: 높음
- 0.5-0.8: 중간
- 0.5 미만: 낮음 (추가 검토 권장)
```

## 에러 처리

| 상황 | 처리 |
|------|------|
| CLI 실패 | Exponential Backoff 2회 재시도 |
| 위원 1명 실패 | 2인 위원회로 진행 |
| 2명 미만 응답 | 세션 중단, 사용자 알림 |
| JSON 파싱 실패 | 자유 형식으로 폴백 |
| 타임아웃 | 120초/위원 |

## 출력 예시

```markdown
# LLM 위원회 결론 (최대 출력)

## 질문
Python과 Go 중 어떤 언어가 백엔드에 더 적합한가?

## Stage 1: 전문가별 분석

### 보안/성능 전문가 (Gemini)
**보안:** Go의 메모리 안전성 우수
**성능:** Go가 동시성 처리에 강점

### 구현/실용성 전문가 (Codex)
**구현:** Python이 빠른 개발에 유리
**품질:** 풍부한 라이브러리 생태계

### UX/아키텍처 전문가 (Claude)
**확장성:** 마이크로서비스는 Go 적합
**유연성:** Python은 프로토타이핑에 적합

## Stage 2: 교차 평가
| 위원 | 정확성 | 깊이 | 실용성 | 명료성 | 총점 |
|------|--------|------|--------|--------|------|
| Gemini | 28/30 | 22/25 | 23/25 | 18/20 | 91 |
| Codex | 27/30 | 24/25 | 22/25 | 19/20 | 92 |
| Claude | 29/30 | 23/25 | 24/25 | 18/20 | 94 |

## Stage 3: 최종 결론

### 우선순위별 권장사항
1. **즉시 실행:** 프로젝트 요구사항 명확화
2. **단기 개선:** 팀 기술 스택 고려
3. **장기 고려:** 확장성 계획 수립

### 신뢰도
점수: 0.85
등급: 높음
```

## 핵심 원칙

1. **독립성** - 각 위원은 역할 기반으로 독립적으로 분석
2. **익명성** - 평가 시 응답자 신원 비공개
3. **투명성** - 모든 과정과 근거 공개
4. **합의 지향** - 다수결보다 논거의 질 중시
5. **구조화** - JSON 형식으로 파싱 안정성 확보

## 버전 히스토리

### v3.0 (2025-01-11)
- 단일 명령어 통합: `/council` 하나로 모든 기능
- 역할 기반 전문가 분석 기본 포함
- 완전한 3단계 프로세스 (교차 평가 포함)
- 최대 병렬 실행
- 우선순위별 권장사항 출력

### v2.0
- 병렬 실행 도입
- 구조화된 JSON 출력
- 평가 기준 명확화 (100점 척도)
- 신뢰도 계산 공식 추가

### v1.0
- 초기 버전
- 3개 분리 명령어 (council, council-quick, council-expert)

## 라이선스

MIT License

## 기여

이슈 및 PR 환영합니다!

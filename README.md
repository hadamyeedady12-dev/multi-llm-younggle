# Multi-LLM Council

> 다중 LLM CLI를 활용한 집단 지성 협의 시스템

Claude Code가 의장으로서 Gemini CLI, Codex CLI를 조율하여 **추가 API 비용 없이** 3단계 협의 프로세스를 진행합니다.

## 특징

- **무비용**: 기존 CLI 구독만으로 운영
- **집단 지성**: 3개 LLM의 관점 종합
- **익명 평가**: 편향 없는 교차 검증
- **투명성**: 모든 과정과 근거 공개

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

```bash
# Claude Code 플러그인 디렉토리에 클론
cd ~/.claude/plugins
git clone https://github.com/hadamyeedady12-dev/multi-llm-council.git
```

## 사용법

### 표준 위원회 (3단계 전체)

```
/council Python과 Go 중 어떤 언어가 백엔드에 더 적합한가?
```

### 신속 위원회 (Stage 2 생략)

```
/council-quick AI 윤리의 핵심 원칙은?
```

### 전문가 패널 (역할 기반)

```
/council-expert 마이크로서비스 아키텍처의 장단점은?
```

## 3단계 프로세스

```
┌─────────────────────────────────────────────┐
│              Multi-LLM Council               │
├─────────────────────────────────────────────┤
│                                             │
│  Stage 1: 독립적 의견 수집                   │
│  ├── Gemini (gemini-3-pro-preview)          │
│  ├── Codex (gpt-5.2-codex)                  │
│  └── Claude (claude-opus-4.5) - 의장         │
│                                             │
│  Stage 2: 익명 교차 평가                     │
│  ├── 응답 익명화 (Response A, B, C)          │
│  ├── 각 위원이 타 응답 평가                  │
│  └── 순위 집계                              │
│                                             │
│  Stage 3: 최종 종합                          │
│  ├── 합의점 도출                            │
│  ├── 이견 명시                              │
│  └── 신뢰도 평가                            │
│                                             │
└─────────────────────────────────────────────┘
```

## 위원 구성

| 위원 | CLI 명령어 | 모델 | 역할 |
|------|-----------|------|------|
| Gemini | `gemini --yolo` | gemini-3-pro-preview | 위원 |
| Codex | `codex exec` | gpt-5.2-codex | 위원 |
| Claude | (내장) | claude-opus-4.5 | 의장 |

## 출력 예시

```markdown
# 🏛️ LLM 위원회 결론

## 📋 질문
Python과 Go 중 어떤 언어가 백엔드에 더 적합한가?

## 👥 Stage 1: 위원 응답
[각 위원의 독립적 의견]

## ⚖️ Stage 2: 교차 평가
[익명 평가 결과 및 순위]

## 🎯 Stage 3: 최종 결론
### ✅ 합의 사항
### ⚠️ 이견 사항
### 📝 종합 결론
### 🔒 신뢰도: 높음
```

## 핵심 원칙

1. **독립성** - 각 위원은 타 의견 참고 없이 독립적으로 답변
2. **익명성** - 평가 시 응답자 신원 비공개
3. **투명성** - 모든 과정과 근거 공개
4. **합의 지향** - 다수결보다 논거의 질 중시

## 라이선스

MIT License

## 기여

이슈 및 PR 환영합니다!

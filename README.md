# gov-skills

한국 정부·지자체 지원사업 및 학교 민간위탁 제안서 작성 워크플로우.

신청 주체(**모아킷** / **스카이진로교육** / **컨소시엄**)에 따라 문서 구조와 서술 원칙을 자동으로 전환한다.

## 왜 필요한가

같은 공고라도 누구 명의로 쓰느냐에 따라 **문서 종류 자체가 바뀐다.**

| 명의 | 주로 지원하는 것 | 문서 구조 | 핵심 주장 |
|---|---|---|---|
| 모아킷 | 창업·R&D·사업화 지원사업 | PSST | *무엇을 만들 수 있는가* |
| 스카이진로교육 | 학교 진로체험 민간위탁 | 운영제안서 | *얼마나 안정적으로 굴릴 수 있는가* |
| 컨소시엄 | 지역 교육 협력 사업 | 사안별 | *역할 분담이 진짜인가* |

## 설치

**마켓플레이스 추가와 플러그인 설치는 별개의 두 단계다.**
마켓플레이스는 카탈로그 등록일 뿐이라, 추가만 하면 설치된 것은 없고 `/`를 쳐도 아무것도 뜨지 않는다.

### Claude Desktop (Code 탭)

1. 프롬프트 입력창 옆 **`+`** → **Plugins** → **Add plugin**
2. **Add marketplace from GitHub** → `themonsteredu/skill`
3. 목록에서 `gov-proposal` 설치
4. `gov-review`도 설치 — **두 개를 각각** 설치해야 한다

설치 후 `Run /reload-plugins to activate`가 뜨면 그것까지 실행하거나 세션을 새로 연다.

> 윈도우는 [Git for Windows](https://git-scm.com/downloads/win)가 먼저 설치돼 있어야 한다.
> WSL 세션과 클라우드 세션에서는 플러그인이 동작하지 않는다. **Local 세션**에서 쓴다.

### Claude Cowork (비개발자 권장)

1. 왼쪽 아래 **Customize**
2. **Browse plugins** → **Personal** → **+**
3. **Add marketplace from GitHub**
4. `themonsteredu/skill` 입력
5. 목록에서 `gov-proposal`, `gov-review`를 **각각 설치**

### Claude Code (CLI)

```
claude plugin marketplace add themonsteredu/skill
claude plugin install gov-proposal@gov-skills
claude plugin install gov-review@gov-skills
claude plugin list
```

마지막 줄에서 두 플러그인이 `enabled`로 나오면 끝이다.

### 이 저장소를 직접 열어서 쓸 때

`.claude/settings.json`에 마켓플레이스와 플러그인이 선언돼 있어서, 이 저장소를 연 세션에서는
자동으로 설치된다. 위 과정을 따로 할 필요가 없다.

## 쓰는 법

플러그인 커맨드에는 **플러그인 이름이 앞에 붙는다.** `/gov-draft`로는 뜨지 않는다.

```
/gov-proposal:gov-draft [공고문 첨부]     공고 → 초안 한 사이클
/gov-review:gov-review  [제안서 첨부]     제출 전 모의심사
```

입력창에 `/gov-proposal` 또는 `/gov-review`까지 치면 자동완성에 나온다.

스킬은 따로 부르지 않아도 관련 대화가 나오면 자동으로 읽힌다.

## 구조

```
gov-proposal/          문서 작성
  applicant-profile    누구 명의로, 어떤 문서인지 판별 ← 항상 첫 단계
  psst-structure       창업·R&D 사업계획서 구조
  entrust-structure    위탁운영 제안서 구조
  scoring-reverse      배점표 역산 → 목차·분량 재설계
  evidence-bank        실적 근거 인용 규칙

gov-review/            제출 전 검증
  judge-red-team       심사위원 시점 공격 + 자가채점

gov-brain/             내 자산 창고 (직접 채우는 곳)
  profiles/            기관 프로필 3종
  evidence/            실적·강사·보유자산·인증
  past/                과거 제출본 + 결과 + 사유
```

## 가장 중요한 것

**`gov-brain/`을 먼저 채운다.**

스킬은 프레임워크일 뿐이고, 제안서의 설득력은 인용 가능한 사실의 개수에서 나온다.
`gov-brain`이 비어 있으면 아무리 좋은 스킬도 빈 문장만 만든다.

채우는 순서:
1. `profiles/moakit.md` — 사업자 정보와 가점 요건
2. `evidence/실적-학교출강.md` — 수행 실적 표
3. `evidence/강사진.md` — 강사풀 명수와 관리 체계
4. 나머지

`[확인필요]`로 표시된 칸이 곧 작업 목록이다.

## 원칙

- 실적과 수치를 지어내지 않는다. 없으면 `[확인필요]`로 남긴다.
- 두 기관의 실적을 합산하지 않는다. 허위 기재는 선정 취소 사유다.
- 형식 요건(분량·서식·첨부·기한) 위반은 내용과 무관하게 탈락이다. 항상 먼저 확인한다.

## 참조

구조는 [phuryn/pm-skills](https://github.com/phuryn/pm-skills) (MIT)의 marketplace / plugin / skill / command 3층 구조를 참고했다.

## License

MIT

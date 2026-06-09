# 갈래 — Vercel 배포 가이드

본줄기는 이어가고, 곁가지는 옆으로 펼치는 프로토타입입니다.

## 구성
- `index.html` — 화면 전체 (정적)
- `api/ask.js` — Claude에게 답을 받아오는 서버리스 함수 (API 키를 숨겨줌)
- `package.json` — ESM 설정

브라우저에서 Anthropic API를 직접 부르면 키가 노출되고 막히기 때문에, 답변은 항상 `api/ask.js`를 거칩니다.

## 배포하기

### 1) Anthropic API 키 발급
https://console.anthropic.com 에서 API 키를 만듭니다. (사용량만큼 과금됩니다.)

### 2) Vercel에 올리기
가장 쉬운 두 가지 방법 중 하나를 고르세요.

**A. GitHub로 (권장)**
1. 이 폴더를 GitHub 저장소에 올린다.
2. vercel.com → Add New → Project → 저장소 Import.
3. 빌드 설정은 건드릴 필요 없음 (정적 + 서버리스 자동 인식).

**B. CLI로**
```
npm i -g vercel
cd galae
vercel
```

### 3) 환경 변수 설정 (필수)
Vercel 프로젝트 → Settings → Environment Variables 에서 추가:

| Name | Value |
|------|-------|
| `ANTHROPIC_API_KEY` | 발급받은 키 |

저장 후 한 번 재배포(Redeploy)하면 적용됩니다. CLI라면 `vercel env add ANTHROPIC_API_KEY` 후 `vercel --prod`.

## 참고
- 모델은 `api/ask.js`의 `model: "claude-sonnet-4-6"`에서 바꿀 수 있습니다.
- 키는 서버에만 있고 브라우저로 노출되지 않습니다.

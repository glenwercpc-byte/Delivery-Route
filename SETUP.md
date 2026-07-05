# Blossom Route — 설치 및 배포 안내

## 1. 폴더 구성
```
blossom-route/
├── index.html          ← 앱 전체 (여기에 API 키를 넣습니다)
├── manifest.json        ← PWA 설정
├── service-worker.js    ← 오프라인 캐싱
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── apple-touch-icon.png
└── SETUP.md
```

## 2. API 키 넣기
`index.html` 파일을 열어서 아래 줄을 찾으세요 (파일 상단 `<script>` 부분):

```js
window.GOOGLE_MAPS_API_KEY = "YOUR_GOOGLE_MAPS_API_KEY";
```

`"YOUR_GOOGLE_MAPS_API_KEY"` 부분을 새로 발급받은(rotate 완료된) 키로 교체하세요.

**키에 필요한 API (사용 설정 + API restriction에 체크):**
- Maps JavaScript API
- Directions API
- Geocoding API
- Places API (New)

**Application restriction**은 이 앱을 올릴 도메인으로 제한하세요. 예:
```
https://glenwercpc-byte.github.io/*
```

## 3. GitHub Pages에 배포 (기존에 하시던 방식과 동일)
1. GitHub 저장소를 만들고 `blossom-route` 폴더 안의 4개 파일 + `icons` 폴더를 그대로 업로드
2. 저장소 Settings → Pages → Branch를 `main`(또는 `gh-pages`) / `root`로 설정
3. 배포된 주소 예: `https://내계정.github.io/blossom-route/`

## 4. 휴대폰에 "앱처럼" 설치하기 (PWA)
**iPhone (Safari에서):**
1. 배포된 주소로 접속
2. 공유 버튼(⬆️) 탭 → "홈 화면에 추가" 선택
3. 홈 화면에 아이콘이 생기고, 탭하면 브라우저 주소창 없이 전체 화면 앱처럼 실행됩니다

**Android (Chrome에서):**
1. 배포된 주소로 접속
2. 우측 상단 점 3개 메뉴 → "홈 화면에 추가" 또는 화면 하단에 뜨는 "설치" 배너 탭
3. 마찬가지로 홈 화면 아이콘 생성 → 앱처럼 실행

## 5. 사용 흐름
1. **Setup 화면**: 출발지(꽃집) 주소 입력 → 배송지 주소들을 하나씩 추가 → "Round trip"(출발지로 복귀) 또는 "One-way"(마지막 배송지에서 종료) 선택 → "Optimize route"
2. **Overview 화면**: 최적화된 방문 순서, 지도, 예상 총 소요 시간(이동 시간 + 각 정류장 평균 3분) 확인 → "Start deliveries"
3. **Active 화면**: 현재 목적지 확인 → "Navigate to this stop"을 누르면 휴대폰에 설치된 Google Maps 앱으로 바로 길안내가 넘어갑니다 → 도착하면 "I've arrived" → "Arrived at [주소]" 메시지가 뜨고 "Move to next stop?" 확인 → 다음 정류장으로 이동
4. **Complete 화면**: 전체 배송 완료 후 실제 소요 시간 vs 예상 소요 시간, 정류장별 도착 시각 로그 확인

## 6. 참고 / 향후 확장 아이디어
- 지금은 **직접 입력 방식**으로 만들었습니다. 나중에 스프레드시트에서 주소 목록을 붙여넣거나 CSV로 업로드하는 기능을 추가하고 싶으시면 말씀해주세요.
- 현재 "경로 최적화"는 왕복 기준으로 방문 순서를 계산한 뒤, One-way를 선택하면 마지막 복귀 구간만 제외하는 방식입니다. 정류장이 매우 많아지고(10곳 이상) 편도 경로의 정확한 최적화가 중요해지면, 별도의 최적화 로직(예: 여러 종료 지점 후보 비교)을 추가할 수 있습니다.
- Jay님의 다른 시스템들처럼 Google Sheets를 연동해서 배송 목록을 자동으로 불러오고 싶다면, Apps Script API를 추가로 붙이는 것도 가능합니다.

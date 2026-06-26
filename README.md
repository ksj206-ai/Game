# 🦊 눈썹 점프 (Eyebrow Jump)

> 웹캠으로 **눈썹을 올리면 점프**하는 얼굴 인식 사막 러너 게임

키보드도, 마우스도 아닌 **표정**으로 플레이합니다. 카메라를 보고 눈썹을 위로 치켜올리면 여우가 점프해서 선인장·바위·텀블위드를 피해 달려요. MediaPipe FaceMesh로 얼굴 랜드마크를 실시간 추적해 눈썹 움직임을 감지합니다.

🎮 **플레이하기:** https://game-ashy-kappa-88.vercel.app/

---

## 📸 한눈에 보기

- 🦊 **3D 여우**가 사막을 달리는 끝없는 러너 게임 (Three.js)
- 🤨 **눈썹을 올려서 점프** — 웹캠 + 얼굴 인식
- 🌵🪨🌾 **랜덤 장애물** — 선인장 2종 / 바위 2종 / (100점 이후) 굴러오는 텀블위드
- 🏜️ **3D 사막 배경** — 모래 언덕, 피라미드, 사막 마을, 달과 별, 구름
- 🎬 **타격감 연출** — 화면 흔들림, 폭발·먼지 파티클, 캐릭터 찌그러짐, 빨간 플래시
- 📷 카메라가 없어도 **키보드(Space)로 플레이 가능**

---

## 🎮 조작법

| 입력 | 동작 |
|------|------|
| 🤨 **눈썹 올리기** | 점프 |
| **Space** | 점프 (키보드 모드) |
| **Enter** | (타이틀/보정 화면에서) 카메라 없이 키보드 모드로 시작 |
| **R** | 다시 시작 |
| **P** / **Esc** | 일시정지 / 해제 |
| **C** | 눈썹 재보정 |

### 플레이 순서
1. **▶ 시작하기** 버튼 클릭 (또는 Space/Enter)
2. 카메라 권한 **허용**
3. **2단계 보정**: ① 평상시 표정 유지 → ② 눈썹을 올린 채 유지
4. 보정이 끝나면 게임 시작! 눈썹을 올려 장애물을 피하세요

---

## ✨ 주요 기능

### 얼굴 인식 & 보정
- MediaPipe FaceMesh로 **눈썹–눈 사이 거리 / 얼굴 높이** 비율을 계산해 눈썹 올림을 감지
- 사람마다 표정이 다르므로 **평상시/눈썹 올림 2단계 보정**으로 개인별 임계값을 자동 설정
- 값을 부드럽게(smoothing) 처리해 떨림 없이 안정적으로 인식

### 게임플레이
- 속도에 비례한 **거리 기반 랜덤 장애물 생성** → 어떤 속도에서도 점프로 넘을 수 있는 간격 보장
- 점수가 오를수록 **점진적 난이도 상승**
- **100점 돌파 시** 텀블위드가 굴러오는 추가 위험 등장

### 연출 (Juice)
- 충돌 시 **카메라 흔들림 + 빨간 플래시 + 폭발 파티클**
- 달릴 때 **먼지**, 착지 시 **먼지 튐**, 점프/착지 **찌그러짐(squash & stretch)**
- 깊이별 **패럴랙스 스크롤** 배경

---

## 🛠 기술 스택

- **[Three.js](https://threejs.org/)** (r160) — 3D 렌더링, GLTFLoader로 GLB 모델 로드
- **[MediaPipe FaceMesh](https://github.com/google/mediapipe)** — 실시간 얼굴 랜드마크 추적
- **Web Audio API** — 외부 파일 없이 즉석 생성하는 효과음
- **순수 HTML/JS** — 빌드 도구 없는 정적 단일 페이지

---

## 📁 프로젝트 구조

```
.
├── index.html        # 게임 본체 (배포되는 파일)
├── model/            # 3D 모델 에셋 (.glb)
│   ├── Cactus.glb
│   ├── Barrel cactus.glb
│   ├── Rock.glb / Rock Large.glb
│   ├── Tumbleweed.glb
│   ├── Pyramid.glb
│   └── Little Desert Town.glb
└── README.md
```

> 여우 캐릭터는 Three.js 공식 **Khronos Fox** 모델(Run 애니메이션 포함)을 CDN에서 로드합니다.

---

## ▶ 로컬에서 실행하기

⚠️ **중요: 파일을 더블클릭(`file://`)으로 열면 3D 모델(.glb)이 로드되지 않습니다.**
브라우저 보안 정책상 `file://`에서는 로컬 파일을 fetch할 수 없어요. 반드시 **로컬 서버**로 띄워야 합니다.

```bash
# Node가 있다면
npx serve

# 또는 Python
python -m http.server 8000
```

그 후 브라우저에서 `http://localhost:8000/` 으로 접속하세요. (웹캠은 localhost/https에서만 동작합니다)

---

## 🚀 배포 (Vercel)

빌드가 필요 없는 정적 사이트라 그대로 올리면 됩니다.

1. 이 저장소를 [Vercel](https://vercel.com/new)에서 **Import**
2. 설정 변경 없이 **Deploy** (Framework Preset: Other)
3. 끝! `https://...vercel.app` 주소로 배포되며, **HTTPS라 웹캠도 정상 동작**합니다

이후 코드를 수정하고 `git push`하면 **자동으로 재배포**됩니다.

---

## 🧩 작동 원리 (요약)

```
웹캠 영상 ─▶ MediaPipe FaceMesh ─▶ 눈썹–눈 거리 / 얼굴 높이 비율
                                          │
                              보정으로 정한 임계값과 비교
                                          │
                          임계값 초과(눈썹 올림) ─▶ 점프!
```

게임 루프는 `requestAnimationFrame`으로 매 프레임 물리·장애물·파티클을 갱신하고 Three.js로 렌더링합니다. 얼굴 인식이 실패하거나 카메라가 없어도 게임 화면은 항상 뜨고, 키보드(Space)로 플레이할 수 있게 설계했습니다.

---

## 🗺 향후 계획

- 😊 **미소 버전** — 입꼬리를 인식해 "활짝 웃으면 날아오르는" 응용 게임
- 🏆 최고 점수 저장(NEW RECORD!) · 콤보 · 3·2·1 카운트다운
- 🔊 배경음악 루프

---

## 🙏 크레딧

- 여우 모델: [Khronos glTF Sample Assets — Fox](https://github.com/KhronosGroup/glTF-Sample-Assets) (CC0)
- 얼굴 인식: [Google MediaPipe](https://github.com/google/mediapipe)
- 3D 엔진: [Three.js](https://threejs.org/)
- 사막 모델(선인장·바위·텀블위드·피라미드·마을): `model/` 폴더의 GLB 에셋

---

🤖 이 프로젝트는 [Claude Code](https://claude.com/claude-code)와 함께 만들었습니다.

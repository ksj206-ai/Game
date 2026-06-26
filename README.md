# 🦖 눈썹 점프 (Eyebrow Jump)

웹캠으로 **눈썹을 올리면 점프**하는 공룡 달리기 게임. MediaPipe FaceMesh로 눈썹 움직임을 감지합니다.

## 플레이
- 카메라를 허용하고 안내에 따라 보정(평상시 표정 → 눈썹 올린 표정)
- 눈썹을 올려 선인장을 점프로 피하기
- 카메라가 없으면 **Enter**로 키보드 모드 시작, **Space**로 점프
- `R` 다시 시작 · `P` 일시정지 · `C` 재보정

## 배포
정적 HTML 한 파일(`index.html`)입니다. Vercel에 그대로 배포하면 됩니다.
> 웹캠은 HTTPS에서만 동작하므로 Vercel(https) 배포 시 정상 작동합니다.

## 기술
- HTML5 Canvas, Web Audio API
- [MediaPipe FaceMesh](https://github.com/google/mediapipe)

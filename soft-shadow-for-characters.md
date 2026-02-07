# Soft/Low-Resolution Shadows for Characters / 캐릭터용 부드러운 저해상도 그림자

Make background shadows on characters intentionally blurry to avoid a "dirty" look.  
캐릭터에 받는 배경 그림자를 의도적으로 흐릿하게 만들어 지저분한 느낌 방지.

---

## Method 1: Light Source Angle (Directional Light) / 라이트 소스 앵글

**Easiest method / 가장 쉬운 방법**

```
Directional Light → Details → Light → Light Source Angle
```

| Value | Result |
|-------|--------|
| 0.5 (default) | Sharp shadows / 선명한 그림자 |
| 2~5 | Soft penumbra / 부드러운 반그림자 |

Physically simulates a larger sun → bigger penumbra.  
물리적으로 태양 크기를 크게 → 반그림자 영역 증가.

---

## Method 2: Shadow Filter Sharpen / 섀도우 필터 선명도

```
Light → Details → Shadows → Shadow Filter Sharpen
```

| Value | Result |
|-------|--------|
| 1.0 (default) | Normal sharpness / 기본 선명도 |
| 0.2~0.5 | Blurry shadows / 흐릿한 그림자 |
| 0 or negative | Maximum blur / 최대 블러 |

---

## Method 3: Shadow Resolution Scale / 그림자 해상도 스케일

Per-light shadow resolution control.  
라이트별 그림자 해상도 제어.

```
Light → Details → Shadows → Shadow Resolution Scale
```

| Value | Approx. Texel Size (40m range) |
|-------|--------------------------------|
| 1.0 | ~2cm/texel |
| 0.5 | ~4cm/texel |
| 0.1 | ~20cm/texel |

### With Lighting Channels / 라이팅 채널과 조합

1. Create separate light for characters / 캐릭터용 별도 라이트 생성
2. Set `Lighting Channel 1` on both light and character / 라이트와 캐릭터 모두 채널 1 설정
3. Lower `Shadow Resolution Scale` on this light / 해당 라이트의 해상도 낮춤

---

## Method 4: Source Radius (Point/Spot Light) / 소스 반경

For non-directional lights / 방향성 라이트가 아닌 경우:

```
Point/Spot Light → Details → Light → Source Radius
```

Larger value = softer shadow edges.  
값이 클수록 그림자 경계가 부드러워짐.

---

## Method 5: PCSS (Project Setting) / PCSS 프로젝트 설정

Distance-based soft shadows.  
거리 기반 소프트 섀도우.

```
Project Settings → Rendering → Shadows → Shadow Filter Method → PCSS
```

- Shadows blur naturally with distance / 거리에 따라 자연스럽게 블러
- Higher performance cost / 성능 비용 있음

---

## Recommended Combination / 권장 조합

For stylized character shadows / 스타일라이즈드 캐릭터 그림자:

```
Light Source Angle: 3.0
+ Shadow Filter Sharpen: 0.3
= Soft, clean character shadows / 부드럽고 깔끔한 캐릭터 그림자
```

For maximum control / 최대 제어:
```
Lighting Channel separation + Shadow Resolution Scale 0.1~0.2
```

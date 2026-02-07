# Selective Shadow Receiving in UE5 / UE5에서 선택적 그림자 받기

How to make objects receive shadows from specific lights only.  
특정 라이트의 그림자만 선택적으로 받는 방법.

---

## Lighting Channels / 라이팅 채널

The primary method for selective shadow receiving.  
선택적 그림자 수신의 핵심 기능.

### How it works / 작동 방식

- Both **Light** and **Mesh** components have `Lighting Channels` settings
- Only lights and meshes sharing the same channel affect each other
- 3 channels available: **0, 1, 2** (multiple selection possible)

- **Light**와 **Mesh** 컴포넌트 모두 `Lighting Channels` 설정 보유
- 같은 채널을 공유하는 라이트와 메시만 서로 영향
- 채널 3개 사용 가능: **0, 1, 2** (복수 선택 가능)

### Setup / 설정 방법

**1. Object to receive shadow / 그림자를 받을 오브젝트**
```
Mesh → Details → Lighting → Lighting Channels → Check desired channel
Mesh → Details → Lighting → Lighting Channels → 원하는 채널 체크
```

**2. Light source / 라이트 소스**
```
Light → Details → Light → Lighting Channels → Check same channel
Light → Details → Light → Lighting Channels → 동일한 채널 체크
```

### Example / 예시

| Object | Channel 0 | Channel 1 | Result |
|--------|-----------|-----------|--------|
| Character / 캐릭터 | ✓ | ✓ | Receives shadows from both channels |
| Background / 배경 | ✓ | - | Only receives Channel 0 shadows |
| Main Light / 메인 라이트 | ✓ | - | Affects all objects |
| Character Light / 캐릭터 라이트 | - | ✓ | Only affects character |

---

## Other Shadow Settings / 기타 그림자 설정

### Per-Mesh Options / 메시별 옵션

| Setting | Description |
|---------|-------------|
| `Cast Shadow` | Whether this object casts shadow / 그림자 드리움 여부 |
| `Cast Dynamic Shadow` | Dynamic shadow casting / 동적 그림자 생성 |
| `Cast Static Shadow` | Static shadow casting / 정적 그림자 생성 |
| `Self Shadow Only` | Only receive own shadow / 자기 그림자만 받음 |

---

## Important Notes / 주의사항

- Default: All objects and lights are on **Channel 0**
- Only works fully with **Stationary/Movable Lights** (Static lights bake shadows)
- Ray Tracing: Additional `Affect Ray Tracing Shadows` option available

- 기본값: 모든 오브젝트와 라이트가 **Channel 0**에 체크됨
- **Stationary/Movable Light**에서만 완전히 작동 (Static Light는 그림자 베이킹됨)
- 레이트레이싱: `Affect Ray Tracing Shadows` 추가 옵션 사용 가능

---

## Recommended Channel Usage / 권장 채널 구성

| Channel | Usage |
|---------|-------|
| 0 | Default environment lighting / 기본 환경광 |
| 1 | Character-specific lighting / 캐릭터 전용 조명 |
| 2 | Special effects / Cutscenes / 특수 효과, 컷씬용 |

# Rigid Body Physics in Animation Blueprint / ABP에서 Rigid Body 물리 시뮬레이션

Physics Asset-based bone simulation in Animation Blueprints.  
Animation Blueprint에서 Physics Asset 기반 본 물리 시뮬레이션.

---

## Rigid Body Node / 리지드 바디 노드

The primary node for physics simulation in AnimGraph.  
AnimGraph에서 물리 시뮬레이션의 핵심 노드.

```
AnimGraph → Add Node → Rigid Body
```

Also known as **RBAN** (Rigid Body Anim Node).

---

## Key Properties / 주요 속성

| Property | Description |
|----------|-------------|
| `Override Physics Asset` | Specify PA to use / 사용할 PA 지정 |
| `Simulation Space` | World / Component / Bone |
| `Alpha` | Blend strength (0~1) / 블렌딩 강도 |

---

## Physics Asset Resolution / Physics Asset 결정 규칙

| Situation | Result |
|-----------|--------|
| Override PA specified | Uses Override PA / 오버라이드 PA 사용 |
| No Override, Mesh has PA | Uses Mesh's default PA / 메시 기본 PA 사용 |
| No Override, Mesh has no PA | Simulation disabled / 시뮬레이션 안 됨 |

### Default PA Location / 기본 PA 위치

```
Skeletal Mesh Asset → Asset Details → Physics → Physics Asset
```

---

## When to Use Override / Override 사용 시점

- Different physics settings for same mesh / 같은 메시에 다른 물리 세팅
- State-based PA switching / 상태별 PA 전환
  - Normal PA vs Ragdoll PA vs Partial simulation PA

---

## AnimGraph Example / AnimGraph 예시

```
[Animation Pose] → [Rigid Body] → [Output Pose]
                        ↑
              Simulates bones defined in Physics Asset
              Physics Asset에서 정의된 본들 시뮬레이션
```

---

## Related Nodes / 관련 노드

| Node | Use Case |
|------|----------|
| `Anim Dynamics` | Simple spring/chain (no PA needed) / 단순 스프링 (PA 불필요) |
| `Physical Animation Component` | Component-level full physics / 컴포넌트 레벨 전체 물리 |
| `Pose Driver` | Drive bones by orientation / 본 방향 기반 드라이브 |

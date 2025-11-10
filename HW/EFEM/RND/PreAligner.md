# PreAligner

## XYR vs XZR 타입 얼라이너

### 얼라인 이동량 확인 차이점

**XYR 얼라이너**
- 얼라인 후 APS(모터 위치 확인) 명령으로 얼라인 시 이동량 확인 가능

**XZR 얼라이너**
- APS 명령으로 이동량 확인 불가
- Y축 방향 모터가 없어 Y축 이동량 확인 불가능
- 편심량은 변수 73번(V73)에 저장되어 확인 가능
  - 이 값은 XYR 기준 XY 대각선 길이에 해당: `sqrt(x^2 + y^2)`

### 편심량 확인 방법 (XZR)

```
SEND>ALS  1
RECV>ALS
SEND>VAR  V73
RECV>VAR  V73=1234
```

**단위 환산**
- 변수 73번 리턴 값: pulse 단위
- 3200 pulse = 5mm

---

## 얼라이너 타입 확인 방법

### 방법 1: 버전 정보 확인 (VER 명령)

**XYR 타입**
- 버전 첫 자리: 1.xx.xxx
```
SEND>VER
RECV>VER  RVA300 1.02.074, Firmware:001
```

**XZR 타입**
- 버전 첫 자리: 2.xx.xxx
```
SEND>VER
RECV>VER  RVA300 2.02.100, Firmware:001
```

### 방법 2: 변수 74번 확인 (VAR V74)

**XYR 타입**
```
SEND>VAR  V74
RECV>VAR  V74=1
```

**XZR 타입**
```
SEND>VAR  V74
RECV>VAR  V74=2
```

### 방법 3: ALT 명령 사용

변수 74번 대신 ALT 명령 사용 가능

**XYR 타입**
```
SEND>ALT
RECV>ALT  1
```

**XZR 타입**
```
SEND>ALT
RECV>ALT  2
```

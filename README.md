# MinIO Cert Practice Lab

MinIO Certified Administrator / AIStor Administrator 시험 대비용 단일 HTML 퀴즈 앱입니다. `MinIO_Quiz_v3.html` 파일 하나로 실행되며, 별도의 백엔드나 빌드 과정 없이 브라우저에서 바로 사용할 수 있습니다.

## 구성 파일

| 파일 | 설명 |
| --- | --- |
| `MinIO_Quiz_v3.html` | MinIO 자격증 대비 퀴즈, 모의시험, `mc` 명령어 연습이 포함된 단일 페이지 앱 |
| `README.md` | 사용 방법과 기능 요약 |

## 실행 방법

브라우저에서 HTML 파일을 직접 열면 됩니다.

```bash
cd /home/wny/minio-cert-practice-lab
```

GUI 환경이라면 파일 탐색기나 브라우저에서 `MinIO_Quiz_v3.html`을 열면 됩니다.

원격 서버에서 접속하거나 브라우저가 파일 직접 열기를 제한하는 경우 간단한 정적 서버로 실행할 수 있습니다.

```bash
python3 -m http.server 8080
```

그 다음 브라우저에서 접속합니다.

```text
http://<server-ip>:8080/MinIO_Quiz_v3.html
```

SSH 터널을 사용할 경우:

```bash
ssh -L 8080:127.0.0.1:8080 wny@k8s-master01
```

내 PC 브라우저에서:

```text
http://127.0.0.1:8080/MinIO_Quiz_v3.html
```

## 주요 기능

- 총 570문항의 MinIO 관련 4지선다 퀴즈
- 한국어/영어 병기 전환 버튼
- 전체 문제, 랜덤 셔플, 파트별 풀이
- 오답 복습 및 오답 횟수 저장
- 60문항 / 90분 모의시험
- 시험 제출 후 정답, 오답, 미응답 리뷰
- 파트별 정답률 분석
- `mc` 명령어 직접 입력 연습
- `mc --help`, `mc alias set --help` 같은 도움말 시뮬레이션
- 브라우저 `localStorage` 기반 학습 기록 저장

## 퀴즈 범위

| 파트 | 문항 수 |
| --- | ---: |
| Configure & Deploy | 45 |
| Encryption | 30 |
| Erasure Code | 50 |
| Events | 40 |
| Lifecycle Mgmt | 40 |
| Manage Deployments | 40 |
| MinIO Client (`mc`) | 50 |
| Monitoring | 40 |
| Recovery | 20 |
| Replication | 50 |
| Retention | 40 |
| Security | 50 |
| Versioning | 40 |
| Performance | 15 |
| Advanced Configuration | 20 |
| **합계** | **570** |

## 학습 모드

### 전체 문제

570문항을 HTML에 정의된 순서대로 풉니다. 처음부터 전체 범위를 훑을 때 사용합니다.

### 랜덤 셔플

전체 문제를 무작위 순서로 풉니다. 반복 학습 시 문제 순서 암기를 줄이는 데 좋습니다.

### 오답 복습

이전에 틀린 문제만 다시 풉니다. 오답 목록과 오답 횟수는 브라우저 `localStorage`에 저장됩니다.

### 파트별

원하는 주제만 골라 집중 학습합니다. 예를 들어 Erasure Code, Replication, Security처럼 시험에서 헷갈리기 쉬운 파트를 따로 연습할 수 있습니다.

### 모의시험

실제 시험 형식에 맞춰 60문항을 랜덤으로 출제하고 90분 타이머를 제공합니다. 제출 후 합격/불합격 판정, 소요 시간, 남은 시간, 정답/오답 리뷰를 확인할 수 있습니다.

앱 내부 합격 기준은 80%입니다. MinIO 공식 합격 점수가 공개되어 있지 않으므로 커뮤니티 기준의 추정값으로 보아야 합니다.

## `mc` 명령어 연습

터미널처럼 명령어를 직접 입력하며 MinIO Client 사용법을 익히는 모드입니다. 실제 명령을 서버에 실행하지 않고, 브라우저 안에서 정답 여부만 채점합니다.

지원 범위:

| 카테고리 | 문제 수 |
| --- | ---: |
| alias | 4 |
| bucket | 5 |
| object | 7 |
| mirror | 3 |
| policy | 3 |
| admin | 7 |
| versioning | 3 |
| retention | 2 |
| ilm | 2 |
| replicate | 1 |
| encrypt | 2 |
| event | 1 |
| watch | 1 |
| support | 2 |
| **합계** | **43** |

예시 도움말:

```text
mc --help
mc alias --help
mc alias set --help
mc admin user --help
mc ilm --help
mc support perf --help
```

## 저장되는 데이터

이 앱은 서버에 학습 기록을 저장하지 않습니다. 아래 정보만 현재 브라우저의 `localStorage`에 저장합니다.

- 틀린 문제 ID
- 맞힌 문제 ID
- 문제별 오답 횟수

브라우저 캐시/사이트 데이터를 삭제하거나 다른 브라우저를 사용하면 오답 기록이 초기화됩니다.

## 주의 사항

- 이 앱은 학습 보조용입니다. 실제 시험 문제나 공식 덤프를 보장하지 않습니다.
- MinIO 명령어와 옵션은 버전에 따라 달라질 수 있으므로 실무 적용 전 공식 문서를 확인해야 합니다.
- `mc` 명령어 연습 모드는 시뮬레이터이며 실제 MinIO 서버에 명령을 실행하지 않습니다.
- 단일 HTML 파일 구조라 배포는 쉽지만, 문제 데이터 수정 시 HTML 내부 JavaScript 배열을 직접 수정해야 합니다.

## 추천 학습 순서

1. 전체 문제를 한 번 풀며 약한 파트를 확인합니다.
2. 파트별 모드로 취약 파트를 반복합니다.
3. 오답 복습으로 틀린 문제를 정리합니다.
4. `mc` 명령어 연습으로 실무형 명령어를 익힙니다.
5. 모의시험 모드로 60문항 / 90분 환경에 적응합니다.

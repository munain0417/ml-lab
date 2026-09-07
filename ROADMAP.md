# 입대 전 6개월 NLP 로드맵

> 기간: 2026.09 → 2027.02 · 목표: 연구 중심(대학원/랩실) · 가용 시간: 주 10–15시간
> 원본(체크리스트 진행도 저장됨): https://claude.ai/code/artifact/03fc2ce2-5038-4c59-8657-cf4a7bf2f70b

## 현재 상태 ← Phase 넘어갈 때마다 여기만 고칠 것

- Phase: 0 (환경 세팅)
- 진행: WSL2·Git·uv 설치 완료, 첫 커밋 완료, Colab GPU 확인
- 막힌 것: Cowork 폴더 연동(WSL UNC 경로) — GitHub 연동으로 우회
- 다음: 셸 명령어 30개, VS Code 디버거
- 갱신일: 2026-09-07

---

## 전제

병목은 지식이 아니라 손이다. 기계학습 이론(지도·비지도·강화학습, ANN, 경사하강법 등)은 이미 알고 있고
직접 구현한 경험이 없다. 이번 학기 21학점(선형대수, 객체지향, 알고리즘, 운영체제, 컴파일러, 강화학습기초,
인공지능특강)이 이론을 담당하므로, 개인 시간은 전부 구현에 쓴다.

**학습 방식**: 순수 탑다운도 바텀업도 아닌 나선형 — 작은 것은 밑바닥까지(numpy·PyTorch로 직접),
큰 것은 라이브러리로(Hugging Face). 같은 개념을 두 층위에서 반복해 만난다.

**6개월 안의 현실적 목표**: LLM 사전학습은 불가능. 가능한 것은 (1) 작은 언어모델 완전 이해 후 직접 구현,
(2) 공개 모델 파인튜닝·평가, (3) 논문 한 편 재현. (3)이 최종 산출물이다.

**우선순위**: 수업 > 랩실 > 이 로드맵 > 학회. 무너질 것 같으면 Phase 5와 학회부터 버린다.

## 제외한 것

| 항목 | 판정 | 이유 |
|---|---|---|
| HTML/CSS·JS·React·Next.js·TypeScript·Django | 제외 | 연구용 데모는 Gradio로 30분. 6개월 내 연구 기여 0. |
| 프론트/백엔드 로드맵 | 제외 | 연구실에 필요한 인프라는 셸·Git·Docker·GPU 접속이 전부. |
| ORCA·바이브코딩·GPT/Codex 활용서 | 제외 | Phase 1–2는 코드 생성을 막는 구간이라 정반대 방향. |
| Obsidian 활용 가이드 | 축소 | 논문 노트 폴더 하나면 충분. |
| 알고리즘 캠프 60% | 수업 대체 | 알고리즘 수강 중. 감각 유지용 주 2–3문제만. |
| 강화학습 심화 | 수업 대체 | 강화학습기초 수강 중. RLHF는 Phase 3에서 개념만. |
| 도커·Git·WSL | 위치 이동 | Git·WSL은 Phase 0에서 세팅으로, 도커는 쓸 데가 생기는 Phase 3으로. |

## 일정

| 구간 | 시기 | 분량 |
|---|---|---|
| Phase 0 환경 | 9월 2주 | 1주 · 12h |
| Phase 1 손으로 딥러닝 | 9월 3주 – 10월 2주 | 4주 · 48h |
| Phase 2 GPT 직접 구현 | 10월 3주 – 11월 4주 | 6주 · 65h |
| (기말) | 12월 1–3주 | 로드맵 정지 |
| Phase 3 파인튜닝·평가 | 12월 말 – 1월 | 5주 · 90h |
| Phase 5 서빙 (선택) | 2월 | 20h |
| Phase 4 논문·랩실 | 9월 – 입대 전 | 상시 병행, 주 2–3h |

---

## Phase 0 — 돌아가는 책상 만들기

1주 · 12h · 한 번만 하면 끝. 공부가 아니라 설치다.

- [ ] 리눅스 환경 확보 (윈도우면 WSL2 + Ubuntu)
- [ ] 셸 기본 명령어 30개 (`cd ls cp mv grep find ssh scp tmux nvidia-smi`)
- [ ] Python 환경을 `uv`로 통일 (conda/pip/venv 혼용 금지)
- [ ] Git: add / commit / push / branch / PR 다섯 개만
- [ ] GitHub `ml-lab` 레포 생성 — 이후 모든 코드가 여기 쌓인다
- [ ] VS Code 디버거로 중단점 찍고 변수 보기 (print 디버깅 탈출)
- [ ] Colab / Kaggle 무료 GPU 확인 (`torch.cuda.is_available()`)

**통과 기준**: 빈 폴더에서 가상환경 → PyTorch 설치 → GPU 확인 → 커밋 → 푸시까지 10분 안에 막힘없이.

**자료**: [MIT Missing Semester](https://missing.csail.mit.edu/) · [uv 문서](https://docs.astral.sh/uv/) · [Pro Git 한국어](https://git-scm.com/book/ko/v2) 1–3장

## Phase 1 — 알고 있는 걸 손으로 다시 만들기

4주 · 48h · 바텀업 구간. **가장 중요하고 가장 건너뛰고 싶어지는 구간.**

- [ ] Karpathy micrograd 영상 따라 치며 자동미분 엔진 구현
- [ ] numpy만으로 2층 MLP → MNIST 정확도 95%+
- [ ] 역전파를 종이에 손으로 유도한 뒤 자기 코드와 대조
- [ ] 같은 MLP를 PyTorch로 재구현 (autograd/optimizer/DataLoader 대응시키기)
- [ ] 텐서 shape 감각 (broadcasting, `view`/`reshape`/`permute`, 배치 차원)
- [ ] 학습 루프를 아무것도 안 보고 쓰기 (zero_grad → forward → loss → backward → step)
- [ ] 일부러 망가뜨리기: 학습률 100배, 정규화 제거, 활성함수 제거

**통과 기준**: "역전파가 뭔가요"에 수식을 쓰고 코드 어느 줄인지 짚으며 10분 설명.

**자료**: [micrograd 영상](https://www.youtube.com/watch?v=VMj-3S1tku0) · [PyTorch Learn the Basics](https://docs.pytorch.org/tutorials/beginner/basics/intro.html) · 밑바닥부터 시작하는 딥러닝 1권 3–5장

## Phase 2 — GPT를 직접 짠다

6주 · 65h · 핵심 구간. 여기가 "쓰는 사람"과 "다루는 사람"을 가른다.

- [ ] Karpathy "Let's build GPT" 따라 치며 완주
- [ ] **영상 닫고 빈 파일에서 다시 짜기** ← Phase 2 가치의 절반
- [ ] BPE 토크나이저 직접 구현 (minbpe). 한국어 토크나이징 문제를 직접 확인
- [ ] 부품별 설명 가능하게: QKV, multi-head, positional encoding, layer norm, residual
- [ ] 그 다음에 Attention Is All You Need 읽기 (코드 먼저, 논문 나중)
- [ ] 한국어 텍스트로 학습 돌리고 loss curve 읽기
- [ ] Stanford CS336 Assignment 1 도전 ← 이 구간의 최종 보스
- [ ] nanoGPT 코드 읽고 자기 구현과 비교

**통과 기준**: 자료 없이 30분 안에 동작하는 미니 GPT. "왜 attention이 RNN을 이겼나"를 계산 구조로 설명.

**자료**: [Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) · [minbpe](https://github.com/karpathy/minbpe) · [nanoGPT](https://github.com/karpathy/nanoGPT) · [CS336](https://github.com/stanford-cs336) · [Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)

## Phase 3 — 현대 LLM 생태계 (탑다운 구간)

5주 · 90h · 방학. Phase 2를 통과했으면 이제 라이브러리가 블랙박스가 아니라 단축키다.

- [ ] HF 3종: `transformers`, `datasets`, `tokenizers`
- [ ] LoRA/QLoRA로 1–3B 모델 파인튜닝 (Colab, `peft`)
- [ ] **평가 파이프라인 만들기** ← 연구에서 제일 중요한데 다들 건너뛴다
- [ ] Weights & Biases로 실험 추적 + 하이퍼파라미터 스윕
- [ ] Docker로 실험 환경 재현 가능하게
- [ ] RAG 파이프라인 하나 구성 (임베딩, 벡터 검색, 컨텍스트 구성)
- [ ] RLHF/DPO는 개념과 코드 구조만
- [ ] Smol Training Playbook 통독

**통과 기준**: "이 모델이 저 모델보다 낫다"를 실험 설계·지표·베이스라인·재현 방법까지 갖춰 방어.

**자료**: [HF LLM Course](https://huggingface.co/learn/llm-course) · [smol-course](https://huggingface.co/learn/smol-course) · [Smol Training Playbook](https://huggingface.co/spaces/HuggingFaceTB/smol-training-playbook) · [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)

## Phase 4 — 연구 파이프라인 (9월부터 상시 병행)

주 2–3h. "연구 파이프라인이 어떻게 돌아가는가"에 대한 답은 코드가 아니라 여기서 나온다.

- [ ] 3-pass 논문 읽기법 익히기
- [ ] 지원 랩 교수의 논문 전부 읽기 (부임 초기라 편수가 적은 건 오히려 기회)
- [ ] 주 1편 논문 + 5줄 요약 (문제 / 한계 / 제안 / 실험 / 내 의문)
- [ ] 바이오+NLP 접점: PubMedBERT·BioBERT, BLURB, PubMed·BioASQ
- [ ] **논문 한 편 재현하고 리포트로 남기기** ← 6개월의 최종 산출물
- [ ] 랩실 미팅에서 최소 한 번 질문하기

**통과 기준**: 처음 보는 NLP 논문을 한 시간 안에 "뭘 주장하고 실험이 뒷받침하는지" 판단.

**자료**: [How to Read a Paper](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf) · [ACL Anthology](https://aclanthology.org/) · [Papers with Code](https://paperswithcode.com/)

## Phase 5 — 엔지니어링 최소 세트 (선택)

2월 · 20h · 앞이 밀렸으면 미련 없이 버린다.

- [ ] FastAPI로 모델 호출 API 하나
- [ ] Gradio로 데모 UI
- [ ] Docker로 감싸서 다른 컴퓨터에서 실행 확인

---

## LLM 사용 규칙 (로드맵의 일부)

| 구간 | 규칙 |
|---|---|
| Phase 0 | 자유롭게. 환경 설정은 배움의 대상이 아니라 통과할 관문. |
| Phase 1–2 | **코드 생성 금지.** 허용: 개념 설명, 에러 해석, 내 코드 리뷰, "왜 틀렸나". 금지: "짜줘", 함수 통째로 받기. |
| Phase 3–5 | 다시 자유롭게. 생성된 코드의 틀린 부분을 짚을 수 있으니 가속기로 작동. |
| 논문 | 먼저 혼자 읽고, 다 읽은 뒤 이해 검증용으로만. |

## 막혔을 때 (15분 규칙)

1. 15분은 혼자 붙잡는다 ← 실력이 붙는 구간
2. 에러 메시지를 그대로 검색
3. 그래도 안 되면 질문 — 단 Phase 1–2에서는 "짜줘"가 아니라 "어디를 봐야 하나"로

## 주간 운영

- 평일 저녁 2h × 3 + 주말 1블록 4–6h
- 세션 시작: 5분간 지난 코드 읽기 (컨텍스트 복구)
- 세션 끝: 이 파일 상단 "현재 상태" 갱신
- 시험 기간: 로드맵 완전 정지. 방학에서 회수
- 랩실 과제와 겹치면 **로드맵을 버리고 랩 과제를 한다**

## 이 로드맵이 실패하는 방식

1. **Phase 1–2가 지루해서 Phase 3으로 뛰는 것.** HF는 즉각적 성취감을 주고 numpy 역전파는 안 준다.
   3개월 뒤에 남는 건 정확히 반대다. **Phase 2를 통과 못 했으면 넘어가지 마라** — 이 문서의 유일한 강제 규칙.
2. **21학점 + 랩실 + 학회 + 로드맵을 전부 100%로 하려다 12월에 무너지는 것.**
   남길 것은 완주 기록이 아니라 재현 리포트 한 편과 직접 짠 GPT 하나다.

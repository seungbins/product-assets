# AI 콘텐츠 생성 도구 특화 보안 리스크

이 저장소의 제품군(scene_renderer, puppet_animator, bg_batch_kit, lora_recipe, shorts_converter)은 모두 "모델 가중치를 로드/배포하고, 사용자 프롬프트·미디어를 입력받고, GPU 추론을 실행하고, 파일을 배치 처리한다"는 공통 구조를 가집니다. [`annotated-bibliography.md`](./annotated-bibliography.md)의 28편은 버그바운티 프로그램 자체에 대한 연구였다면, 이 문서는 **이 제품군의 실제 공격 표면에 무엇이 걸릴 수 있는지**를 CVE·실제 사고 사례·주요 AI 기업의 실제 프로그램 구조로 조사한 결과입니다. [`templates/scope-template.md`](./templates/scope-template.md)의 취약점 카테고리를 채우는 데 직접 사용하세요.

> 조사 방법: WebSearch/WebFetch로 학술 논문뿐 아니라 CVE, 벤더 공지, 실제 플랫폼(Civitai·HackerOne·Google 등)의 공개 정책을 직접 확인. 근거를 찾지 못한 부분은 "미확인"으로 명시.

---

## 1. 모델 파일 & 공급망 보안

### 1.1 Pickle 역직렬화 RCE (모델 체크포인트 파일)
**핵심:** `.pt`/`.pth`/`.ckpt` 같은 PyTorch 체크포인트는 기본적으로 Python `pickle`로 직렬화되며, `torch.load()`는 파일 안에 심어진 임의 코드를 그대로 실행합니다. 5개 제품 모두(베이스 모델·LoRA 어댑터·모션 모델 로드) 해당될 수 있는 가장 확실한 RCE 클래스.
**근거:** 2025년 2월 Hugging Face에 업로드된 악성 모델 2건이 7z 압축 + 손상된 opcode 스트림으로 `torch.load()` 에러와 Picklescan 탐지를 모두 우회하며 리버스쉘을 열었던 실제 사례("nullifAI"). [CSO Online](https://www.csoonline.com/article/3819920/attackers-hide-malicious-code-in-hugging-face-ai-model-pickle-files.html) / Rapid7 [분석](https://www.rapid7.com/blog/post/from-pth-to-p0wned-abuse-of-pickle-files-in-ai-model-supply-chains/) / 탐지 연구 [PickleBall](https://arxiv.org/pdf/2508.15987), [SafePickle](https://arxiv.org/html/2602.19818v1)
**스코프 문구 제안:** "조작된 모델/체크포인트 파일(.pt, .pth, .ckpt, 그 외 pickle 기반 포맷) 로드 시 발생하는 임의 코드 실행 — 인스코프."

### 1.2 악성 가중치 공급망 & 스캐너 우회
**핵심:** `lora_recipe`(서드파티/사용자 업로드 가중치 배포)와 "직접 모델을 가져올 수 있는" 제품에 직결. 스캐너가 있어도 스캐너 자체를 우회하는 기법이 활발히 연구되는 별도 취약점군.
**근거:** Sonatype이 Hugging Face 자체 스캐너(Picklescan)를 우회하는 취약점 4건 발견 [Sonatype](https://www.sonatype.com/blog/bypassing-picklescan-sonatype-discovers-four-vulnerabilities), JFrog도 독립적으로 제로데이 3건 발견 [JFrog](https://jfrog.com/blog/unveiling-3-zero-day-vulnerabilities-in-picklescan/). OWASP가 **LLM03:2025 Supply Chain**으로 공식 분류하며 LoRA/PEFT 어댑터를 명시적으로 언급. [OWASP GenAI Security Project](https://genai.owasp.org/llmrisk/llm03-training-data-poisoning/)
**스코프 문구 제안:** "모델 파일 악성코드/포맷 스캐닝을 우회하는 기법(스캐너를 속이는 인코딩, zip/7z 트릭 등) — 실제 페이로드가 없어도 공급망 이슈로 인스코프."

### 1.3 LoRA/어댑터 백도어 & 가중치 오염
**핵심:** 코드 실행이 아니라 가중치 자체에 은밀한 트리거 행동이 심어지는 방식 — `lora_recipe`의 핵심 위협 모델. **주의:** 실제 유포 사례가 아직 보고되진 않은, 연구로 입증된 리스크(2025-2026 프리프린트/NDSS 논문 수준)이므로 확정된 사실처럼 다루지 말 것.
**근거:** [arXiv 2602.21977](https://arxiv.org/pdf/2602.21977) (LoRA 백도어), NDSS 2026 채택 논문 [PDF](https://www.ndss-symposium.org/wp-content/uploads/2026-f168-paper.pdf), 탐지 어려움을 보인 [arXiv 2602.15195](https://arxiv.org/html/2602.15195)
**스코프 문구 제안:** "제공된 LoRA/어댑터/레시피가 문서화되지 않은 트리거 조건부 숨겨진 동작을 보인다는 증명 — 모델 무결성 이슈로 인스코프."

---

## 2. 프롬프트 인젝션 & 입력 조작

### 2.1 직접/간접 프롬프트 인젝션
**핵심:** 텍스트 프롬프트를 받는 모든 제품(scene_renderer, puppet_animator의 텍스트-투-모션, shorts_converter의 자동 편집/요약)에 해당. 간접 인젝션(자막·URL 등 외부 텍스트를 통해 유입)이 더 위험.
**근거:** OWASP Top 10 for LLM Applications **LLM01**(1위 리스크). [OWASP PDF](https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf)
**스코프 문구 제안:** "운영자가 설정한 제약(세이프티 필터, 출력 포맷, 에이전틱 동작이라면 미승인 도구/파일 접근)을 무시하게 만드는 프롬프트 인젝션 — 인스코프. 단순히 품질 낮은/주제 이탈 출력만 유발하는 경우는 보안·안전 영향이 없으면 아웃오브스코프."

### 2.2 이미지/비주얼 프롬프트 인젝션
**핵심:** 이 제품군은 "시각적" 도구라 더 중요 — 업로드된 참조 이미지·영상 프레임 자체가 신뢰되지 않은 입력 채널일 수 있음(예: bg_batch_kit이 처리 전 이미지를 비전 분류하는 경우, puppet_animator가 참조 이미지 내용을 해석하는 경우).
**근거:** 이미지에 인간 눈에는 안 보이거나 배경에 섞인 텍스트로 지시문을 심어 멀티모달 모델이 이를 그대로 수행하게 만든 연구(스텔스 조건에서 공격 성공률 최대 64%). [arXiv 2603.03637](https://arxiv.org/pdf/2603.03637)
**스코프 문구 제안:** "업로드된 이미지/영상/오디오 파일에 (시각적으로, 메타데이터로, 또는 스테가노그래피로) 심어진 지시문이 처리 시 파이프라인 동작을 바꾸는 경우 — 인스코프."

---

## 3. 생성 콘텐츠 오남용 ⚠️ 이 제품군에서 가장 중요한 리스크

### 3.1 비동의 이미지·딥페이크·아동 관련 콘텐츠 오남용
**핵심:** puppet_animator·shorts_converter(실제 인물의 얼굴·모션을 다룸)와 lora_recipe(특정 인물을 대상으로 한 파인튜닝이 실제로 딥페이크/NCII 제작에 쓰이는 바로 그 메커니즘)에 대해 **가장 심각하고 가장 제품 특화된 리스크**입니다. 추측이 아니라 이미 업계에서 실제로 벌어지고 있는 문제입니다.
**근거:**
- 이 제품군과 정확히 같은 카테고리(비디오 딥페이크)를 실증 분석한 논문 — 모델을 큐레이션 없이 오픈 공개하거나 플랫폼 모더레이션이 없는 등 "개발자/플랫폼의 선택"이 다운스트림 NCII/CSAM 오남용 패턴을 예측 가능하게 만든다는 것을 보이며, **LoRA 파인튜닝 수천 건이 이런 목적으로 CivitAI에 호스팅되고 있다고 구체적으로 명시**. [arXiv 2512.11815](https://arxiv.org/html/2512.11815v2)
- ACM FAccT 2025 "Deepfakes on Demand" — 공개 다운로드 가능한 딥페이크 모델 변형 약 35,000개를 발견, 대부분 Civitai. [ACM DL](https://dl.acm.org/doi/full/10.1145/3715275.3732107)
- LoRA 호스팅 플랫폼의 실제 운영 데이터(lora_recipe와 가장 가까운 비교 대상): NCII/CSAM 성격 모델 183개 삭제, 계정 17,436개 밴. [Civitai Safety Center](https://civitai.com/articles/3266/civitai-safety-center-and-the-prevention-of-csam)
- NIST가 생성형 AI 리스크 분류체계에서 "외설적/모욕적/학대적 콘텐츠"를 CBRN, 폭력적 콘텐츠와 나란히 공식 리스크 카테고리로 명시. [NIST AI 600-1](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf)
**권고:** 이건 버그바운티 스코프 한 줄로 끝날 문제가 아니라 **제품 설계·모더레이션 정책** 차원의 이슈입니다. 최소한: (1) 실제 인물 얼굴을 다루는 기능에 대한 사용 정책·신고 채널이 있는지 우선 점검, (2) lora_recipe가 제3자 가중치를 배포/호스팅하는 구조라면 Civitai 사례처럼 콘텐츠 심사·차단 메커니즘 필요 여부 검토, (3) 버그바운티 스코프에는 "실제 식별 가능한 인물의 비동의 콘텐츠 생성 기법"을 최상위 등급으로 포함하되 안전 관련 신고 채널을 통해 접수(3.2 참고).
**스코프 문구 제안:** "업로드된 참조 사진 등을 이용해 실제 식별 가능한 인물의 비동의 콘텐츠, 또는 미성년자를 성적 맥락으로 묘사하는 콘텐츠를 생성하는 기법 — 최상위 등급으로 인스코프, [안전 전용 채널]로 접수, CSAM 관련 사안은 공개 disclosure 대신 법적 신고 절차로 처리."

### 3.2 세이프티 가드레일 우회 — 별도 트랙으로 설계할 것
**핵심:** 실제 AI 기업들이 "안전 우회"를 유료 버그바운티에 포함하는지, 어떻게 구조화하는지 조사한 결과 — **점점 포함하는 추세지만, 기존 보안 트랙과 분리된 별도 트랙으로 운영**하는 것이 표준입니다.
**근거 (실제 프로그램 비교):**
- **Anthropic**: "Model Safety Bug Bounty" — CBRN·사이버보안 등 고위험 영역의 새로운 범용 탈옥에 최대 $15,000, 일반 보안 VDP와 별도 운영. [Anthropic](https://www.anthropic.com/news/model-safety-bug-bounty)
- **OpenAI**: 보안 버그바운티와 별도로 "Safety Bug Bounty" 운영. 단순 무례한 답변·검색 가능한 정보 수준의 범용 탈옥은 세이프티 트랙에서도 명시적으로 아웃오브스코프 — 실제 오남용 영향이 입증되는 경우만 인정. [OpenAI](https://openai.com/index/safety-bug-bounty/)
- **Google AI VRP**: 반대로 프롬프트 인젝션·탈옥·정렬 문제를 유료 VRP에서 명시적으로 **제외** — "중요하게 생각하지만 유료 VRP 형식이 맞지 않다"는 이유로 별도 비금전 피드백 채널로 분리. VRP는 대신 rogue action, 데이터 유출, 지속적 계정/환경 조작, 모델 탈취, 지속적 DoS 등 "보안적 성격"의 AI 이슈에 보상. [Google Bug Hunters](https://bughunters.google.com/about/rules/google-friends/ai-vulnerability-reward-program-rules)
- **HackerOne**: 플랫폼 차원에서 "AI Safety"(유해/편향 출력, 오남용 시나리오)를 "AI Security"(기술적 익스플로잇)와 별도 카테고리로 설계하도록 권고. [HackerOne AI Bug Bounty 프레임워크](https://docs.hackerone.com/en/articles/12570435-ai-bug-bounty)
**미확인:** Midjourney·Stability AI가 콘텐츠 안전 우회를 스코프에 명시적으로 포함하는지는 공개 문서로 확인하지 못함(추정 금지).
**스코프 문구 제안:** "콘텐츠 안전/가드레일 우회 리포트는 핵심 보안 버그바운티와 별도 트랙(별도 접수 폼·트리아지 팀·보상 체계)으로 운영 — OpenAI/Anthropic 방식을 따라 단순 무례함이 아닌 실질적 오남용 영향이 입증되는 경우만 인정."

---

## 4. 클래식 파일 파싱 & 배치 처리 취약점 (AI와 무관한 기본기)

### 4.1 악성 미디어 파일 파싱 → RCE
**핵심:** 5개 제품 모두 사용자가 올린 이미지/영상/오디오를 파싱함 — AI 요소와 무관하게 수십 년째 이어지는 고전적 RCE 소스.
**근거:** CVE-2016-3714 "ImageTragick" — ImageMagick이 이미지 메타데이터의 쉘 메타문자를 그대로 실행, 공개 전부터 실사용 악용됨. [imagetragick.com](https://imagetragick.com/)
**스코프 문구 제안:** "이미지/영상/오디오/모델 프리뷰 파일 처리 중 발생하는 코드 실행·메모리 손상·쉘 커맨드 인젝션 — 번들된 서드파티 파싱 라이브러리(ImageMagick, FFmpeg 등) 경유 포함 인스코프."

### 4.2 경로 순회 / "Zip Slip" (배치·압축 처리)
**핵심:** bg_batch_kit(대량 파일/압축 업로드 가능성)과 나머지 제품의 일괄 임포트 기능에 직결. 여러 언어에 걸쳐 반복적으로 발견되는 잘 알려진 취약점군.
**근거:** Snyk의 2018 "Zip Slip" 연구, 이후로도 관련 CVE가 계속 발견됨(예: [CVE-2022-48285](https://security.snyk.io/vuln/SNYK-JS-JSZIP-3188562), [CVE-2024-21518](https://security.snyk.io/vuln/SNYK-PHP-OPENCARTOPENCART-7266578)). [원문](https://security.snyk.io/research/zip-slip-vulnerability)
**스코프 문구 제안:** "배치/압축 파일 추출 또는 내보내기 중 의도한 출력 디렉터리 밖에 파일이 쓰이는 경우(경로 순회, 심링크 악용, Zip Slip) — 인스코프."

### 4.3 미디어 처리 라이브러리를 통한 SSRF
**핵심:** shorts_converter(FFmpeg 기반일 가능성 높은 영상 처리)에 특히 관련. 실제로 **유료 보상까지 지급된 선례**가 있음.
**근거:** FFmpeg HLS/자막 디먹서의 CVE-2016-1897/1898, CVE-2017-9993 — 조작된 재생목록/자막으로 임의 로컬 파일 읽기 및 SSRF 유발. **실제 사례**: Automattic(WordPress.com)이 업로드된 영상의 FFmpeg HLS 처리를 통한 SSRF/로컬 파일 노출 리포트에 실제로 보상 지급. [HackerOne #237381](https://hackerone.com/reports/237381)
**스코프 문구 제안:** "영상/오디오 수집 파이프라인(조작된 재생목록·자막·컨테이너 메타데이터 경유)을 통한 SSRF 또는 로컬/내부 파일 노출 — 클라우드 메타데이터 엔드포인트 노출 위험을 고려해 High 등급으로 인스코프."

---

## 5. API 비용 남용 & 리소스 고갈

### 5.1 무제한 GPU 추론 소모 ("지갑 서비스거부")
**핵심:** 5개 제품 모두 과금되는 고비용 GPU 추론을 트리거함 — 요청 단가가 높아 일반 웹앱보다 경제적 DoS 리스크가 오히려 더 큼.
**근거:** OWASP **LLM10:2025 "Unbounded Consumption"**으로 공식 분류. [OWASP](https://genai.owasp.org/llmrisk/llm102025-unbounded-consumption/) — 실제 금전 피해 사례: 노출된 Gemini API 키 하나로 48시간 만에 $82,000 사용(평소 월 사용액의 수백 배), 별도 사고에서는 $600,000 피해. [PointGuard AI](https://www.pointguardai.com/blog/when-a-stolen-ai-api-key-becomes-an-82-000-problem) / [IT Pro](https://www.itpro.com/security/cyber-attacks/hackers-ran-up-a-usd600-000-ai-bill-after-swiping-api-keys-says-metr-and-nobody-realized-for-weeks)
**스코프 문구 제안:** "사용자별 rate limit·쿼터·인증을 우회해 공격자가 통제하는 규모로 GPU 추론 자원을 소모시키는 경우 — 인스코프. 리포트에 요청당 비용과 달성 가능한 요청 속도를 포함할 것(심각도 산정용)."

### 5.2 인증되지 않은 파이프라인 노출 → 컴퓨팅 탈취 ⚠️ scene_renderer/puppet_animator/bg_batch_kit 우선 점검 권장
**핵심:** 이 조사에서 나온 가장 직접적인 실제 선례입니다. scene_renderer·puppet_animator·bg_batch_kit은 모두 노드 기반 생성 파이프라인 구조(Stable Diffusion용 도구 ComfyUI와 동일한 아키텍처 형태)를 가질 가능성이 높은데, **바로 그 구조의 실제 도구가 현재 진행형으로 악용되고 있습니다.**
**근거:** ComfyUI-Manager의 인증되지 않은 원격 설정 조작 취약점 **CVE-2025-67303**(CVSS 7.5)을 악용해 악성 커스텀 노드를 설치, **GPU 서버 1,000대 이상**을 Monero/Conflux 채굴 및 프록시 봇넷으로 편입시키는 캠페인이 2026년 기준 현재도 진행 중. [The Hacker News](https://thehackernews.com/2026/04/over-1000-exposed-comfyui-instances.html) / [Censys](https://censys.com/blog/comfyui-servers-cryptomining-proxy-botnet/)
**권고:** 만약 이 3개 제품이 로컬/네트워크에서 관리 인터페이스나 렌더링 API를 노출하는 구조라면, "기본적으로 인증 없이는 접근 불가"인지부터 최우선으로 확인할 것 — 버그바운티 스코프 이전에 기본 배포 설정 자체를 점검할 가치가 있음.
**스코프 문구 제안:** "인증 없이 렌더링/추론/플러그인 관리 엔드포인트에 접근해 작업 제출, 설정 변경, 커스텀 노드/플러그인 설치가 가능한 경우 — 유사 도구에서 실제 크립토마이닝/봇넷 편입에 쓰인 선례가 있으므로 Critical 등급으로 인스코프."

### 5.3 API 남용을 통한 모델/레시피 추출
**핵심:** lora_recipe(가치의 핵심이 가중치/학습 설정 자체)에 특히 관련. 대량·체계적 쿼리로 보호된 모델의 동작이나 파라미터를 재구성하는 것은 학술적으로 입증된 경로.
**근거:** Tramèr et al., "Stealing Machine Learning Models via Prediction APIs" (USENIX Security 2016) — 실제 상용 ML API를 예측 결과만으로 거의 완벽하게 복제. [USENIX](https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_tramer.pdf). Google AI VRP도 "모델 탈취"를 명시적 보상 대상으로 포함. [Google AI VRP](https://bughunters.google.com/about/rules/google-friends/ai-vulnerability-reward-program-rules)
**스코프 문구 제안:** "체계적 API 쿼리를 통해 독점 레시피/LoRA/모델의 가중치나 파인튜닝 설정을 재구성·추출·무단 복제할 수 있는 경우 — 인스코프. 이를 가능케 하는 rate-limit/쿼리 예산 우회는 일반 쿼터 남용보다 높은 등급으로 취급."

---

## 카테고리 → 제품 관련도

| 카테고리 | scene_renderer | puppet_animator | bg_batch_kit | lora_recipe | shorts_converter |
|---|:---:|:---:|:---:|:---:|:---:|
| 1.1 Pickle RCE | ✓ | ✓ | | ✓✓ | |
| 1.2 가중치 공급망 | ✓ | ✓ | | ✓✓ | |
| 1.3 LoRA 백도어 | | ✓ | | ✓✓ | |
| 2.1 프롬프트 인젝션 | ✓✓ | ✓ | | | ✓ |
| 2.2 비주얼 프롬프트 인젝션 | ✓ | ✓ | ✓ | | ✓ |
| 3.1 딥페이크/NCII 오남용 | ✓ | ✓✓ | | ✓✓ | ✓✓ |
| 3.2 가드레일 우회(트랙 설계) | ✓ | ✓ | | ✓ | ✓ |
| 4.1 미디어 파싱 RCE | ✓ | ✓ | ✓✓ | | ✓✓ |
| 4.2 경로 순회/Zip Slip | | | ✓✓ | ✓ | ✓ |
| 4.3 미디어 라이브러리 SSRF | | ✓ | | | ✓✓ |
| 5.1 지갑 DoS | ✓✓ | ✓✓ | ✓✓ | ✓ | ✓✓ |
| 5.2 인증되지 않은 파이프라인 탈취 | ✓✓ | ✓✓ | ✓✓ | ✓ | ✓ |
| 5.3 모델/레시피 추출 | | | | ✓✓ | |

(✓✓ = 해당 제품의 주요 리스크, ✓ = 부차적/개연성 있는 리스크)

## 확인하지 못한 부분 (추정하지 않음)

- Midjourney·Stability AI가 콘텐츠 안전 우회를 스코프에 명시적으로 포함하는 공개 문서를 찾지 못함(Stability의 Bugcrowd VDP는 존재하나 상세 스코프 페이지를 직접 확인하지 못함).
- LoRA 백도어의 "실제 유포된" 사례(의도적 NCII 오남용과 별개로)는 아직 연구 단계(2025-2026 프리프린트/NDSS)이며 공개된 실제 침해 사례는 아님.
- "3D 씬 생성" 파일 포맷 특화 리스크에 대한 별도 학술 문헌은 찾지 못함 — 일반 이미지/영상 파싱 리스크(4.1)로 갈음.

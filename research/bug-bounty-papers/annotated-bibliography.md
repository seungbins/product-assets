# 버그바운티(Bug Bounty) 연구 논문 주석 목록

복수의 리서치 트랙(① 경제성/정책 ② 해커 행동·비교연구 ③ 법률·정책·최신동향 ④ 국내(한국어) 연구 ⑤ 블록체인/스마트컨트랙트)을 통해 웹 검색·원문 확인(arXiv, USENIX, ACM DL, Oxford Academic, SSRN, KoreaScience, KCI, DBpia, ScienceON, MDPI 등)으로 실존을 검증한 논문 **44편**입니다. 각 논문은 제목/저자/게재처/링크와 함께, 빠르게 훑어볼 수 있는 한글 핵심 요약, 그리고 원 조사 내용을 보존한 상세 요약(해외 논문은 영문, 국내 논문은 국문)을 담고 있습니다.

> 실제 적용 가능한 액션 아이템은 [`program-improvement-recommendations.md`](./program-improvement-recommendations.md)에 별도로 정리했습니다.

---

## 목차

1. [경제성 & 비용 효율성](#1-경제성--비용-효율성)
2. [플랫폼 역학 & 취약점 발견 생태계](#2-플랫폼-역학--취약점-발견-생태계)
3. [정책 설계 & 인센티브/메커니즘 디자인](#3-정책-설계--인센티브메커니즘-디자인)
4. [보안 효과 측정](#4-보안-효과-측정)
5. [해커·리서처 행동 & 동기](#5-해커리서처-행동--동기)
6. [법률·정책 & 정부/기관 사례연구](#6-법률정책--정부기관-사례연구)
7. [기술 특화 & 최신 동향(AI)](#7-기술-특화--최신-동향ai)
8. [국내(한국어) 연구](#8-국내한국어-연구)
9. [블록체인 & 스마트컨트랙트](#9-블록체인--스마트컨트랙트)

---

## 1. 경제성 & 비용 효율성

### An Empirical Study of Vulnerability Rewards Programs
**저자:** Matthew Finifter, Devdatta Akhawe, David Wagner
**게재처:** USENIX Security '13 (22nd USENIX Security Symposium), pp. 273–288, 2013
**링크:** https://www.usenix.org/conference/usenixsecurity13/technical-sessions/presentation/finifter

**핵심 요약:** 버그바운티 연구의 시조 격 논문. Chrome·Firefox의 VRP 지출(각 ~$58만/$57만)을 사내 보안 엔지니어 고용 비용과 비교해, 취약점 보고서의 24~28%가 바운티를 통해 들어왔고 비용 대비 효율이 더 높다는 것을 최초로 정량 입증했다. 보상액과 제보량 사이의 상관관계는 생각보다 약했다는 점도 지적.

<details><summary>영문 상세 요약</summary>

This is the founding empirical paper on VRP economics, comparing Google Chrome's and Mozilla Firefox's vulnerability reward programs. The research question: are VRPs a cost-effective way to find security bugs relative to hiring in-house researchers? Using three years of bounty-payout records, bug-tracker data, and security-advisory data for both browsers (Chrome: ~$580,000 paid across 501 bounties; Firefox: ~$570,000 across 190 bounties), the authors compare VRP spend against the fully-loaded cost of an equivalent in-house security researcher and compute what share of externally reported vulnerabilities entered official security advisories. They find that roughly a quarter to a third of vulnerabilities fixed in each browser (about 28% for Chrome, 24% for Firefox) came through the VRP, and that running the VRP cost substantially less than hiring even one to two full-time engineers with comparable output — making both programs economically efficient. They also note VRPs functioned as a complement to, not a replacement for, internal security teams, and found reward levels were not strongly correlated with submission volume, an early challenge to simple price-elasticity assumptions about hacker behavior. The paper established the methodological template used throughout nearly all later VRP economics research.
</details>

---

### Analyzing Bug Bounty Programs: An Institutional Perspective on the Economics of Software Vulnerabilities
**저자:** Andreas Kuehn, Milton Mueller
**게재처:** 42nd Research Conference on Communication, Information and Internet Policy (TPRC), 2014
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2418812

**핵심 요약:** 버그바운티를 "제도경제학" 관점에서 분석 — Microsoft·Facebook 초기 프로그램의 정책 문서를 분석해, 바운티가 법·규범 공백을 메우는 민간 자율규제(private ordering) 장치로 등장했다고 주장. 프로그램마다 규칙이 제각각이라 여러 프로그램을 오가는 리서처에게 마찰이 크다는 점을 지적.

<details><summary>영문 상세 요약</summary>

This paper asks how bug bounty programs function as new institutions governing the trade of software-vulnerability information. The authors apply Douglass North's institutional economics to case studies of Microsoft's and Facebook's then-new bounty programs, using qualitative document analysis of program rules (eligibility, scope, safe-harbor terms, payment schedules). They argue bounty programs are private-ordering institutions that emerged because public/legal frameworks for vulnerability disclosure were absent or inadequate, reducing transaction costs and legal uncertainty between researchers and vendors. The programs are framed as a market-based alternative to the earlier grey market and full-disclosure norms, though institutional quality varies widely and inconsistent rules across programs create friction for researchers working across many of them.
</details>

---

### An Empirical Study of Bug Bounty Programs
**저자:** Thomas Walshe, Andrew Simpson
**게재처:** 2nd IEEE International Workshop on Intelligent Bug Fixing (IBF 2020), co-located with SANER 2020
**링크:** https://ora.ox.ac.uk/objects/uuid:3245c33c-3542-43c7-9611-257f6116b866 (오픈액세스)

**핵심 요약:** 2013년 Finifter 연구를 플랫폼 시대(HackerOne·Bugcrowd)로 업데이트. 프로그램 연간 운영 비용이 엔지니어 2명 고용 비용보다 낮다는 것을 재확인했지만, 소수 상위 헌터에게 보상·성과가 매우 편중되어 있어 특정 헌터 의존 리스크가 크다는 점을 새로 지적.

<details><summary>영문 상세 요약</summary>

This paper revisits the Finifter-et-al.-style cost/benefit question for the much larger, platform-mediated bounty ecosystem of the late 2010s. Using public program and report data from HackerOne and Bugcrowd, the authors compare average program cost against benchmark salary costs of additional in-house security engineers, alongside analysis of participation concentration and reward distributions. The headline finding is that the average yearly cost of operating a bug bounty program is now lower than the fully loaded cost of two additional software engineers. The paper also documents a highly skewed distribution of researcher earnings and output — a small share of hunters account for most valid reports — and discusses the risk this concentration poses to programs that come to depend on a few top performers.
</details>

---

### Hacking for Good: Leveraging HackerOne Data to Develop an Economic Model of Bug Bounties
**저자:** Kiran Sridhar, Ming Ng
**게재처:** Journal of Cybersecurity, Vol. 7, Issue 1, tyab007, 2021 (오픈액세스)
**링크:** https://academic.oup.com/cybersecurity/article/7/1/tyab007/6168453

**핵심 요약:** HackerOne 5년치(5만+ 유효 리포트) 데이터로 도구변수 회귀분석. 헌터의 "보상 탄력성"은 매우 낮음(0.1~0.2) — 즉 보상을 올려도 리포트 양이 비례해서 늘지 않고, 금전 외 동기(학습·평판)가 더 중요함을 시사. 회사 규모·브랜드는 유효 리포트 수에 거의 영향 없음.

<details><summary>영문 상세 요약</summary>

Using a HackerOne dataset spanning August 2014–January 2020 (50,000+ valid reports, 3,800+ program-level observations), the authors apply two-stage least squares regression with instrumental variables to address the endogeneity of bounty amounts. They find security researchers exhibit a low price elasticity of supply (~0.1–0.2 at the median), consistent with researchers being substantially motivated by non-monetary factors such as learning and reputation. A firm's revenue and brand prominence have negligible effect on valid-report volume, suggesting bounty programs extend crowdsourced security benefits to smaller/less-famous firms. Finance, retail, and healthcare programs receive comparatively fewer valid reports, and reports decline as programs age (partly offset by scope expansion).
</details>

---

### The Simple Economics of an External Shock to a Bug Bounty Platform
**저자:** Aviram Zrahia, Neil Gandal, Sarit Markovich, Michael H. Riordan
**게재처:** Journal of Cybersecurity, Vol. 10, Issue 1, tyae006, 2024
**링크:** https://academic.oup.com/cybersecurity/article/10/1/tyae006/7667075

**핵심 요약:** 코로나19를 "자연실험"으로 활용 — Bugcrowd 데이터(2017–2021)에서 실직/소득감소로 헌터 공급(제보량)이 2020년에 151% 급증했지만, 기업 쪽 수요(신규 프로그램·스코프 확장)는 훨씬 느리게 늘어 중복 제보가 급증하고 헌터 1인당 보상은 하락. 수요가 공급을 따라갔다면 고유 취약점 발견이 최대 64% 더 많았을 것으로 추정.

<details><summary>영문 상세 요약</summary>

This paper uses the COVID-19 pandemic as a natural experiment to ask how a bug bounty platform's supply and demand respond to a large economic shock. Using proprietary Bugcrowd transaction data (2017–2021), the authors model the platform as a two-sided marketplace. They find COVID-19 triggered a large rightward shift in researcher supply (submissions rose ~151% in 2020) while firm-side demand grew far more slowly, producing a sharp rise in duplicate submissions and pushing down average per-researcher rewards. They estimate unique vulnerability discoveries could have been ~64% higher had demand matched the supply shock — a rare natural-experiment contribution with direct platform-policy implications: build more elastic onboarding/scope capacity to absorb positive supply shocks.
</details>

---

### Merchants of Vulnerabilities: How Bug Bounty Programs Benefit Software Vendors
**저자:** Esther Gal-Or, Muhammad Zia Hydari, Rahul Telang
**게재처:** Production and Operations Management, 2026 (accepted; 2024년부터 워킹페이퍼로 유통)
**링크:** https://arxiv.org/abs/2404.17497

**핵심 요약:** ⚠️ 중요 — 버그바운티 프로그램이 있으면 벤더가 오히려 출시 전(pre-release) 테스트 투자를 줄이고 더 일찍 출시하는 "모럴 해저드"가 생길 수 있음을 게임이론으로 증명. 바운티는 사내 보안 투자의 대체재가 아니라 보완재로 취급해야 한다는 시사점.

<details><summary>영문 상세 요약</summary>

The authors build a game-theoretic model of a vendor choosing pre-release testing effort and release timing, where post-release vulnerabilities can be found by ethical hackers (via bounty) or malicious attackers. They identify an "incentive channel" (redirects severe-vulnerability discovery toward ethical disclosure) and a "governance channel" (structured control over remediation). The headline, counter-intuitive finding is a moral-hazard effect: because bounty programs provide a cheap, bounded-cost safety net for post-release discovery, vendors rationally reduce costly pre-release testing and release earlier than they would without a program — even while the vendor becomes more profitable and the overall system more secure on net. They also derive guidance on sizing the invited ethical-hacker pool relative to the expected population of malicious attackers.
</details>

---

### Crowdsourcing from Hackers: Strategic Coopetition and Governance in Bug Bounty Programs
**저자:** Jiali Zhou, Kai-Lung Hui
**게재처:** Management Science, 2026 online first (워킹페이퍼명: "Sleeping with the Enemy", HKUST Business School Research Paper No. 2021-038)
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3940307 (오픈 SSRN 워킹페이퍼)

**핵심 요약:** 바운티 헌터 풀은 잠재적 공격자 풀과 겹친다는 "coopetition(협력+경쟁)" 관점의 모델. 반직관적 결과: 협력적 헌터 수가 늘어난다고 최적 보상액이 항상 늘어나야 하는 건 아니며, 오히려 줄여야 하는 구간도 존재함 — "보상은 무조건 많이 줄수록 좋다"는 통념에 대한 반례.

<details><summary>영문 상세 요약</summary>

This paper asks how firms should set bounty rewards and governance given that participating researchers are drawn from the same pool as potential adversaries. The authors formalize two benefit channels — "attack diversion" and "protection delegation" — and show bounty programs are most valuable to firms with low in-house detection efficiency or a high share of dual-capable ("coopetitive") hackers. A key non-obvious result: optimal bounty rewards can be non-monotonic in the number of cooperative hackers — a firm should sometimes reduce rewards as more researchers join, sharply contrasting the simple "more money attracts more reports" intuition elsewhere in the literature. Even though firms rationally scale back some in-house protection once a program launches, total system security still improves on net.
</details>

---

## 2. 플랫폼 역학 & 취약점 발견 생태계

### An Empirical Study of Web Vulnerability Discovery Ecosystems
**저자:** Mingyi Zhao, Jens Grossklags, Peng Liu
**게재처:** ACM CCS 2015, pp. 1105–1117
**링크:** https://doi.org/10.1145/2810103.2813704 (ACM DL, 페이월)

**핵심 요약:** 중국 Wooyun(무보상·평판 기반, 강제적 공개)과 미국 HackerOne(금전 보상, 자발적 참여)을 정면 비교. 돈이 없어도 평판 시스템만으로 대규모 커뮤니티가 활발히 기여한다는 점, 강제적 참여 모델이 조직 커버리지 면에서 훨씬 넓다는 점을 보여줌. "손쉬운 먹잇감 고갈" 패턴도 최초 문서화.

<details><summary>영문 상세 요약</summary>

The authors collect full public datasets from Wooyun (non-monetary reputation incentives) and HackerOne (monetary bounty), covering thousands of reports across many organizations. Both ecosystems host large, steadily growing researcher communities. Wooyun's community remained highly productive through reputation/ranking mechanisms alone, suggesting non-pecuniary motivation is a powerful driver alongside money. On HackerOne, regression finds a significant positive relationship between bounty size and reported-vulnerability volume. Many client organizations see declining report rates over time (low-hanging-fruit depletion). This was among the first large-sample comparisons of monetary vs. non-monetary crowdsourced vulnerability discovery.
</details>

---

### Given Enough Eyeballs, All Bugs Are Shallow? Revisiting Eric Raymond with Bug Bounty Programs
**저자:** Thomas Maillart, Mingyi Zhao, Jens Grossklags, John Chuang
**게재처:** Journal of Cybersecurity, Vol. 3, Issue 2, pp. 81–90, 2017 (arXiv:1608.03445)
**링크:** https://arxiv.org/abs/1608.03445

**핵심 요약:** 개인 헌터가 한 프로그램에서 찾을 수 있는 버그 수는 금방 한계에 도달함(발견 확률이 t^-0.4로 감소) — "많은 눈"이 도움되는 건 개별 헌터가 계속 잘 찾아서가 아니라 다양한 헌터가 계속 유입되기 때문. 헌터들은 신규 런칭 프로그램으로 쏠리는 경향이 강해, 오래된 프로그램은 보상이 높아도 참여가 급감함.

<details><summary>영문 상세 요약</summary>

Using a large HackerOne panel dataset, the authors model how an individual's probability of finding a new bug in a given program decays over time. Each researcher's expected yield within a single program is strongly bounded, with discovery probability decaying roughly as a power law (~t^-0.4); "more eyeballs" mainly helps by adding researchers with diverse skills, not by making any one researcher more effective over time. They document a strong "front-loading" effect: researchers systematically prioritize newly launched programs over mature ones. Policy implication: firms benefit more from refreshing scope or launching new programs than from expecting sustained output from a static one.
</details>

---

### An Exploratory Study of White Hat Behaviors in a Web Vulnerability Disclosure Program
**저자:** Mingyi Zhao, Jens Grossklags, Kai Chen
**게재처:** ACM CCS Workshop on Security Information Workers (SIW '14), 2014, pp. 51–58
**링크:** https://dl.acm.org/doi/10.1145/2663887.2663906

**핵심 요약:** Wooyun 3.5년치 데이터(화이트햇 3,254명, 리포트 16,446건) 분석. 소수 최상위 기여자가 리포트를 많이 차지하지만, 훨씬 많은 저활동 헌터 집단도 광범위한 대상 조직에 걸쳐 중복되지 않는 의미 있는 기여를 함 — "다양성이 곧 생산성"이라는 초기 실증 근거.

<details><summary>영문 상세 요약</summary>

One of the earliest empirical studies of "white hat" hacker behavior at scale. The authors find Wooyun continuously attracted new contributors throughout the period studied, and while a small set of top contributors accounted for a disproportionate share of reports, a much larger population of less-active hunters still made substantial, non-redundant contributions across a broad range of target organizations. This diversity of contributor skill sets and targeting strategies is directly relevant to aggregate productivity — an early empirical grounding for arguments that crowdsourced hunting benefits from breadth of participation, not just concentration among elite hunters.
</details>

---

### Understanding the Heterogeneity of Contributors in Bug Bounty Programs
**저자:** Hideaki Hata, Mingyu Guo, Muhammad Ali Babar
**게재처:** ACM/IEEE ESEM 2017 (arXiv:1709.06224)
**링크:** https://arxiv.org/abs/1709.06224

**핵심 요약:** 기여자를 "프로젝트 특화형"(특정 제품/커뮤니티에 애착이 있어 참여)과 "비특화형"(보상·평판·실력향상 등 일반적 동기로 여러 프로그램을 옮겨다님) 두 유형으로 구분. 두 유형은 동기부여 방식이 달라야 한다는 시사점 — 예: 자사 제품 사용자 커뮤니티를 헌터로 유도하는 전략이 유효할 수 있음.

<details><summary>영문 상세 요약</summary>

Combining a quantitative analysis of 82 bug bounty programs and 2,504 contributors with a qualitative survey, the authors identify a core distinction between "project-specific" contributors (motivated by attachment to a particular product/community) and "non-specific" contributors (hunt broadly, motivated by money/reputation/skill development). This heterogeneity has direct implications for program design: recruitment, communication, and incentive strategies that work for reputation-seeking generalists may not engage loyalty-driven specialists, and vice versa.
</details>

---

### Who are Vulnerability Reporters? A Large-scale Empirical Study on FLOSS
**저자:** Nikolaos Alexopoulos, Andrew Meneely, Dorian Arnouts, Max Mühlhäuser
**게재처:** ACM/IEEE ESEM 2021
**링크:** https://dl.acm.org/doi/10.1145/3475716.3475783

**핵심 요약:** 금전 보상이 없는 오픈소스(FLOSS) 생태계에서도 상용 버그바운티와 유사하게 소수 기여자에게 리포트가 집중되지만, 일회성 신규 제보자들도 전체 리포트의 상당 부분을 차지함 — 금전 보상 유무와 무관하게 "폭넓은 참여 기반 유지"가 중요하다는 걸 재확인.

<details><summary>영문 상세 요약</summary>

This paper extends the "who does vulnerability discovery" question beyond commercial bug bounty platforms into FLOSS projects, where reporting is typically uncompensated. Applying concentration metrics (including a generalized Pareto-style measure), the study finds reporting activity is highly concentrated among prolific reporters, while first-time/one-off reporters collectively still account for a substantial share of total reports — reinforcing that a broad, continually renewing base of occasional contributors is important even absent formal monetary incentives.
</details>

---

## 3. 정책 설계 & 인센티브/메커니즘 디자인

### Banishing Misaligned Incentives for Validating Reports in Bug-Bounty Platforms
**저자:** Aron Laszka, Mingyi Zhao, Jens Grossklags
**게재처:** ESORICS 2016, LNCS vol. 9879, pp. 161–178
**링크:** https://www.cs.cit.tum.de/fileadmin/w00cfj/ct/papers/2016-ESORICS-Laszka.pdf (오픈액세스)

**핵심 요약:** 왜 무효/중복 리포트가 그렇게 많은지를 게임이론으로 규명 — 헌터는 유효 리포트에만 보상받고 무효 리포트 제출엔 비용이 거의 없어 "일단 많이 제출"하는 게 합리적 전략이 되어버림. 신뢰도/확신도를 함께 제출하게 하는 신호 메커니즘을 대안으로 제시.

<details><summary>영문 상세 요약</summary>

The authors build a game-theoretic/mechanism-design model of the report-validation stage: because researchers are paid only for valid, novel reports but bear little cost for invalid ones, they are rationally incentivized to over-submit low-quality reports. Common existing countermeasures (flat reputation penalties, simple rate limits) are shown to be insufficient. The authors propose letting researchers signal their effort/confidence level, allowing platforms to elicit more truthful submissions and allocate validation effort more efficiently — foreshadowing confidence/signal scoring features later adopted in practice.
</details>

---

### Devising Effective Policies for Bug-Bounty Platforms and Security Vulnerability Discovery
**저자:** Mingyi Zhao, Aron Laszka, Jens Grossklags
**게재처:** Journal of Information Policy, Vol. 7, pp. 372–418, 2017
**링크:** https://www.aronlaszka.com/papers/zhao_devising.pdf (오픈액세스)

**핵심 요약:** 보상 구조·스코프·응답시간 약속·커뮤니케이션 관행 등 어떤 정책 레버가 실제로 유효한 노력을 끌어내는지 정리. 보상이 낮거나 불투명한 프로그램은 헌터의 노력을 낭비시킨다는 점을 강조. 정부가 버그바운티를 의무화해야 하는지에 대한 정책 논의도 포함.

<details><summary>영문 상세 요약</summary>

Building on the authors' related empirical/game-theoretic work, they construct models on how firms should design reward schedules and scope to attract effort efficiently, and how platform competition affects researcher allocation. They identify concrete policy levers — reward structure, scope definition, response-time commitments, communication practices — that materially affect useful effort attracted; poorly designed policies (low, flat, or opaque rewards) waste researcher effort and depress discovery. They also discuss whether governments should mandate/subsidize bug bounties, cautioning against one-size-fits-all mandates.
</details>

---

### Bug Bounty Programs for Cybersecurity: Practices, Issues, and Recommendations
**저자:** Suresh Malladi, Hemang Subramanian
**게재처:** IEEE Software, Vol. 37, No. 1, pp. 31–39, 2020
**링크:** https://doi.org/10.1109/MS.2018.2880508 (IEEE Xplore, 페이월)

**핵심 요약:** 실무자 대상 논문. 프로그램 41개의 정책 문서 + 54개 벤더/533개 취약점 데이터를 분석해 "보상액보다 스코프와 프로그램 성숙도가 발견량을 더 크게 좌우한다"는 역설적 결론 도출. 출시 후가 아니라 개발 단계부터 바운티를 통합하고, 프리릴리즈/베타 코드도 대상에 포함하라고 권고.

<details><summary>영문 상세 요약</summary>

Using grounded-theory analysis of 41 bug-bounty program specifications combined with ~2 years of empirical data (54 vendors, 533 disclosed vulnerabilities), the authors organize practices into five areas: scope, timing of crowd engagement across the software lifecycle, submission-quality management, firm–researcher communication, and hacker motivation. Recommendations include integrating bounty programs into product development rather than adding them post-release, engaging researchers on pre-release/beta code, and tying rewards to demonstrated bug/fix value. Notably, they report an inverse relationship between bugs discovered and bounty size — scope and maturity, not reward money alone, are the primary yield drivers.
</details>

---

### Coordinated Vulnerability Disclosure Programme Effectiveness: Issues and Recommendations
**저자:** Thomas Walshe, Andrew Simpson
**게재처:** Computers & Security, Vol. 123, 102936, 2022
**링크:** https://ora.ox.ac.uk/objects/uuid:58b63628-8a00-4958-8d1f-8c880bfc8d91 (오픈액세스)

**핵심 요약:** 운영자 39명 설문 + 심층 인터뷰 8건. 수년 전 지적된 "저품질 리포트로 인한 트리아지 부담" 문제가 지금도 거의 그대로 반복되고 있다는 다소 씁쓸한 결론. 다만 프로그램에서 나온 신호가 테스트 방법론·요구사항 명세 등 조직의 상위 보안 프로세스 개선에 실제로 피드백된다는 긍정적 발견도 있음.

<details><summary>영문 상세 요약</summary>

Based on 39 survey responses and 8 in-depth interviews with CVD/bounty program operators, the authors find persistent operational obstacles — high volumes of low-quality reports straining triage, staffing/legal-clarity challenges — echoing problems identified years earlier by Laszka, Zhao, and Grossklags. They also find program results increasingly feed back into broader organizational security practice (testing methodology, requirements specification), suggesting CVD/bounty programs function as an organizational learning mechanism. Recommendations: clearer scoping, dedicated triage staffing, better use of program data to inform upstream development practice.
</details>

---

### Incentives and Outcomes in Bug Bounties
**저자:** Serena Wang, Martino Banchio, Krzysztof Kotowicz, Katrina Ligett, R. Preston McAfee, Eduardo Vela Nava
**게재처:** arXiv 2509.16655, 2025년 9월 게시 — **동료심사 전 프리프린트** (일부 저자가 Google VRP 소속, 이해관계 고려 필요)
**링크:** https://arxiv.org/abs/2509.16655

**핵심 요약:** 2024년 7월 Google VRP가 최고 등급 보상을 최대 200% 인상한 실제 정책 변화를 "자연실험"으로 분석. 보상 인상이 (1) 기존 헌터의 고임팩트 취약점으로의 노력 재배분, (2) 신규 헌터 유입이라는 두 경로 모두를 통해 제보의 양과 질을 실제로 끌어올렸다는 드문 인과적(상관관계 아닌) 증거를 제시.

<details><summary>영문 상세 요약</summary>

This working paper studies a July 2024 change to Google's VRP that raised payouts by up to 200% for the highest-impact vulnerability tier. Exploiting the change as a natural experiment, the authors separate two behavioral channels: existing researchers reallocating effort toward higher-impact vulnerability classes, versus new researchers entering because of improved incentives. The reward increase produced measurable gains in both volume and severity/quality mix, driven by a combination of both channels — rare program-scale causal evidence that bounty economics meaningfully shape real-world vulnerability discovery outcomes.
</details>

---

## 4. 보안 효과 측정

### The Benefits of Vulnerability Discovery and Bug Bounty Programs: Case Studies of Chromium and Firefox
**저자:** Soodeh Atefi, Amutheezan Sivagnanam, Afiya Ayman, Jens Grossklags, Aron Laszka
**게재처:** ACM Web Conference 2023 (WWW '23) (arXiv:2301.12092)
**링크:** https://arxiv.org/abs/2301.12092

**핵심 요약:** "리포트 개수"가 아니라 "그 취약점을 공격자가 독자적으로 재발견했을 확률(rediscovery probability)"이라는 새 지표로 실제 보안 효과를 측정. 바운티는 실제로 공격자의 진입장벽을 높이지만, 외부 헌터가 찾는 버그 유형이 실제 악용되는 버그 유형과 잘 안 맞는 경우가 많고, 특히 프리릴리즈/베타 채널에 대한 인센티브가 부족하다는 점을 지적.

<details><summary>영문 상세 요약</summary>

Using over a decade of Chromium and Firefox VRP vulnerability records, the authors distinguish vulnerabilities found by external hunters, internal teams, and those confirmed exploited in the wild, introducing "probability of rediscovery" as a novel metric. They find vulnerability discovery/patching meaningfully raises the difficulty for attackers, but current bounty incentives are imperfectly targeted: external hunters' output doesn't closely track the profile of vulnerabilities that end up exploited, and development/beta release channels appear under-incentivized relative to their security value. Recommendation: redesign reward structures to better align hunter effort with real-world threat-actor behavior.
</details>

---

## 5. 해커·리서처 행동 & 동기

### Hackers vs. Testers: A Comparison of Software Vulnerability Discovery Processes
**저자:** Daniel Votipka, Rock Stevens, Elissa M. Redmiles, Jeremy Hu, Michelle L. Mazurek
**게재처:** IEEE S&P 2018, pp. 374–391 — Distinguished Paper Award
**링크:** https://www.umiacs.umd.edu/~dvotipka/papers/VotipkaHackerTesters2018.pdf

**핵심 요약:** 외부 해커와 사내 테스터를 심층 인터뷰(각 25명)로 비교. 두 그룹의 "탐색 프로세스" 자체는 구조적으로 비슷하지만, 해커는 공격자 마인드셋과 익스플로잇 지향 휴리스틱을, 테스터는 기능 명세 기반 지식을 주로 활용 — 이 지식 차이가 해커가 더 "공격자 관점에서 위험한" 버그를 찾아내는 이유라고 설명.

<details><summary>영문 상세 요약</summary>

Through 25 semi-structured interviews split between practicing hackers and professional testers, the authors build a descriptive process model of how each group searches for, hypothesizes about, and confirms vulnerabilities. The two groups' underlying processes are structurally similar, but hackers and testers differ sharply in the knowledge they bring: hackers draw on broader attacker-mindset training, testers rely more on functional-specification knowledge. This knowledge gap explains why hackers tend to surface exploitable, attacker-relevant bugs that testers miss. Recommendations: more adversarial/security training for testers, better hacker-developer communication channels, and incentive structures that better motivate hacker participation and reporting quality.
</details>

---

### Bug Hunters' Perspectives on the Challenges and Benefits of the Bug Bounty Ecosystem
**저자:** Omer Akgul, Taha Eghtesad, Amit Elazari, Omprakash Gnawali, Jens Grossklags, Michelle L. Mazurek, Daniel Votipka, Aron Laszka
**게재처:** USENIX Security '23 — Distinguished Paper Award (arXiv:2301.04781)
**링크:** https://arxiv.org/abs/2301.04781

**핵심 요약:** ⭐ 이 리서치 전체에서 가장 실무 적용도가 높은 논문 중 하나. 헌터 159명 설문 + 24명 인터뷰. **금전 보상과 학습/실력향상이 최고 동기**, 반대로 **평판은 의외로 동기 순위가 낮음**. 가장 큰 고통은 "불명확한 스코프"와 "느리고 일관성 없는 트리아지 커뮤니케이션(응답 지연, 보상/심각도 분쟁)".

<details><summary>영문 상세 요약</summary>

The methodology is a three-stage mixed-methods design: an open-ended free-listing survey (n=56), a factor-rating survey (n=159), and semi-structured interviews (n=24) — together surfacing 54 distinct factors. Monetary rewards and learning/skill-development opportunities are the most valued benefits; reputation-building ranks surprisingly low, contradicting some industry narratives. Program scope (unclear or overly restrictive) is the single most consequential challenge factor, and poor communication — unresponsive triagers, disputes over report validity/severity, inconsistent payment decisions — is the most damaging recurring pain point, actively suppressing participation from an "underutilized" pool of potential hunters.
</details>

---

### Vulnerability Discovery for All: Experiences of Marginalization in Vulnerability Discovery
**저자:** Kelsey R. Fulton, Samantha Katcher, Kevin Song, Marshini Chetty, Michelle L. Mazurek, Chloé Messdaghi, Daniel Votipka
**게재처:** IEEE S&P 2023, pp. 1997–2014
**링크:** https://www.eecs.tufts.edu/~dvotipka/files/papers/FultonV4A2023.pdf

**핵심 요약:** 소외 계층 헌터 16명 심층 인터뷰. 대부분 비공식 자기주도학습(CTF, 온라인 write-up)으로 입문했고, 좋은 멘토를 만나는 것이 지속 참여의 가장 큰 열쇠였지만 정작 멘토 접근 자체가 어려움. 인터뷰 참여자 16명 전원이 성차별·인종차별·트랜스포비아·성폭력 등 어떤 형태로든 편견을 경험했다고 응답 — 익명 멘토링·스폰서십 체계 도입을 권고.

<details><summary>영문 상세 요약</summary>

Motivated by the vulnerability-discovery workforce's documented homogeneity (~94% male, ~90% white/Asian in surveys), this study conducted 16 semi-structured interviews with self-identified marginalized community members. Most entered the field through unstructured, self-directed learning; finding a good mentor was the single strongest lever for persistence, yet mentorship was hard to access without already having an entry-level job. All 16 participants reported experiencing some form of bias, and many adopted pseudonymity to conceal marginalized aspects of identity. Recommendations: anonymous mentoring systems, mentor-mentee matching, sponsorship (not just mentorship), clearer community conduct norms.
</details>

---

### "You've Got Your Nice List of Bugs, Now What?" Vulnerability Discovery and Management Processes in the Wild
**저자:** Noura Alomar, Primal Wijesekera, Edward Qiu, Serge Egelman
**게재처:** SOUPS 2020 (USENIX)
**링크:** https://www.usenix.org/system/files/soups2020-alomar.pdf

**핵심 요약:** 조직(보안팀) 쪽 관점 — 실무자 53명 인터뷰. 버그바운티가 사내 보안팀 유지 비용을 아끼는 "대체 수단"으로 (옳든 그르든) 인식되는 경우가 많다는 점, 그리고 "발견"보다 오히려 "치료(remediation)"에서 조직들이 더 어려움을 겪는다는 점을 지적 — 팀 간 신뢰 부족, 보안-엔지니어링 소통 부재, 인력 부족이 원인.

<details><summary>영문 상세 요약</summary>

The authors conducted 53 interviews with security practitioners, asking how security teams choose among and combine internal review, red/blue/purple teams, third-party pentesting, and bug bounty programs. Bug bounty programs are frequently perceived as a cost-effective substitute for maintaining a larger internal security team. Regardless of method combination, vulnerability *remediation* (not discovery) is where organizations most often struggle, hampered by cross-team trust deficits, poor security-engineering communication, and chronic funding/staffing shortfalls.
</details>

---

## 6. 법률·정책 & 정부/기관 사례연구

### Private Ordering Shaping Cybersecurity Policy: The Case of Bug Bounties
**저자:** Amit Elazari Bar On
**게재처:** *Rewired: Cybersecurity Governance* 도서 챕터 (Wiley, 2019); 워킹페이퍼는 2017년부터 유통
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3161758

**핵심 요약:** ⚠️ 법적 안전장치("safe harbor") 관련 가장 중요한 논문. 수백 개 버그바운티 프로그램의 법적 조항을 분석한 결과, **당시 DOJ 기준에 부합하는 진짜 safe harbor 조항을 갖춘 프로그램은 극소수**였고 대부분은 모호한 문구로 법적 리스크를 오히려 헌터에게 떠넘기고 있었음. 이후 disclose.io 등 표준 safe harbor 템플릿 운동의 출발점이 된 논문.

<details><summary>영문 상세 요약</summary>

The research question is whether bug bounty programs' legal terms actually authorize researchers' access and shield them from liability (CFAA, DMCA §1201), or merely claim to. Through systematic content analysis of legal terms across hundreds of programs, benchmarked against the DOJ's framework for authorizing good-faith security research, the author finds only a small handful of programs met a genuine DOJ-aligned safe-harbor standard; most retained broad, discretionary, or ambiguous language that effectively shifted legal risk onto researchers. Elazari frames this as "private ordering" — corporate contract terms de facto setting cybersecurity/CFAA policy — and argues for standardized, Creative-Commons-style legal templates.
</details>

---

### Navigating Vulnerability Markets and Bug Bounty Programs: A Public Policy Perspective
**저자:** Aviram Zrahia
**게재처:** Internet Policy Review, Vol. 13, Issue 1, 2024년 2월
**링크:** https://policyreview.info/articles/analysis/navigating-vulnerability-markets-and-bug-bounty-programs

**핵심 요약:** 정부 정책 관점에서 (1) 시큐어 개발 관행 의무화, (2) 정부의 취약점 매입(그레이마켓), (3) 버그바운티 장려라는 세 가지 대안을 비교 평가. 플랫폼이 정보 비대칭과 거래비용을 낮춰주는 버그바운티가 세 대안 중 발견량·비용효율·접근성 면에서 가장 정책 효과가 높다고 결론.

<details><summary>영문 상세 요약</summary>

Zrahia compares three government policy alternatives for improving vulnerability discovery/disclosure: mandating secure-development practices, government acquisition of exploitable vulnerabilities (gray market), and promoting bug bounty programs. Using a structured qualitative policy-impact analysis scored across six impact categories, the paper finds bug bounty programs — mediated by platforms that reduce information asymmetries and transaction costs — produce the highest overall policy impact of the three, outperforming on discovery volume, cost-efficiency, and disclosure accessibility. The three approaches are concluded to be complementary rather than mutually exclusive.
</details>

---

### Crowdsourced Cybersecurity Innovation: The Case of the Pentagon's Vulnerability Reward Program
**저자:** Akemi Takeoka Chatfield, Christopher G. Reddick
**게재처:** Information Polity, Vol. 23, No. 2, 2018 (dg.o '17 학회 발표본도 존재)
**링크:** https://ro.uow.edu.au/eispapers1/556/ (오픈액세스)

**핵심 요약:** 미 국방부 최초의 버그바운티 "Hack the Pentagon"(2016) 사례연구. 등록 리서처 약 1,400명, 유효 제출 250건, 검증된 고유 취약점 138건, 지급액 $75,000. 보수적인 정부 관료조직이 어떻게 민간식 크라우드소싱 보안 혁신을 받아들였는지를 공공행정/혁신수용 이론으로 분석 — 이후 Hack the Army, Hack the Air Force로 이어진 정책 확산의 출발점.

<details><summary>영문 상세 요약</summary>

This is a direct academic case study of "Hack the Pentagon," the DoD's 2016 pilot VRP run with HackerOne — the first bug bounty program in U.S. federal government history. The authors examine the organizational/institutional factors — DoD leadership buy-in via the Defense Digital Service, legal authorization structures, risk-management adaptations — that allowed a famously risk-averse defense bureaucracy to embrace crowdsourced ethical hacking, and discuss how the pilot's success catalyzed DoD's subsequent formal Vulnerability Disclosure Policy and follow-on programs.
</details>

---

### Your Vulnerability Disclosure Is Important To Us: An Analysis of Coordinated Vulnerability Disclosure Responses Using a Real Security Issue
**저자:** Koen van Hove, Jeroen van der Ham-de Vos, Roland van Rijswijk-Deij
**게재처:** ACM Digital Threats: Research and Practice, Vol. 7, Issue 2, pp. 1–24 (arXiv:2312.07284)
**링크:** https://arxiv.org/abs/2312.07284

**핵심 요약:** 실제로 발견한 이메일 스푸핑 취약점을 다수 조직에 실제로 신고해보는 "필드 실험". 공식 취약점 신고 정책을 갖춘 조직조차 90일 관찰 기간 내 리포트의 절반 가량이 무응답/미해결로 남았음 — CVD "정책상 존재"와 "실제 작동"의 큰 간극을 실증.

<details><summary>영문 상세 요약</summary>

Rather than surveying opinions about CVD, this paper uses a real, self-discovered email-spoofing vulnerability affecting numerous mail providers as an instrument to empirically measure organizational response. The authors sent disclosure reports to affected organizations and tracked response times, quality, and remediation outcomes over 90 days, comparing organizations with published disclosure policies against those without. Findings are notably pessimistic: many organizations are difficult to reach even with a nominal security contact point, and even among organizations with a formal disclosure policy, roughly half of reports remained unanswered/unresolved after 90 days.
</details>

---

## 7. 기술 특화 & 최신 동향(AI)

### Cryptography Vulnerabilities on HackerOne
**저자:** Mohammadreza Hazhirpasand, Mohammad Ghafari
**게재처:** IEEE QRS 2021 (arXiv:2111.03859)
**링크:** https://arxiv.org/abs/2111.03859

**핵심 요약:** HackerOne 공개 리포트 중 암호화 관련 취약점만 골라 8개 테마로 분류(약한 알고리즘, 키 관리 부실, 불충분한 난수, TLS/인증서 검증 오류 등). 대부분 암호 라이브러리 자체의 결함이 아니라 "개발자의 오사용"에서 비롯된다는 게 핵심 결론 — 개발팀 교육 자료로 활용 가치가 높음.

<details><summary>영문 상세 요약</summary>

Using HackerOne's public disclosure archive, the authors classify cryptography-related vulnerability reports into eight recurring thematic categories, discussing for each the root cause, real-world consequence, and recommended prevention. Cryptographic vulnerabilities found via bug bounty tend to stem from misuse of otherwise-sound cryptographic libraries/APIs (developer-level misunderstanding) rather than flaws in the underlying primitives — an educational taxonomy to help developers avoid common bounty-documented mistakes.
</details>

---

### CAI: An Open, Bug Bounty-Ready Cybersecurity AI
**저자:** Víctor Mayoral-Vilches 외 12인
**게재처:** arXiv 2504.06017, 2025년 4월 게시 — **동료심사 전 프리프린트, 일부 저자 상업적 로보틱스/보안 회사 소속(자체 발표 수치이므로 독립 검증 필요)**
**링크:** https://arxiv.org/abs/2504.06017

**핵심 요약:** ⚠️ 주목할 최신 동향 — 실전 버그바운티/CTF에 곧바로 투입 가능하도록 설계된 오픈소스 LLM 에이전트 프레임워크. 자체 발표 기준 CTF 벤치마크 SOTA, AI 전용 팀 중 1위, Hack The Box 세계 500위권, 특정 작업에서 인간 대비 최대 3,600배 빠른 속도와 156배 낮은 비용을 주장. **자체 보고 수치이므로 액면 그대로 받아들이지 말고 독립 재현 결과를 기다릴 것.**

<details><summary>영문 상세 요약</summary>

This preprint presents CAI, an open-source LLM-agent framework explicitly designed for real bug bounty/CTF engagements, positioned as a response to a growing gap between well-resourced offensive AI capabilities and tooling available to individual ethical hackers. Benchmark evaluation across CTF challenge sets and Hack The Box, plus an AI-vs-human CTF competition, reports state-of-the-art CTF results, first place among AI-only teams, top-500 worldwide Hack The Box ranking, up to ~3,600x faster task completion than human baselines, and ~156x lower estimated cost. These are self-reported, industry-authored preprint claims — not independently peer-reviewed — and several authors are affiliated with a commercial company, so the magnitude of these claims warrants independent replication.
</details>

---

## 8. 국내(한국어) 연구

RISS·KCI·DBpia·KoreaScience·ScienceON 원문 대조로 검증한 국내 논문·학위논문 9편입니다. "국내 기업(삼성/네이버/카카오)의 버그바운티 운영 사례를 다룬 전용 학술 논문"은 조사 결과 존재하지 않았습니다(언론 기사·기업 블로그만 확인) — 학술 문헌의 공백으로 기록해둡니다.

### 한국 버그 바운티 프로그램의 제도적인 문제점과 해결방안
**저자:** 박혜성, 권헌영 (고려대학교)
**게재처:** 한국IT서비스학회지, 18권 5호, 2019, pp.53-70
**링크:** https://www.koreascience.kr/article/JAKO201910861317205.page (오픈액세스)
**핵심 요약:** KISA '소프트웨어 신규 취약점 신고포상제'(한국형 버그바운티)의 약 7년간 운영 경험에서 드러난 제도적 한계(포상 기준, 참여 유인 부족, 법적 보호 미비)를 진단하고 시장 지향적 정부 정책 등 개선방안을 제시.

### 기업 제품의 보안 취약점 개선을 위한 보상제 동향
**저자:** 유동훈((주)아이넷캅), 노봉남(전남대학교)
**게재처:** 정보보호학회지(Review of KIISC), 28권 2호, 2018, pp.43-50
**링크:** https://koreascience.kr/article/JAKO201814442074014.page?lang=ko (오픈액세스)
**핵심 요약:** 국내외 기업의 보안취약점 신고포상제(버그바운티) 운영 동향 개관. 해외 벤더의 SW 개발 전 단계 취약점 발굴 내재화 사례와, 배포 후 외부 화이트해커 집단지성을 활용하는 국내외 프로그램 사례를 비교.

### 화이트 해커 양성 및 활성화 방안에 대한 연구
**저자:** 홍준호(한국정보보호산업협회), 유현우(단국대학교)
**게재처:** 법학연구, 17권 4호(통권 68호), 2017, pp.463-515 (한국법학회)
**링크:** https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE07285175 (DBpia, 유료/기관 접근)
**핵심 요약:** 화이트 해커의 역할을 법·제도, 교육, 지원·관리 세 차원에서 검토. 모의해킹·취약점 점검 등 윤리적 해킹 활동을 뒷받침할 법적 근거 마련과 국가 차원 인력 양성 체계 구축 필요성을 강조.

### 블랙해커가 화이트해커로 전환하는데 미치는 요인에 관한 연구
**저자:** 김병천 (지도교수: 신용태) — 숭실대학교 박사학위논문
**게재처:** 숭실대학교 대학원, 2019
**링크:** https://www.dbpia.co.kr/journal/detail?nodeId=T15305510
**핵심 요약:** PPM(Push-Pull-Mooring) 모델로 언더그라운드·화이트해커 커뮤니티 239명을 설문. 생계 문제가 가장 강한 '푸시' 요인, 성장 욕구가 주요 '풀' 요인. 국내 화이트해커는 200~400명 수준으로 미국(7만)·중국(35만) 대비 현저히 적고, 좁은 시장과 낮은 사회적 인식이 핵심 장벽이라고 진단.

### 보안취약점의 사회적 인식과 법·기술적 대응전략
**저자:** 윤상필 (지도교수: 권헌영) — 고려대학교 박사학위논문
**게재처:** 고려대학교 정보보호대학원, 2021 (이후 단행본 『사이버보안취약점의 법적 규제』로 출간)
**링크:** https://scienceon.kisti.re.kr/srch/selectPORSrchArticle.do?cn=DIKO0015944523
**핵심 요약:** 취약점 공개 관행, 버그바운티 프로그램, 제로데이 익스플로잇, 취약점 마켓, 보안연구와 법 집행 간의 긴장관계를 종합 검토. 국가 차원의 취약점 데이터베이스 구축과 연구 윤리기준 마련 등 대응전략 제시.

### 선의의 취약점 탐지 행위에 관한 형사법적 검토
**저자:** 송영진, 신상현, 장응혁, 김기범
**게재처:** 형사정책연구, 35권 2호, 2024, pp.59-96 (한국형사법무정책연구원)
**링크:** https://www.kicj.re.kr/boardDownload.es?bid=0003&list_no=15240&seq=3 (오픈액세스 PDF)
**핵심 요약:** 윤리적 해커의 선의 취약점 탐지가 정보통신망법상 처벌 대상이 될 수 있는 법적 공백을 미국·벨기에·독일·일본 비교법으로 분석. KISA 신고포상제 및 2022년 신설 정보통신망법 제47조의6(포상금 지급 근거) 운영 현황을 검토하고 입법 개선방안 제안.

### 선의의 취약점 탐지 면책에 대한 미국 제도의 발전 과정과 국내 법제 시사점
**저자:** 조현재, 오소정, 문병훈, 김기범 (성균관대학교)
**게재처:** 정보보호학회논문지, 36권 3호, 2026, pp.1025-1045
**링크:** KCI ART003346524
**핵심 요약:** 미국의 선의 취약점 탐지 면책 제도(2015 DMCA §1201 예외, 2021 Van Buren 판결, 2022 DOJ 기소지침) 발전 과정 분석. 취약점공개정책(VDP)이 입법과 함께 핵심 보호장치로 기능한다고 평가, 국내 맥락에 맞춘 다층적 법제 설계방안 제안.

### 보안취약점 협력대응제도(CVD) 도입을 위한 법제화 방안 연구 — 정보통신망법 중심으로
**저자:** 이태승 (한국인터넷진흥원 KISA)
**게재처:** 정보보호학회논문지, 34권 4호, 2024, pp.781-799
**링크:** DBpia NODE11909848 (유료/기관 접근)
**핵심 요약:** *버그바운티 인접 주제.* 정보통신망법 중심의 CVD 국내 법제화 3단계 도입방안. 취약점 공개정책 수립, 보안연구자 법적 보호, 조정기관(coordinator) 지정 등 제도 설계 요건을 도출해 국내 신고포상제·버그바운티 생태계의 법적 기반 강화방안 논의.

### 버그바운티 프로그램의 특성이 기업의 보안성에 미치는 영향: 데이터 유출 사례를 중심으로
**저자:** 김준태, 한진수 (KAIST) — 학술대회 발표논문
**게재처:** 한국경영정보학회 2025년 춘계통합학술대회 발표논문집, 2025.05, pp.763-770
**링크:** https://www.earticle.net/Article/A472713 (유료/기관 접근)
**핵심 요약:** 버그바운티 플랫폼 데이터로 프로그램 특성이 기업 보안성(데이터 유출 빈도)에 미치는 영향을 실증. 포상금을 지급하지 않는 기업보다 지급하는 기업에서 오히려 데이터 유출 빈도가 증가하는 반직관적 결과 발견 — 정식 학술지 논문이 아닌 컨퍼런스 발표논문임에 유의.

> **인용 금지 권장 (실재 확인 실패):** 조사 과정에서 "김형열·김태성(2016)", "윤선영(2020, 동국대 석사)", "이태훈(2026, 건국대 석사)", "이창훈, 「군사」(2022)" 4건이 검색 결과에 함께 나타났으나, 1차 출처(KCI/DBpia/RISS)로 독립 검증하지 못했습니다. 일부는 허위 정보(환각)일 가능성이 있어 목록에서 제외했으며, 실제 인용이 필요하면 반드시 직접 원문을 재확인하세요.

---

## 9. 블록체인 & 스마트컨트랙트

전통적인 웹/소프트웨어 버그바운티(HackerOne, Bugcrowd)와 구조·경제성이 다른 블록체인/DeFi 버그바운티(Immunefi, Code4rena 등) 연구입니다. WebSearch/WebFetch에 더해 페이월로 막힌 원문은 PDF 직접 추출로 대조 검증했습니다.

### Predicting the Effectiveness of Blockchain Bug Bounty Programs
**저자:** Ed Marcavage, Jake Mason, Chen Zhong (University of Tampa)
**게재처:** 36th International FLAIRS Conference (FLAIRS-36), 2023
**링크:** https://journals.flvc.org/FLAIRS/article/view/133377 (오픈액세스)

**핵심 요약:** HackerOne·Bugcrowd·HackenProof·Immunefi에서 수집한 블록체인 버그바운티 프로그램 약 200개를 분석 — 보상액이 아니라 "정책 문서의 텍스트 구성"과 "스코프 내 Solidity 함수 종류·소스코드 공개 여부" 같은 기술적 스코핑 선택이 헌터 참여도를 유의미하게 좌우한다는 것을 회귀분석으로 입증. 블록체인 버그바운티의 "프로그램 설계 자체"를 통계적으로 모델링한 몇 안 되는 논문.

<details><summary>영문 상세 요약</summary>

Investigates what structural and textual features of a blockchain bug bounty program predict its ability to attract ethical-hacker participation — i.e., what makes a Web3 bounty program "effective" independent of reward size. The authors compiled a dataset of roughly 200 blockchain-related bug bounty programs sourced from HackerOne, Bugcrowd, HackenProof, and Immunefi. For each program they extracted features spanning program-description characteristics (length/wording of key policy sections such as scope and reward tables) and smart-contract-specific characteristics (which Solidity function types were in scope, and whether source code was made publicly viewable to researchers). These features were fed into regression models predicting program effectiveness at drawing hacker engagement. Key finding: both textual presentation of a bounty program and technical scoping choices (source-code visibility, in-scope function types) are significantly associated with how much hacker attention a blockchain bounty program attracts — actionable, addressable design levers distinct from simply raising payouts. Limitations: small sample (~200 programs), short conference-paper format rather than journal depth.
</details>

---

### A Survey of Bug Bounty Programs in Strengthening Cybersecurity and Privacy in the Blockchain Industry
**저자:** Junaid Arshad, Muhammad Talha, Bilal Saleem, Zoha Shah, Huzaifa Zaman (Air University), Zia Muhammad (North Dakota State University)
**게재처:** *Blockchains* (MDPI), Vol. 2, Issue 3, pp. 195–216, 2024
**링크:** https://www.mdpi.com/2813-5288/2/3/10 (오픈액세스, CC BY 4.0)

**핵심 요약:** 블록체인 산업에 특화된 버그바운티 프로그램만 다룬 사실상 유일한 동료심사 서베이 논문. 플랫폼 기반 vs. 기업 자체 운영 프로그램을 비교분석해 각 모델의 장단점과 신뢰도를 정리하고, 트리아지 품질·보상 분쟁 등 구조적 과제와 향후 방향을 제시.

<details><summary>영문 상세 요약</summary>

A dedicated survey/SoK of bug bounty programs specifically in the blockchain industry, explicitly motivated by the authors' observation that "there remains a conspicuous absence of comprehensive research that explores this domain." The paper reviews the bug-bounty ecosystem broadly (citing precedents like "Hack the Pentagon") before narrowing to blockchain-specific platforms, comparing program structures, incentive design, vulnerability types typically surfaced, and the role of ethical hackers. It conducts a comparative analysis of platform-based vs. company-run programs to identify each model's advantages/disadvantages and credibility, closing with recommendations for addressing structural challenges (e.g., triage quality, payout disputes) and future directions.
</details>

---

### Auditing Smart Contracts
**저자:** Wayne R. Landsman (UNC), Evgeny Lyandres (Tel Aviv University), Edward L. Maydew (UNC), Daniel Rabetti (NUS), Che Zhang (Tsinghua University)
**게재처:** SSRN 워킹페이퍼(2025년 10월 개정판), Journal of Accounting and Economics 심사 중으로 추정 — **아직 정식 동료심사 완료 전**
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5198563

**핵심 요약:** ⭐ 이번 조사에서 가장 직접적으로 관련된 논문. "중앙화 감사자"(고정 수수료, 출시 전 1회성 코드 리뷰)와 "탈중앙화 감사자"(=버그바운티 헌터, 출시 후 실운영 환경에서 지속적으로 심각도 기반 보상)를 명시적으로 구분해 경제적 효과를 비교. DeFi 프로토콜 수천 개 + 감사 리포트 약 1만 건 데이터로, 평균적으로는 감사가 향후 침해 가능성을 낮추지 않지만 **최상위 등급의 중앙화 감사와 탈중앙화(버그바운티) 감사는 둘 다 침해 가능성·손실 규모를 낮춘다**는 것을 발견. 침해 이후 개발팀은 상위 등급 감사자로 갈아타고 버그바운티 프로그램 쪽으로도 옮겨가는 경향.

<details><summary>영문 상세 요약</summary>

Explicitly frames and studies the exact economic distinction: "centralized auditors" (hired for a fixed fee, one-time pre-launch code review) versus "decentralized auditors," glossed as "bounty hunters" operating through bug bounty programs that run continuously post-launch and pay based on vulnerability severity. Using nearly 10,000 audit reports from 100+ firms/programs linked to thousands of DeFi protocols (Jan 2020–Jan 2025), the authors find: pre-launch audit adoption correlates with risk-exposed protocol designs; on average audits do not reduce future breach likelihood, but top-tier centralized *and* decentralized/bounty audits specifically are associated with lower breach likelihood and lower losses conditional on a breach; post-breach, developers upgrade to top-tier auditors and pivot toward bounty programs; breached auditors suffer only short-term reputational losses.
</details>

---

### Decentralized Finance (DeFi) assurance: early evidence
**저자:** Thomas Bourveau (Columbia), Janja Brendel, Jordan Schoenfeld
**게재처:** Review of Accounting Studies, 29권 3호, pp. 2209–2253, 2024
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4457936 (SSRN 오픈액세스 워킹페이퍼판)

**핵심 요약:** 스마트컨트랙트 감사 리포트 약 8,500건을 수작업 코딩해 DeFi "어슈어런스" 시장의 등장을 문서화 — 기존 대형 회계법인이 아니라 신생 "기술 감사 전문 업체"가 시장을 장악하고 있고, 감사 리포트 공개가 자본시장에 실제로 긍정적 반응을 일으킴을 입증. **주의:** 버그바운티 vs. 전통 감사를 날카롭게 구분하진 않는, 스마트컨트랙트 감사 시장 전반에 대한 기초 연구.

<details><summary>영문 상세 요약</summary>

Using a hand-coded sample of ~8,500 smart-contract audit reports, this paper documents the emergence of a voluntary "assurance" market for DeFi: audits are pervasive; the auditor market is dominated by new, non-traditional "technical audit firms" rather than incumbent (Big-4-style) financial auditors; audit scope varies widely; and capital markets react positively to report releases. This paper is about the broader voluntary smart-contract-audit-report market as a whole and is not centered on the bug-bounty-vs-traditional-audit distinction specifically — included as foundational background, frequently cited by the more bounty-specific papers above.
</details>

---

### Auditing Decentralized Finance
**저자:** Siddharth Bhambhwani, Allen H. Huang (HKUST)
**게재처:** British Accounting Review, 2024
**링크:** https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4613529

**핵심 요약:** DeFi 프로토콜 316개 분석 — 감사 수·감사 품질이 높을수록 TVL(예치자산)과 토큰 시가총액이 높고, 첫 감사 이후 TVL·토큰가치가 유의미하게 상승하며, 감사 품질이 좋을수록 TerraUSD 붕괴 같은 충격에도 더 견고했음을 발견. **주의:** 버그바운티/탈중앙화 감사자를 별도로 다루지 않음 — 중앙화 감사 자체의 시그널링 가치에 초점.

<details><summary>영문 상세 요약</summary>

Provides what the authors describe as the first empirical evidence on DeFi smart-contract audit services' effect on protocol outcomes. Using data on 316 of the largest DeFi protocols, the study finds protocols vetted by more auditors and higher-quality auditors have higher TVL and higher token market capitalization; an event-study around each protocol's first audit shows TVL and token value increase significantly afterward; better-audited protocols showed more resilience after the TerraUSD collapse shock. Repeated searches turned up no evidence this paper specifically discusses bug bounty programs as a distinct category — included as directly relevant background, not a bug-bounty-specific study.
</details>

---

### The Role of Auditor Reputation in an Emerging Audit Marketplace: Evidence from Decentralized Finance (DeFi)
**저자:** W. Robert Knechel (University of Florida), Steven A. Maex (George Mason University), Hyun Jong Park
**게재처:** Management Science, 2025 (Forthcoming — 3개 독립 출처로 실재 확인)
**링크:** https://pubsonline.informs.org/doi/10.1287/mnsc.2023.02245

**핵심 요약:** ⚠️ 존재·저자·venue는 3개 출처로 교차확인했으나, SSRN·INFORMS 모두 직접 접근이 막혀 원문 초록을 확보하지 못했습니다. 구체적 연구 결과는 다른 논문 요약과 섞여 오염될 위험이 있어 **의도적으로 기재하지 않습니다** — 인용 전 SSRN/INFORMS에서 직접 초록을 확인하세요. (규제 감독이 없는 DeFi 감사 시장에서 "평판"이 품질 신호로 작용하는 방식을 다루는 논문이라는 주제만 확인됨.)

---

### Decentralized Attack Search and the Design of Bug Bounty Schemes
**저자:** Hans Gersbach, Akaki Mamageishvili, Fikri Pitsuwan (ETH Zurich)
**게재처:** 16th International Symposium on Algorithmic Game Theory (SAGT 2023), Springer LNCS (arXiv:2304.00077)
**링크:** https://arxiv.org/abs/2304.00077 (오픈액세스)

**핵심 요약:** 버그바운티를 게임이론적 콘테스트 모델로 정식화 — 탐색비용이 서로 다른 참가자 집단의 균형 탐색 행동을 도출하고, 최적 그룹 크기·전담 전문가 추가 고용 시점·"의도적으로 가짜 버그를 심어 프로그램 무결성을 검증하는" 기법·단일 보상 대신 등급별 다중 보상 구조 설계 등을 분석. 블록체인/인프라 보안을 명시적 동기로 제시하며 Arbitrum 리서치 포럼에도 게시됨 — 다만 모델 자체는 범용적(스마트컨트랙트 전용 아님).

<details><summary>영문 상세 요약</summary>

A game-theoretic/mechanism-design paper building "a simple contest model of bug bounty" in which a group of individuals with heterogeneous search costs is invited to hunt for vulnerabilities in exchange for rewards. The authors characterize equilibrium search behavior and derive an optimal scheme design across several levers: optimal group size, whether/when to additionally hire dedicated experts, inserting "artificial bugs" to calibrate incentives and verify program integrity, and structuring multiple/tiered prizes rather than a single payout. The paper's motivating framing is explicitly infrastructure- and blockchain-security-oriented, and it was subsequently posted to the Arbitrum Research forum. The formal model itself is general-purpose (applicable to any bug bounty context), offered as the strongest available treatment of incentive mechanism design for bug bounty schemes with explicit blockchain motivation.
</details>

---

> **문헌 공백 (정직하게 기록):** "감사 콘테스트"(Code4rena/Sherlock식 시간제한 경쟁형 감사)를 지속형 버그바운티와 구분해서 그 경제성·효과성을 독자적으로 연구한 학술 논문은 이번 조사에서 **찾지 못했습니다** — 관련 자료는 Sherlock/Code4rena 자체 블로그, Medium 포스트, 커뮤니티 위키뿐이었습니다. 블록체인 버그바운티 헌터의 동기부여를 다룬 독립 학술 연구도 없었습니다(Immunefi의 자체 "Hacker Ecosystem Survey"는 업계 설문이라 미포함). 억지로 약한 매칭을 채우지 않고 공백으로 남깁니다.
>
> **제외된 논문(실재하지만 주제 불일치):** 블록체인을 버그바운티 프로그램의 "구현 인프라"로 제안하는 시스템 논문(Badash et al., ACM SAC 2021), SGX 기반 버그 증명 플랫폼 논문(Fukuchi et al., IEEE ICBC 2024), LLM vs 수동 감사 벤치마크(David et al., arXiv:2306.12338), DeFi 공격 SoK(Zhou et al., IEEE S&P 2023 — 버그바운티를 실질적으로 다루지 않음 확인), Code4rena 리포트를 취약점 분류 데이터셋으로만 활용한 논문들 — 전부 실존은 확인했으나 "버그바운티 메커니즘 자체의 경제성/효과성"이라는 기준에 맞지 않아 제외.

---

## 조사 방법 메모

- 1차 라운드: 3개 병렬 리서치 트랙(경제성/정책, 해커 행동/비교연구, 법률/정책/최신동향)이 각각 WebSearch + WebFetch로 원문 게재처(USENIX, ACM DL, Oxford Academic, arXiv, SSRN 등)를 직접 확인 → 28편.
- 2차 라운드: 국내(한국어) 연구 트랙을 RISS/KCI/DBpia/KoreaScience/ScienceON 기준으로 추가 조사 → 9편 추가(총 37편). 같은 2차 라운드에서 시도한 블록체인/스마트컨트랙트 트랙은 세션 사용량 제한으로 중단되어 재시도.
- 3차 라운드(재시도): 블록체인/스마트컨트랙트 버그바운티(Immunefi, Code4rena 등) 트랙 완료 → 7편 추가(총 44편). "감사 콘테스트 모델 자체를 다루는 독립 학술 연구는 존재하지 않는다"는 문헌 공백도 함께 확인·기록.
- 검증 실패했거나 동료심사 상태가 불확실한 논문(예: 일부 블로그 포스트, 포스터 논문, 미확인 학위논문)은 제외했으며, 프리프린트는 본문에 명시적으로 표기함. 국내 연구 조사에서는 1차 출처로 대조되지 않은 4건을 "인용 금지 권장"으로 별도 표시(8장 하단 참고).
- 원 조사에서 저자가 제시한 게재처 정보 중 일부(Kuehn & Mueller의 경우 WEIS→TPRC, Zhao/Laszka/Grossklags의 경우 WEIS→Journal of Information Policy, Walshe & Simpson 2022의 경우 IEEE→Computers & Security)는 교차검증 과정에서 정정됨.

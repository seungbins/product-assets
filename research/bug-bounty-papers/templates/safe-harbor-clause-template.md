# Safe Harbor 조항 템플릿 (초안)

근거: [`../program-improvement-recommendations.md`](../program-improvement-recommendations.md) 4번 항목. Elazari 2019 — 조사 당시 대부분의 버그바운티 프로그램은 "안전하다"고 홍보하면서도 실제로는 모호한 문구로 법적 리스크를 헌터에게 떠넘기고 있었음. 아래는 [disclose.io](https://disclose.io)류의 표준 safe harbor 접근 방식을 참고한 **초안**입니다.

> ⚠️ **이 문서는 법률 자문이 아닙니다.** 실제 정책에 게시하기 전 반드시 변호사 검토를 받으세요. 관할권(국가/주)에 따라 CFAA(미국) 대응 조항, 개인정보보호법(GDPR 등), 국내 정보통신망법·개인정보보호법 등 적용 법령이 달라집니다.
>
> 🔴 **필수 입력**: 아래 문구의 "we/our"를 실제 서비스 제공 주체(개인/법인명)로 바꿔야 합니다 — 이 저장소에 법인명/사업자 정보가 없어 제가 대신 채울 수 없습니다. 그 외 문구 자체는 disclose.io 표준 구조를 따른 완성된 초안이라 그대로 사용 가능합니다.

---

## 초안 문구 (영문, disclose.io 스타일)

```
Safe Harbor

We consider security research and vulnerability disclosure activities conducted
consistent with this policy to be:

- Authorized in view of any applicable anti-hacking laws, and we will not
  initiate or support legal action against you for accidental, good-faith
  violations of this policy;
- Exempt from restrictions in our Terms of Service that would interfere with
  conducting security research, and we waive those restrictions on a limited
  basis for work done under this policy;
- Lawful, helpful to the overall security of the Internet, and conducted in
  good faith.

You are expected, as always, to comply with all applicable laws. If legal
action is initiated by a third party against you and you have complied with
this policy, we will take steps to make it known that your actions were
conducted in compliance with this policy.

This policy applies only to testing activity that falls within the scope
defined in [scope-template.md], conducted without:
- accessing, modifying, or exfiltrating data beyond what is necessary to
  demonstrate the vulnerability;
- degrading service availability for other users;
- social engineering, phishing, or physical attacks against our staff or
  facilities.
```

## 체크리스트 (Elazari 2019가 지적한 "가짜 safe harbor" 흔한 함정)

- [ ] "선의(good faith)"의 정의가 구체적으로 명시되어 있는가, 아니면 회사가 자의적으로 판단할 수 있게 모호하게 남겨뒀는가?
- [ ] 회사가 "권리를 유보한다(reserve the right to pursue legal action)"는 식의 상충 문구가 다른 곳에 숨어있지 않은가?
- [ ] 스코프 밖 테스트에 대해서도 "선의였다면" 최소한의 보호를 제공하는가, 아니면 스코프를 1mm만 벗어나도 보호가 완전히 사라지는가?
- [ ] 실제 법무팀이 검토했는가, 아니면 마케팅/보안팀이 단독으로 작성했는가?

*이 초안은 연구 종합 결과이며, 게시 전 반드시 법무 검토를 받으세요.*

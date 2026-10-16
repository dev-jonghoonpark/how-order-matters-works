# How Order Matters Works

**Order Matters — 집합을 위한 seq2seq.** Vinyals, Bengio & Kudlur의 *Order Matters: Sequence to Sequence for Sets* (ICLR 2016)를 브라우저에서 직접 실험하며 읽는 인터랙티브 교육 자료입니다. 체인 룰은 어떤 순서로 풀어도 같은 확률을 주는데 왜 순서를 바꾸면 성능이 달라지는지, 순서가 없는 입력은 어떻게 읽고 순서가 없는 출력은 어떻게 내보내는지를 다룹니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-order-matters-works/)**

## 다루는 내용

1. **체인 룰은 순서를 가리지 않는다** · 같은 숫자 다섯 개를 순서만 바꿔 RNN에 넣으면 마지막 상태가 달라지고, 임베딩 합은 그대로인 실험
2. **그런데 입력 순서는 중요했다** · 번역 입력 뒤집기 BLEU +5.0, 파싱 F1 +0.5%p, 볼록 껍질 각도순 정렬 최대 +10%p. 번호만 각도순으로 다시 매기면 정답 출력이 오름차순이 되는 볼록 껍질 데모
3. **합의 한계** · 순열 불변이지만 원소 수와 무관한 고정 차원
4. **Read · Process · Write** · 식 (3)–(7)을 그대로 구현한 Process 블록. 메모리를 섞어도 q\*<sub>T</sub> 차이가 반올림 오차(~1e-16) 수준인 것을 RNN 인코더와 나란히 비교, 포인터 네트워크와 glimpse
5. **정렬 실험 (표 1)** · N = 5/10/15, 처리 스텝 P, glimpse 유무별 정확도. P = 0이 Ptr-Net보다 못한 이유, N이 커질 때 p<sup>N</sup>과 "가장 가까운 두 수의 간격"으로 보는 급락
6. **출력 순서도 중요하다** · PTB 언어 모델 순방향·역방향 86 vs 3단어 뒤집기 96, 파스 트리 깊이 우선 89.5% vs 너비 우선 81.5%, n!개 정답 동치류
7. **별 모양 그래피컬 모델** · 결합분포를 전부 나열해 정확히 계산한 스텝별 조건부 엔트로피 — 합은 같고 조건부의 복잡도가 다르다
8. **학습하면서 순서 찾기 (식 9)** · 균등 사전학습 + p(Y<sub>π</sub>|X)에 비례한 샘플링, 5-gram 실험(표 2). 120가지 순서의 확률을 전부 계산해 max 탐색과 조상 샘플링을 비교하는 데모
9. **그 뒤의 이야기** · Deep Sets, Set Transformer, DETR의 헝가리안 매칭
10. **퀴즈** 6문항

표 1·표 2와 본문 수치는 논문에서 그대로 옮겼습니다. 데모는 모두 브라우저가 실제로 계산하지만, 가중치는 무작위로 고정했거나 손으로 정한 값이며 학습된 모델이 아닙니다.

## 참고

- Vinyals, Bengio & Kudlur (2016), *Order Matters: Sequence to Sequence for Sets* — [arXiv:1511.06391](https://arxiv.org/abs/1511.06391)
- Vinyals, Fortunato & Jaitly (2015), *Pointer Networks* — [arXiv:1506.03134](https://arxiv.org/abs/1506.03134)
- Sutskever, Vinyals & Le (2014), *Sequence to Sequence Learning with Neural Networks* — [arXiv:1409.3215](https://arxiv.org/abs/1409.3215)

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.

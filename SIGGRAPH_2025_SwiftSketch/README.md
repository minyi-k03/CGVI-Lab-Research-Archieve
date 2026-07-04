# SwiftSketch (SIGGRAPH 2025)

* **Full Title:** SwiftSketch: One-Second High-Quality Image-to-Vector Sketching
* **Conference:** SIGGRAPH 2025
* **Materials:** [서베이 PPT (PDF 변환본)](./docs/SwiftSketch-Paper-Survey.pdf)
* **Official Paper:** [저자 논문 링크 혹은 DOI 적기]
* **Official Code:** (https://github.com/swiftsketch/SwiftSketch)

---

## 1. Motivation (연구 배경)
* 기존의 Image-to-Vector(이미지를 벡터 스케치로 변환) 연구들은 생성 속도가 느려 실시간 응용에 한계가 있었음.
* 고품질의 스케치를 유지하면서도 1초 미만의 빠른 추론 속도를 달성하고자 본 연구가 제안됨.

## 2. Key Contribution (핵심 기여도)
* **High Speed & Quality:** 1초 이내로 고품질의 벡터 스케치 생성 가능.
* **Architecture:** Stroke control point를 점진적으로 디노이징하는 Transformer-decoder 기반 아키텍처 도입.
* **Dataset:** 기존 스케치 데이터셋의 한계를 극복하기 위해 Depth-aware ControlNet을 활용한 `ControlSketch` 합성 데이터셋 구축 및 활용.

## 3. Methodology (제안 방법론 요약)
* *PPT 장표 내용을 바탕으로 핵심 아키텍처나 파이프라인 흐름을 간단히 줄글이나 불릿포인트로 요약하여 작성하세요.*

## 4. My Thoughts & Lab Focus (개인 견해 및 랩실 연구 연계)
* *이 논문을 서베이하며 느낀 한계점이나, 우리 랩실의 연구 방향(혹은 캡스톤 디자인)에 어떻게 적용할 수 있을지 주관적인 인사이트를 적어줍니다.*

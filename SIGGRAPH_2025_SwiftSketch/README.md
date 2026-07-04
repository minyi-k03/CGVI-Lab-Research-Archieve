# SwiftSketch (SIGGRAPH 2025)

* **Full Title:** SwiftSketch: A Diffusion Model for Image-to-Vector Sketch Generation
* **Authors:** Ellie Arar, Yarden Frenkel, Daniel Cohen-Or, Ariel Shamir, Yael Vinker
* **Conference:** SIGGRAPH 2025
* **Materials:** [서베이 PPT (PDF 변환본)](./docs/SwiftSketch-Paper-Survey.pdf)
* **Official Paper:** https://doi.org/10.1145/3721238.3730612

---

## 1. Motivation (연구 배경)
* 기존의 VLM(Vision-Language Model) 기반 고품질 벡터 스케치 생성 방식들은 반복적인 최적화(backpropagation) 과정에 의존하기 때문에 스케치 한 장을 생성하는 데 수 분 이상이 소요됨.
* 이로 인해 대화형(interactive) 애플리케이션이나 대규모 스케치 데이터 생성 작업에 적용하기에는 비실용적이라는 치명적인 한계가 존재함.

## 2. Key Contribution (핵심 기여도)
* **ControlSketch & Dataset:** 기존 텍스트 조건부 SDS Loss에 Depth ControlNet을 결합한 `ControlSketch`라는 최적화 기반 기법을 제안하였으며, 이를 활용해 100개 클래스에 걸친 35,000개 이상의 고품질 합성 데이터셋(Image-Sketch pairs)을 구축함.
* **SwiftSketch Model:** 벡터 표현의 이산적인(discrete) 특성을 다루기 위해 스트로크 제어점 공간에서 가우시안 노이즈를 점진적으로 제거하는 Transformer-decoder 기반의 디퓨전 모델을 제안함.
* **Fast Generation:** 10분 가까이 걸리던 기존 최적화 방식의 데이터 분포를 학습하여, 스케치당 약 0.5초의 추론 속도를 달성함. 이는 완벽한 실시간은 아니나, 실시간 대화형 처리를 향한 의미 있는 진전(step toward real-time)임.

## 3. Methodology (제안 방법론 요약)
1. **Feature Extraction:** 사전 학습된 CLIP 이미지 인코더(ResNet)를 사용하여 입력 이미지에서 기하학적, 의미론적 특징(Image Embedding)을 추출함.
2. **Denoising Process:** 추출된 이미지 임베딩과 타임스텝을 교차 주의(Cross-attention) 메커니즘을 통해 Transformer-decoder에 전달하여 32개의 스트로크 좌표 노이즈를 제거함.
3. **Training Objective:** 제어점 간의 L1 거리인 ($$\mathcal{L} _ {points}$$)와 래스터화(Rasterized)된 스케치 이미지 간의 LPIPS 거리인 ($$\mathcal{L}_{raster}$$)를 함께 사용하여 정밀도와 전체적인 구조적 유사성을 동시에 학습함.
4. **Refinement Stage:** 추론 마지막 단계에서 남아있는 미세한 노이즈를 제거하기 위해, 파라미터가 미세 조정된 복제 네트워크($$M_{\theta^+}$$)를 통해 한 번 더 정제 과정을 거침.

## 4. Limitations & Future Work (한계점 및 향후 연구)
* 학습 데이터에 포함되지 않은 카테고리(Unseen categories)의 이미지가 입력될 경우, 스케치가 노이즈처럼 보이거나 인식하기 어려운 형태로 생성되는 등 일반화(Generalization) 성능 저하가 발생함.
* 미세 노이즈를 지우기 위한 Refinement 단계가 오히려 눈, 코 등 객체의 세밀한 디테일까지 과도하게 단순화(over-simplify)하여 지워버리는 문제가 있음.
* 현재는 32개의 고정된 스트로크 수만 지원하지만, 향후 사용자가 원하는 다양한 수준의 추상화(Levels of abstraction)를 위해 가변적인 스트로크 생성을 지원하는 것이 목표임.

## 5. My Thoughts (개인 견해 및 랩실 연계 포인트)
* *(이곳에 랩실 포팅 과정에서 겪은 어려움이나 인사이트를 작성합니다.)*
* *(예시: 논문의 한계점에서 언급된 Unseen 데이터 성능 저하 현상을 실제 코드를 돌려보며 확인하였음. 이를 개선하기 위해...)*

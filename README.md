# 한국어 문서요약 경진대회
## 6조 KeepGoing!!!

| ![박패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![최패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![김패캠](https://avatars.githubusercontent.com/u/156163982?v=4) | ![오패캠](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [문서연](https://github.com/UpstageAILab)             |            [김수현](https://github.com/UpstageAILab)             |            [오정택](https://github.com/UpstageAILab)             |            [이승호](https://github.com/UpstageAILab)             |            [최현](https://github.com/UpstageAILab)             |
|                            팀장, 실험 총괄                           |                            Bart 연구                            |                            T5 연구                             |                            LLM 연구                             |                            파인튜닝 연구                             |

## 0. Overview
### Environment
GPU engine: RTX 3090

### Requirements
Core ML/DL Libraries
torch==2.9.1
transformers==4.57.1
datasets==4.4.1
accelerate==1.11.0
tokenizers==0.22.1
tiktoken==0.12.0
sentencepiece==0.2.1
safetensors==0.6.2

NLP & Evaluation
rouge-score==0.1.2
nltk==3.9.2
konlpy==0.6.0

Data Processing
pandas==2.3.3
numpy==2.2.6
scikit-learn==1.7.2
scipy==1.15.3

Visualization
matplotlib==3.10.7
seaborn==0.13.2

Jupyter & Development
jupyter==1.1.1
jupyterlab==4.4.10
ipykernel==7.1.0
ipython==8.37.0
notebook==7.4.7

Utilities
tqdm==4.67.1
pyyaml==6.0.3
requests==2.32.5


## 1. Competiton Info

### Overview

- 본 대회는 회의, 일상 대화 등 다양한 주제의 대화문을 효과적으로 요약하는 모델을 개발하는 대회입니다. 참가자들은 제공된 대화문-요약문 쌍 데이터셋을 활용하여 모델을 학습시키고, 249개의 테스트 대화문에 대한 요약문을 생성하여 제출합니다. 평가는 ROUGE 지표를 기반으로 생성된 요약문의 품질을 측정합니다.

### Timeline

- ex) November 29, 2025 - Start Date
- ex) December 9, 2025 - Final submission deadline

## 2. Components

### Directory

<img width="439" height="224" alt="image" src="https://github.com/user-attachments/assets/3574e96e-a42b-4fdd-ace5-479e9b71f04b" />



## 3. Data descrption

### Dataset overview

데이터셋은 학교 생활, 직장, 의료 상담, 쇼핑, 여가, 여행 등 30개 주제의 일상 대화와 이에 대한 요약문 쌍으로 구성되어 있습니다. 학습 데이터 약 12,000개, 검증 데이터 약 500개, 테스트 데이터 249개로 구성되며, 대화는 #Person1#, #Person2# 형식의 화자 태그로 구분됩니다. 요약문은 원본 대화의 약 20% 길이로, 핵심 내용을 간결하게 담고 있습니다.

### EDA

<img width="336" height="637" alt="image" src="https://github.com/user-attachments/assets/2a0a7676-fe92-4290-88d0-1ceb9b1b033c" />
<img width="456" height="451" alt="image" src="https://github.com/user-attachments/assets/36c746fd-decc-4f45-92d6-7f2c8c4d855c" />



### Data Processing

속어, 은어, 반복어가 거의 없어 전처리는 따로 수행하지 않았습니다.

## 4. Modeling

### Model descrition

KoBART는 한국어 요약에 특화된 Encoder-Decoder 구조로, mT5나 KE-T5 대비 가볍고 빠르면서도 ROUGE 성능이 우수합니다. 특히 digit82/kobart-summarization은 이미 요약 태스크로 사전학습되어 있어 fine-tuning 효율이 높아 선택하게 되었습니다.

### Modeling Process

베이스라인으로 digit82/kobart-summarization 모델을 선정한 후, R-Drop(alpha=5.0) 정규화 기법을 적용하여 일반화 성능을 향상시켰습니다. 추론 단계에서는 beam search 크기를 56으로, max_length를 82로 체계적으로 튜닝하여 최적의 생성 파라미터를 찾았습니다. 마지막으로 Solar API를 활용하여 잘린 문장을 자연스럽게 완성하는 후처리를 적용해 최종 성능을 개선했습니다.

<img width="1372" height="1152" alt="image" src="https://github.com/user-attachments/assets/4aa9591f-0c1d-4544-a88d-e9d12efefb96" />

<img width="2528" height="1752" alt="image" src="https://github.com/user-attachments/assets/fef33e49-f693-4156-8dc2-bd10e731d526" />


## 5. Result

### Leader Board

<img width="986" height="142" alt="image" src="https://github.com/user-attachments/assets/54ed833e-3682-4aa3-b0fc-af862c96e1f1" />
final result 47.2800 총 3위

### Presentation

[nlp_6_presentation.pdf](https://github.com/user-attachments/files/24055252/nlp_6_presentation.pdf)

## etc

### Reference

- Chen, Y., et al. (2021). DialogSum: A Real-Life Scenario Dialogue Summarization Dataset. ACL 2021.
- Liu, Y., & Liu, P. (2021). SimCLS: A Simple Framework for Contrastive Learning of Abstractive Summarization. ACL 2021.
- Wu, L., et al. (2021). R-Drop: Regularized Dropout for Neural Networks. NeurIPS 2021.


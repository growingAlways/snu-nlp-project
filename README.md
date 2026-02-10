# Automatic Data Pipeline Agent (LLM-based ETL)

## 📖 Overview
**Automatic Data Pipeline Agent**는 비정형 텍스트(이메일, 보고서, 로그 등)를 분석하여 사용자가 정의한 데이터베이스 스키마(RDB, VectorDB)에 맞춰 **자동으로 정형 데이터를 추출하고 분류하는 AI 에이전트**입니다.

단순한 추출을 넘어, **CoT(Chain of Thought)** 방식의 추론과 **Review(Self-Correction)** 모드를 결합하여 데이터 분류의 정확도와 추출 품질을 극대화했습니다. 특히 스키마가 변경되어도 프롬프트 수정 없이 작동하는 **Dynamic Schema Matching** 로직이 적용되어 있습니다.

## ✨ Key Features
* **Dual-Mode Architecture**:
    * **CoT Mode (Senior Engineer)**: 데이터의 형태와 내용을 분석하여 1차 분류 및 추출 수행.
    * **Review Mode (Lead Architect)**: 1차 결과를 검증하고, 놓친 데이터를 복구(Repair)하거나 잘못된 분류를 수정(Override).
* **Dynamic Schema Matching**: 하드코딩된 프롬프트 없이, `schema_metadata`에 정의된 테이블 정보를 동적으로 읽어들여 매핑합니다.
* **Intelligent Validation Logic**:
    * **Data Shape Check**: 텍스트에 포함된 구체적인 값(Column Value)을 기반으로 RDB와 VectorDB를 구분.
    * **Semantic Type Check**: 문서의 의도(Spec vs Issue vs Plan)를 파악하여 테이블 오분류 방지.
* **Automated Evaluation**: Precision, Recall, F1-Score 및 데이터 추출 정확도(Extraction Score) 자동 산출 및 시각화.

## 📂 Repository Structure

```bash
├── Automatic Data Pipeline Agent.ipynb  # 메인 실행 노트북 (Agent 로직, 평가, 시각화 포함)
├── dataset/                             # 평가용 데이터셋 폴더
│   ├── tb_sales_performance.csv
│   ├── tb_product_spec.csv
│   ├── vec_dev_issues.csv
│   ├── vec_sales_strategy.csv
│   └── ... (기타 도메인별 CSV 파일)
└── README.md                            # 프로젝트 설명 문서

🛠️ Prerequisites & Installation
이 프로젝트는 Google Colab 환경에서 실행하는 것을 권장합니다. 로컬 환경에서 실행할 경우 아래 라이브러리가 필요합니다.

Required Libraries
pandas

numpy

scikit-learn

tqdm

matplotlib, seaborn

torch (LLM 모델 로딩용)

transformers (또는 사용하는 LLM API 클라이언트)

🚀 How to Run
[Google Colab (Recommended)]
1. 이 저장소의 .ipynb 파일을 Colab에서 엽니다.
2. 좌측 파일 탐색기 영역에 dataset 폴더를 생성하고, 저장소의 dataset/ 폴더 내 모든 CSV 파일들을 업로드합니다.
   경로 예시: /content/dataset/tb_sales_performance.csv
3. Model Loading 셀에서 사용할 LLM(Gemini, Llama 등)과 Tokenizer를 로드합니다. (API Key가 필요한 경우 설정 필수)
4. 노트북의 모든 셀을 순차적으로 실행합니다.

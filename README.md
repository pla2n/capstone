# 📄 논문 요약 및 시각화를 위한 마인드맵 기반 인터페이스

**(Mind Map-based Interface for Paper Summarization and Visualization)**

> **arXiv 논문의 복잡한 내용을 섹션별로 요약하고, 이를 마인드맵으로 시각화하여 연구자들의 이해를 돕는 지능형 인터페이스입니다.**

## 📌 프로젝트 소개 (Introduction)

현대 학술 연구의 양적 팽창으로 인해 연구자들이 읽어야 할 논문의 양은 급증하고 있습니다. [cite_start]하지만 전문적이고 복잡한 논문의 특성상, 텍스트만으로는 핵심 내용과 논리적 구조를 빠르게 파악하기 어렵습니다[cite: 1698, 1708].

[cite_start]본 프로젝트는 이러한 문제를 해결하기 위해 \*\*LLM(Llama-3.2-3B)\*\*을 활용하여 arXiv 논문의 섹션별 핵심 내용을 요약하고, 이를 **트리 구조의 마인드맵**으로 자동 변환하여 시각화하는 시스템을 제안합니다[cite: 1701]. [cite_start]사용자는 이를 통해 논문의 전체 흐름을 한눈에 파악하고, 인터랙티브한 마인드맵을 통해 능동적으로 지식을 습득할 수 있습니다[cite: 1704, 1717].

## ✨ 주요 기능 (Key Features)

  * [cite_start]**arXiv 논문 자동 크롤링 & 파싱**: 사용자가 입력한 arXiv URL에서 논문 제목, 섹션(Header), 본문 내용을 자동으로 추출하고 구조화합니다[cite: 1774].
  * [cite_start]**섹션별 지능형 요약**: 미세 조정(Fine-tuned)된 **Llama-3.2-3B** 모델을 사용하여 각 섹션의 내용을 문맥에 맞게 요약합니다[cite: 1702].
  * [cite_start]**마인드맵 자동 생성**: 생성된 요약문을 계층적 트리 구조(Markdown 기반)로 변환하여 직관적인 마인드맵으로 시각화합니다[cite: 1857].
  * [cite_start]**인터랙티브 UI**: 사용자가 마인드맵의 노드와 연결선을 자유롭게 드래그(Drag & Drop)하여 배치를 수정할 수 있어, 종이에 그리는 듯한 경험을 제공합니다[cite: 1717, 2221].

## 🛠 기술 스택 (Tech Stack)

[cite_start]논문의 **표 1. 플랫폼 정보** [cite: 1872]에 기반한 개발 환경 및 라이브러리입니다.

| Category | Technology |
| --- | --- |
| **Model** | [cite_start]**Llama-3.2-3B-Instruct** (Fine-tuned with **LoRA**) [cite: 1869] |
| **Backend** | **Python 3.12.4**, **Flask 3.0.3** |
| **ML/DL Framework** | **PyTorch 2.5.0**, **Transformers 4.42.3**, **PEFT 0.12.0** |
| **Web Crawling** | **BeautifulSoup4 4.12.3** |
| **Frontend** | **HTML**, **JavaScript** (LeaderLine 1.0.3 for connections) |
| **Hardware** | [cite_start]H100 (VRAM 80GB) [cite: 1868] |
| **OS** | Ubuntu 22.04 LTS, CUDA 12.2 |

## 🏗 시스템 구조 (System Architecture)

[cite_start]본 시스템의 전체적인 동작 과정은 다음과 같습니다[cite: 1768, 1770]:

1.  **Input**: 사용자가 arXiv 논문 URL 입력
2.  [cite_start]**Crawling**: `BeautifulSoup`을 이용해 논문의 HTML 구조(`<h1>`\~`<h6>`, `<p>`)를 분석하여 텍스트 추출[cite: 1807].
3.  [cite_start]**Summarization**: 추출된 텍스트를 섹션별로 분할하여 **Llama-3.2-3B** 모델에 입력, 프롬프트 엔지니어링을 통해 요약문 생성[cite: 1824].
4.  [cite_start]**Structure Gen**: 요약된 내용을 계층 구조를 가진 Markdown 파일로 변환[cite: 1861].
5.  [cite_start]**Visualization**: Markdown 파일을 파싱하여 웹 상에 노드(Node)와 연결선(LeaderLine)으로 렌더링[cite: 2177].

## 📊 성능 평가 (Performance)

[cite_start]`ccdv/arxiv-summarization` 데이터셋을 활용하여 성능을 평가하였으며, 기존 모델 대비 우수한 요약 성능을 기록했습니다[cite: 2261].

  * [cite_start]**ROUGE-L Score**: **47.00** (기존 SOTA 모델 대비 **+5.23점** 향상)[cite: 1703, 2262].
  * **ROUGE-1**: 58.00
  * **ROUGE-2**: 28.00

> [cite_start]**Note**: LoRA(Low-Rank Adaptation) 기법을 적용하여 적은 파라미터로 효율적인 미세 조정을 수행했습니다[cite: 1869].

## 🚀 설치 및 실행 (Getting Started)

*(논문의 라이브러리 정보를 기반으로 추론한 실행 가이드입니다.)*

1.  **Repository Clone**

    ```bash
    git clone https://github.com/pla2n/capstone.git
    cd capstone
    ```

2.  **Install Dependencies**

    ```bash
    pip install flask torch transformers peft beautifulsoup4
    ```

3.  **Run Application**

    ```bash
    python app.py
    ```

4.  **Usage**

      * 웹 브라우저에서 `http://localhost:5000` 접속
      * 요약하고자 하는 arXiv 논문의 URL 입력
      * 'Generate Mindmap' 버튼 클릭

## 👥 팀원 (Authors)

  * **이세용 (Se-yong Lee)** - rred5899@yu.ac.kr
  * **최정민 (Jeong-min Choi)** - snapflip20@gmail.com
-----

*이 프로젝트는 2025년 영남대학교 정보통신공학과 졸업논문 프로젝트의 일환으로 개발되었습니다.*

# ■ Korean Retrieval-Augmented Question Answering System 
- 이 프로젝트는 한국어 위키백과 문서를 기반으로 하는 Retrieval-Augmented QA 시스템을 구축하는 것을 목표로 하였습니다.
  여러 LangChain 모듈과 Hugging Face 모델 및 도구를 사용하여, 한국어 질문에 대해 적절한 문맥에서 답변을 생성할 수 있도록 하였습니다.

## ■ 개요
- 주어진 한국어 질문에 대해 관련 문서(위키백과 등)에서 정보를 검색하고, 검색된 문맥을 기반으로 정확한 단답형 답변을 생성하는 시스템 구현

## ■ 기술 스택 
- LangChain, Hugging Face Transformers, Chromadb, Python, BeautifulSoup

 ## ■ 사용된 모델 및 구성 요소
 - 임베딩 : 모델: jhgan/ko-sroberta-multitask ( 문서(예: 위키 문서)의 내용을 벡터화하여, 질문에 대해 관련 문서를 retrieval 하는 데 사용 )
 - LLM : 


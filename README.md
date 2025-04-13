# ■ Retrieval-Augmented QA System
- 한국어 위키백과 문서를 기반으로 질문에 대해 관련 문맥을 찾아내고, 해당 문맥에서 정형화된 단답형 응답을 생성하는 Retrieval-Augmented QA 시스템을 구축하는 것을 목표하며
  LangChain, Hugging Face Transformers, 그리고 Chroma 벡터스토어를 이용하여 아래와 같이 구성됩니다.
  <br>
  
 ## ■ 모델 및 구성 요소
 - 임베딩 : 모델: jhgan/ko-sroberta-multitask ( 문서(예: 위키 문서)의 내용을 벡터화하여, 질문에 대해 관련 문서를 retrieval 하는 데 사용 )
 - LLM : paust/pko-t5-base (입력된 질문과 문맥을 인코더에서 처리한 후, 디코더에서 정형화된 단답형 응답 생성)
 - 벡터스토어 : Chroma (분할된 문서를 임베딩 벡터 형태로 저장하여, 사용자 질문에 맞는 관련 문서를 빠르게 검색)
 <br>
 ## ■ 구현 과정 
 - 문서 크롤링 및 전처리 > 벡터스토어 구축 >  LLM 파이프라인 구성 > Retrieval QA 체인 구성 및 프롬프트 설계

 <br>
 

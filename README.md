# ■ Use-langchain-RAG
- 한국어 위키백과 문서를 기반으로 질문에 대해 관련 문맥을 찾아내고, 해당 문맥에서 정형화된 단답형 응답을 생성하는 Retrieval-Augmented QA 시스템을 구축하는 것을
  목표하였으며 LangChain, Hugging Face Transformers, 그리고 Chroma 벡터스토어를 이용하여 아래와 같이 챗봇을 구현하였습니다. 
  <br>
  
## ■ 모델 및 구성 요소
 - 임베딩 : 모델: jhgan/ko-sroberta-multitask ( 문서(예: 위키 문서)의 내용을 벡터화하여, 질문에 대해 관련 문서를 retrieval 하는 데 사용 )
 - LLM : paust/pko-t5-base (입력된 질문과 문맥을 인코더에서 처리한 후, 디코더에서 정형화된 단답형 응답 생성)
 - 벡터스토어 : Chroma (분할된 문서를 임베딩 벡터 형태로 저장하여, 사용자 질문에 맞는 관련 문서를 빠르게 검색)
 <br>
 
## ■ 구현 과정 
 - 문서 크롤링 및 전처리 > 벡터스토어 구축 >  LLM 파이프라인 구성 > Retrieval QA 체인 구성 및 프롬프트 설계

![image](https://github.com/user-attachments/assets/0a317c6f-2ed5-454e-9f7c-c5c85bc1d598)
 <br>

 ## ■ 모델 장점 및 단점 
 - yjgwak/klue-bert-base-finetuned-squard-kor-v1 (BERT 기반의 Encoder‑only 모델)

   - 장점 : Extractive QA에 최적화
   - 단점 : 자유로운 텍스트 생성을 지원하지 않음, 기 존재하는 문구를 선택하여 자연스런운 질의 응답에 형태를 지원하지 않음
  
- paust/pko-t5-base (T5 계열의 Encoder-Decoder 모델) 

  - 장점 : 프롬프트에 흐름에 따라 답변이 생성됨
  - 단점 : 문서 기반에 흐름을 원활하게 읽지 못해 답변에 한계가 있음
 
- skt/kogpt2-base-v2 (GPT2 기반의 Decoder‑only 모델)

   - 장점 : 자유로운 텍스트 생성에 강점이 있으며, 창의적이고 자연스러운 문장 완성이 가능함
   - 단점 : retrieval된 문맥에서 정확한 정보(예: “출연 여부”, “연출 담당자” 등)를 추출하기 어렵고, 프롬프트에 따라 엉뚱한 텍스트 생성함
 
- MBZUAI/LaMini-Flan-T5-248M (경량 T5 모델)

   - 장점 : 경량화된 모델로, 속도와 효율성 좋음
   - 단점 : 한글에 대한 문맥 해석이 많이 떨어짐, 정확도를 내기 어려움
 

요약 : 총 4개의 모델를 비교하여 테스트한 결과 가장 답변이 잘된 모델은 klue-bert 모델인 것으로 확인했으며, 간결한 답변이지만 
        QA에 특화되어 있어 문맥을 정확하게 추출하는 것으로 아래의 이미지를 통해 확인 가능했습니다. 

![image](https://github.com/user-attachments/assets/146bf89d-bd39-439b-bf70-71259cde7fb6)
![image](https://github.com/user-attachments/assets/eb8cfd8e-6417-4dd6-b81b-8b5028399eda)
![image](https://github.com/user-attachments/assets/a87a5ef4-684e-48cf-8de7-a7ab7b439cd9)

최종적으로 질문에 대한 문맥을 기반하여 정형화된 단답형 응답을 목표로 할 때, QA 전용 모델이 가장 좋은 결과를 보여준 것을 확인하였으며 
생성형 모델들은 자유로운 텍스트 생성에는 유리하지만, 대부분의 모델이 영어 기반으로 학습되어 한글 문맥을 정확하게 파악하기 어려워 답변에 
한계가 있는 것으로 확인하였습니다. 

앞으로 계획은 조금 더 다양한 모델을 분석하여 단답형 보단, 질의 응답의 자유로운 형태 답변이 진행될 수 있도록 연구할 예정이며 
LangChain 에이전트 모듈을 활용해 Retrieval QA 체인을 도구로 등록하고, 복합적인 사용자 질의에 대응하는 에이전트 시스템 구축할 예정입니다. 


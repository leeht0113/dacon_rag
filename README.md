# dacon_rag
* 단순한 구조의 Naive RAG, Advanced RAG(Ensemble Retriever, Reranker)와 같은 구조로 성능 실험
* 문서 source 별로 VectorDB를 달리하여 각 source에 해당하는 VectorDB를 활용하게 함
* Train data의 Question-Answer만 QLoRA로 학습한 Gemma와 RAG의 prompt 구조를 가진 Context-Question-Answer 구조로 QLoRA로 학습한 Gemma에 대한 성능 비교 분석함 
* Train data의 Question-Answer만 QLoRA finetuning한 Gemma 모델로 Advanced RAG를 가진 질의응답 모델이 제일 성능이 좋게 나옴


|활용 LLM|finetuning 여부|Document Loader|RAG 구조|F1-Score 성능|
|--------|--------------|---------------|--------|-------------|
|rtzr/ko-gemma-2-9b-it|Train data의 Q&A를 QLoRA로 finetune|pymupdf4llm|MultiVectorDB, Reranker|0.6748 (최종 순위 32위)|
|rtzr/ko-gemma-2-9b-it|X|pymupdf4llm|MultiVectorDB, Reranker|0.66795|
|rtzr/ko-gemma-2-9b-it|X|PDFPlumberLoader|MultiVectorDB, Reranker|0.6317|
|rtzr/ko-gemma-2-9b-it|X|pymupdf4llm|MultiVectorDB,Ensemble Retriever(BM25Retriever, VectorStore-Backend Retriever)|0.6286|
|rtzr/ko-gemma-2-9b-it|X|pymupdf4llm|MultiVectorDB,VectorStore-Backend Retriever|0.6286|
|rtzr/ko-gemma-2-9b-it|Train data를 RAG Prompt 구조로 QLoRA finetune|pymupdf4llm|MultiVectorDB, Reranker|0.5941|
|EEVE-Korean-10.8B(ChatOllama)|X|PDFMinerLoader|Naive Rag|0.2759|
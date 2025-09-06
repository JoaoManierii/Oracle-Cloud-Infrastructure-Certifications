# Oracle Cloud Infrastructure AI Foundations – Resumo de Estudos.

<div align="center"><img src="slides/disclaimer.png" alt="SaaS" width="600" height="300" /></div>

## 1. Init 
A certificação **OCI AI Foundations** da Oracle tem como objetivo validar os conhecimentos fundamentais em Inteligência Artificial (IA) e sua aplicação dentro do portfólio de serviços da Oracle Cloud Infrastructure. A prova aborda desde os conceitos básicos de IA, aprendizado de máquina (ML) e aprendizado profundo (DL), até tópicos relacionados a modelos generativos e grandes modelos de linguagem (LLMs). Essa certificação é importante porque a IA se tornou essencial para acelerar a inovação em empresas de todos os setores, permitindo automação de processos, análise de grandes volumes de dados, personalização de experiências e suporte a tomadas de decisão mais assertivas. Ao compreender os fundamentos e as soluções de IA disponíveis no ecossistema OCI, o profissional se capacita a aplicar a tecnologia de forma estratégica, explorando todo o potencial da nuvem da Oracle para gerar valor real nos negócios.

## 2. AI Foudnations

**Discuss AI Basics**  
Inteligência Artificial (IA) é um campo da ciência da computação que busca desenvolver sistemas capazes de realizar tarefas que normalmente exigiriam inteligência humana, como reconhecimento de padrões, tomada de decisão e compreensão de linguagem natural. Os conceitos básicos envolvem a capacidade das máquinas de aprender com dados, melhorar com a experiência e simular processos cognitivos, criando soluções mais eficientes e escaláveis.

**Discuss AI Applications & Types of Data**  
As aplicações de IA estão presentes em diversas áreas, desde assistentes virtuais e sistemas de recomendação até diagnósticos médicos e veículos autônomos. Esses sistemas dependem de diferentes tipos de dados, como estruturados (bancos de dados organizados), não estruturados (textos, imagens, áudios) e semiestruturados (logs, arquivos JSON ou XML). A qualidade e a diversidade dos dados são fundamentais para o desempenho dos modelos de IA.

**Explain AI vs ML vs DL**  
Embora muitas vezes usados como sinônimos, IA, ML e DL possuem diferenças conceituais. A **IA** é o campo mais amplo, que engloba todas as técnicas para tornar máquinas inteligentes. Dentro dela, o **Machine Learning (ML)** foca em algoritmos que aprendem padrões a partir dos dados para realizar previsões ou classificações. Já o **Deep Learning (DL)** é uma subárea do ML baseada em redes neurais artificiais profundas, capaz de lidar com grandes volumes de dados e tarefas complexas, como visão computacional e processamento de linguagem natural.


## 3. Machine Learn Foundations

**Explain Machine Learning Basics**  
Machine Learning (ML) é uma área da Inteligência Artificial que permite que sistemas aprendam automaticamente a partir de dados sem a necessidade de programação explícita para cada tarefa. O processo envolve fornecer dados de entrada e permitir que algoritmos descubram padrões, façam previsões e tomem decisões com base nessas informações. O objetivo principal é melhorar continuamente o desempenho conforme novos dados são processados.

**Discuss Supervised Learning Fundamentals (Regression & Classification)**  
O aprendizado supervisionado ocorre quando um modelo é treinado com dados rotulados, ou seja, entradas já associadas a respostas corretas. Dentro desse paradigma, a **regressão** é usada para prever valores contínuos, como preços ou temperaturas, enquanto a **classificação** é aplicada para categorizar informações em classes discretas, como identificar se um e-mail é spam ou não. A qualidade dos dados rotulados é essencial para o desempenho do modelo.

**Discuss Unsupervised Learning Fundamentals**  
No aprendizado não supervisionado, os dados não possuem rótulos pré-definidos, e o objetivo é identificar padrões ocultos ou agrupar informações semelhantes. Técnicas comuns incluem **clustering**, que agrupa elementos com características semelhantes, e **redução de dimensionalidade**, que simplifica conjuntos de dados complexos preservando informações relevantes. Esse tipo de aprendizado é útil em cenários de exploração, como segmentação de clientes e análise de comportamento.

**Discuss Reinforcement Learning Fundamentals**  
O aprendizado por reforço é baseado na interação de um agente com um ambiente, onde ele aprende a tomar decisões por meio de tentativa e erro. A cada ação, o agente recebe uma recompensa ou penalidade, ajustando sua estratégia para maximizar o retorno acumulado ao longo do tempo. Esse método é amplamente utilizado em robótica, jogos e sistemas autônomos, pois permite desenvolver comportamentos inteligentes em ambientes dinâmicos e complexos.


## 4. Deep Learn Foundations

**Discuss Deep Learning Fundamentals**  
Deep Learning é uma subárea do Machine Learning que utiliza redes neurais artificiais profundas para aprender representações complexas dos dados. A principal vantagem desse paradigma é sua capacidade de lidar com grandes volumes de dados e extrair automaticamente características relevantes sem a necessidade de engenharia manual. Essa abordagem é a base de avanços recentes em visão computacional, reconhecimento de fala e processamento de linguagem natural.

**Explain Convolutional Models (CNN)**  
As Redes Neurais Convolucionais (CNNs) são especialmente projetadas para processar dados com estrutura de grade, como imagens. Elas utilizam camadas de convolução que aplicam filtros para extrair padrões locais, como bordas, formas e texturas, e camadas de pooling para reduzir a dimensionalidade mantendo informações importantes. Graças a essa arquitetura, as CNNs se tornaram a principal técnica para tarefas de visão computacional, como classificação de imagens, detecção de objetos e reconhecimento facial.

**Explain Sequence Models (RNN & LSTM)**  
Modelos de sequência, como Redes Neurais Recorrentes (RNNs), são projetados para lidar com dados sequenciais, capturando dependências temporais ou contextuais. No entanto, as RNNs tradicionais sofrem com problemas de longo prazo, como o desaparecimento do gradiente. Para resolver isso, surgiram as Long Short-Term Memory (LSTM), que introduzem mecanismos de memória capazes de armazenar informações relevantes por longos períodos. Esses modelos são amplamente utilizados em tradução automática, reconhecimento de fala e análise de séries temporais.


## 5. Generative AI and LLM Foundations

**Discuss Generative AI Overview**  
Generative AI é uma área da inteligência artificial focada em criar novos conteúdos, como textos, imagens, músicas ou códigos, a partir de padrões aprendidos em grandes volumes de dados. Diferente de modelos tradicionais que apenas classificam ou predizem, os modelos generativos produzem resultados originais, simulando criatividade humana. Essa tecnologia tem aplicações em chatbots, design, medicina, entretenimento e muito mais.

**Discuss Large Language Models Fundamentals**  
Os Modelos de Linguagem de Grande Escala (LLMs) são redes neurais treinadas com enormes quantidades de texto para compreender e gerar linguagem natural de forma coerente. Eles funcionam prevendo a próxima palavra em uma sequência, mas devido à sua escala e arquitetura, conseguem capturar nuances linguísticas, contextos complexos e até raciocínio. LLMs são a base de ferramentas como ChatGPT, Bard e Claude.

**Explain Transformers Fundamentals**  
A arquitetura Transformer revolucionou o processamento de linguagem natural ao introduzir mecanismos de atenção, que permitem ao modelo focar em diferentes partes de um texto ao mesmo tempo. Isso possibilita lidar com contextos longos e dependências distantes, superando limitações de modelos anteriores como RNNs e LSTMs. Transformadores são a espinha dorsal de LLMs modernos.

**Explain Prompt Engineering & Instruction Tuning**  
Prompt Engineering é a prática de projetar entradas (prompts) que guiem o modelo a produzir respostas específicas e úteis. Instruction Tuning, por sua vez, consiste em treinar o modelo para seguir instruções em linguagem natural, ajustando-o para entender melhor comandos de usuários. Essas técnicas são fundamentais para tornar LLMs mais alinhados com expectativas humanas e aplicações práticas.

**Explain LLM Fine-tuning**  
Fine-tuning é o processo de ajustar um modelo de linguagem pré-treinado em um conjunto de dados específico, com o objetivo de especializá-lo em uma tarefa ou domínio. Existem diferentes abordagens, como full fine-tuning, few-shot learning ou LoRA (Low-Rank Adaptation), que variam em custo computacional e flexibilidade. Esse processo permite criar versões customizadas de LLMs para áreas como saúde, jurídico ou atendimento ao cliente.

## 6. Get Started with OCI AI Stack

**Discuss OCI AI Services Overview**  
O Oracle Cloud Infrastructure (OCI) oferece uma gama de serviços de Inteligência Artificial prontos para uso, voltados a resolver problemas de negócio sem necessidade de construir modelos do zero. Entre eles estão APIs para visão computacional, processamento de linguagem natural (NLP), tradução, detecção de anomalias e reconhecimento de fala. Esses serviços são pré-treinados, escaláveis e integrados nativamente ao ecossistema OCI.

**Discuss OCI ML Services Overview**  
Os serviços de Machine Learning no OCI permitem que desenvolvedores e cientistas de dados treinem, implantem e gerenciem modelos personalizados. O **OCI Data Science** é a plataforma central para criação e treinamento de modelos, com suporte a frameworks populares como TensorFlow, PyTorch e Scikit-learn. Além disso, há integração com pipelines MLOps, automação de treinamento e suporte a notebooks Jupyter para colaboração.

**Discuss OCI AI Infrastructure Overview**  
A infraestrutura de AI do OCI fornece poder computacional otimizado para workloads intensivos, como GPUs NVIDIA A100 e clusters HPC. Ela é projetada para suportar desde treinamento de modelos de larga escala até inferência em tempo real. Além disso, a infraestrutura inclui armazenamento de alto desempenho, rede RDMA (Remote Direct Memory Access) para baixa latência e ferramentas de monitoramento e escalabilidade.

**Explain Responsible AI**  
A Oracle destaca princípios de **IA Responsável**, que incluem transparência, justiça, segurança e governança. Isso envolve fornecer modelos auditáveis, monitoramento para evitar viés, práticas de privacidade de dados e conformidade regulatória. O objetivo é garantir que as soluções de AI sejam éticas, confiáveis e aplicáveis em setores sensíveis, como saúde, finanças e governo.

## 📊 Comparação dos serviços de AI/ML — OCI x AWS x Azure x GCP

| Categoria | **OCI** | **AWS** | **Azure** | **GCP** |
|-----------|---------|---------|-----------|---------|
| **AI Services (APIs pré-treinadas)** | OCI AI Services (Vision, Language, Speech, Anomaly Detection, Document Understanding) | Amazon AI Services (Rekognition, Comprehend, Polly, Translate, Textract) | Azure Cognitive Services (Vision, Speech, Language, Decision) | Google Cloud AI APIs (Vision AI, Natural Language, Translation, Speech-to-Text, Document AI) |
| **ML Services (treino e deploy)** | OCI Data Science (JupyterLab, MLOps, AutoML) | SageMaker (Studio, Training, Inference, Pipelines) | Azure ML (Designer, Notebooks, MLOps, AutoML) | Vertex AI (Training, Pipelines, Notebooks, AutoML) |
| **Infraestrutura AI (GPU/HPC)** | Bare Metal GPU (NVIDIA A100, H100), HPC Clusters, RDMA Networking | EC2 P4/P5 Instances, Elastic Inference, Trainium/Inferentia chips | Azure ND/NC Series GPUs, AI Supercomputer | TPU v5e, GPU A100/H100, AI-optimized VMs |
| **Responsible AI** | Governança, ética, transparência integradas no OCI | AI Ethics & Responsibility Program, Model Card Toolkit | Responsible AI Dashboard, Fairness/Transparency Toolkits | Responsible AI Toolkit, Explainable AI, Model Cards |

## 7. Get started with OCI Generative AI Services

**Describe OCI Generative AI Services**  
O OCI Generative AI Services oferece acesso direto a modelos de linguagem de grande escala (LLMs) hospedados na Oracle Cloud, permitindo a geração de texto, resumos, traduções, classificações e assistentes conversacionais. Esses serviços eliminam a necessidade de treinar modelos do zero, já que fornecem APIs prontas para integração em aplicações corporativas, com foco em segurança, escalabilidade e governança de dados.

**Discuss Autonomous Database Select AI**  
O recurso **Select AI** integra diretamente modelos generativos ao **Oracle Autonomous Database**, permitindo consultas SQL que chamam modelos de IA para análise de texto e geração de insights em tempo real. Isso possibilita que equipes usem SQL tradicional para tarefas como sumarização de documentos, análise semântica e enriquecimento de dados, sem necessidade de pipelines externos ou reprocessamento.

**Discuss Oracle Vector Search**  
O **Oracle Vector Search** é uma funcionalidade que adiciona suporte a embeddings vetoriais no banco de dados. Com isso, é possível realizar buscas semânticas eficientes em dados não estruturados, como documentos, imagens ou texto. Esse recurso é essencial para aplicações baseadas em **RAG (Retrieval-Augmented Generation)**, pois permite combinar a busca vetorial com modelos generativos para respostas mais contextuais e precisas.

## 8. Dive-Deep into OCI AI Services

**Explore OCI AI Services & related APIs (Language, Vision, Document Understanding, Speech)**  
O **OCI AI Services** oferece um conjunto de APIs especializadas que permitem integrar inteligência artificial em aplicações corporativas sem a necessidade de criar e treinar modelos do zero. Esses serviços são totalmente gerenciados, escaláveis e podem ser consumidos diretamente via chamadas de API.  

- **Language**: APIs para análise de texto, incluindo processamento de linguagem natural (NLP), extração de entidades, análise de sentimentos, classificação e tradução automática. Ideais para chatbots, análise de feedback e sistemas de suporte.  
- **Vision**: Serviços para análise de imagens, reconhecimento de objetos, detecção de rostos e classificação de conteúdo visual. Amplamente usados em inspeção de qualidade, segurança e aplicações de reconhecimento.  
- **Document Understanding**: APIs que permitem extrair automaticamente informações estruturadas de documentos não estruturados, como PDFs, contratos e faturas. Usado para automação de processos e redução de trabalho manual.  
- **Speech**: Serviços de reconhecimento e síntese de fala (Speech-to-Text e Text-to-Speech), possibilitando transcrições automáticas, legendas em tempo real e interfaces de voz para aplicações.  

Essas APIs são projetadas para funcionar de forma integrada, permitindo que empresas construam soluções completas que combinam linguagem, visão, documentos e fala em um mesmo fluxo inteligente.

## 📊 Comparação de APIs de AI — OCI vs AWS vs Azure vs GCP

| Categoria | **OCI AI Services** | **AWS** | **Azure** | **GCP** |
|-----------|----------------------|---------|-----------|---------|
| **Language (NLP)** | OCI Language (análise de sentimentos, extração de entidades, tradução, classificação de texto) | Amazon Comprehend (NLP, entidades, sentimentos, tópicos) + Amazon Translate | Azure Cognitive Services – Text Analytics & Translator | Cloud Natural Language API + Translation AI |
| **Vision (Imagens)** | OCI Vision (detecção de objetos, classificação, OCR básico) | Amazon Rekognition (objetos, rostos, moderação de imagens e vídeos) | Azure Computer Vision + Face API | Cloud Vision AI (objetos, OCR, SafeSearch, labels) |
| **Document Understanding** | OCI Document Understanding (extração de informações estruturadas de PDFs, faturas, contratos) | Amazon Textract (OCR avançado e parsing de documentos) | Azure Form Recognizer (extração de dados estruturados de documentos) | Document AI (OCR e extração inteligente de documentos) |
| **Speech (fala)** | OCI Speech (Speech-to-Text e Text-to-Speech) | Amazon Transcribe (STT) + Amazon Polly (TTS) | Azure Speech Services (Speech-to-Text, Text-to-Speech, tradução de fala) | Cloud Speech-to-Text + Cloud Text-to-Speech |
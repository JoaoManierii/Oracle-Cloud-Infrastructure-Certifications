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

## 6. OCI AI Portifolio

## 7. OCI Generative Service 

## 8. OCI AI services

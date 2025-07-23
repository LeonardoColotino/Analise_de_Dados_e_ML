Decision - Co-Piloto de Recrutamento
Python Streamlit Docker

O Decision é uma aplicação inteligente de recrutamento que utiliza Machine Learning para prever a compatibilidade entre candidatos e vagas. O sistema usa um modelo semântico unificado, baseado em embeddings de texto (SBERT) e um algoritmo de Gradient Boosting (XGBoost), para analisar o contexto completo de currículos e descrições de vagas, gerando um score de afinidade preciso.

Desenvolvido como solução para o Datathon Data Analytics da Decision, esta ferramenta de IA é focada em duas frentes: a priorização estratégica de candidatos para vagas abertas e a descoberta de perfis de sucesso com base em dados históricos, visando tornar o processo de seleção mais rápido, assertivo e data-driven.

Funcionalidades
Matching Semântico: Análise de compatibilidade baseada no significado e contexto dos textos, e não apenas em palavras-chave.
Modelo de ML Unificado: Um único e robusto modelo XGBoost que aprende com embeddings de texto e features de engenharia.
Análise de Requisitos: Avaliação de compatibilidade de níveis de senioridade, idiomas e localização.
Interface Streamlit: Interface web intuitiva para análise de vagas e candidatos.
Visualização de Dados: Gráficos para análise de importância de features e performance do modelo.
Containerização Docker: Deploy simplificado e reproduzível.
Arquitetura do Projeto
Datathon/
├── app/                        # Aplicação Streamlit
│   ├── main.py                 # Ponto de entrada principal
│   └── pages/
│       ├── match.py           # Página de matching
│       └── sobre.py           # Página sobre o projeto
├── data/                      # Dados do projeto
│   ├── raw/                   # Dados brutos
│   │   ├── applicants.json    # Dados dos candidatos
│   │   ├── jobs.json          # Dados das vagas
│   │   └── prospects.json     # Dados de prospects
│   └── processed/             # Dados processados
├── models/                    # Modelos de Machine Learning
│   ├── modelo_treinado*.pkl   # Modelos especializados por tecnologia
│   └── modelo.py              # Script de treinamento
├── notebooks/                 # Análises exploratórias
│   ├── eda_applicants.ipynb   # EDA dos candidatos
│   ├── eda_jobs.ipynb         # EDA das vagas
│   └── eda_prospects.ipynb    # EDA dos prospects
├── Dockerfile                 # Configuração Docker
├── requirements.txt           # Dependências Python
└── README.md                  # Este arquivo
Arquitetura do Modelo
O sistema abandonou a abordagem de múltiplos modelos por tecnologia em favor de um modelo semântico unificado, que se mostrou mais flexível e poderoso. A arquitetura funciona da seguinte forma:

Engenharia de Features: Dados como nível de senioridade, idiomas e localização são extraídos e comparados.
Embeddings de Texto: Os textos completos da vaga e do currículo são convertidos em vetores numéricos (embeddings) usando o modelo SBERT (paraphrase-MiniLM-L6-v2). Isso permite que o modelo entenda o significado semântico dos textos.
Modelo Preditivo: Os vetores de embeddings e as features de engenharia são combinados para treinar um classificador XGBoost, que prevê a probabilidade de um "match" de sucesso.
Balanceamento de Classes: A técnica SMOTE é usada durante o treinamento para lidar com o desbalanceamento entre candidatos contratados e não contratados.
Esta abordagem permite que o modelo generalize para qualquer tipo de vaga, incluindo tecnologias novas que não estavam nos dados de treino originais.

Tecnologias Utilizadas
Python 3.12+
Streamlit - Interface web
XGBoost - Algoritmo de Machine Learning
Sentence-Transformers (SBERT) - Processamento de linguagem natural e embeddings
NLTK - Toolkit de linguagem natural (para stopwords)
Imbalanced-learn - Para balanceamento de classes (SMOTE)
Pandas/NumPy - Manipulação de dados
Scikit-learn - Ferramentas de ML
Docker - Containerização

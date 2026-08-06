# 💰 Sr. EasyWay — Educador Financeiro Inteligente

O **Sr. EasyWay** é um assistente de inteligência artificial voltado para educação financeira personalizada. O objetivo do projeto é transformar a maneira como as pessoas lidam com suas finanças pessoais, oferecendo orientações claras, análise de perfis e sugestões de produtos financeiros adequados a cada perfil de cliente.

---

## 📹 Pitch do Projeto

Confira o vídeo de demonstração e apresentação do **Sr. EasyWay**:

[![Assista ao Pitch do Sr. EasyWay](https://img.youtube.com/vi/SEU_VIDEO_ID/maxresdefault.jpg)](https://www.youtube.com/watch?v=SEU_VIDEO_ID)

---

## 📁 Estrutura do Repositório

O projeto está organizado da seguinte forma:

```
.
├── assets/                  # Recursos visuais e roteiros do laboratório
│   ├── README.md
│   └── RoteiroLab.md        # Passo a passo e diretrizes do lab
├── data/                    # Módulos de dados simulados / Base do agente
│   ├── historico_atendimento.csv
│   ├── perfil_investidor.json
│   ├── produtos_financeiros.json
│   └── transacoes.csv
├── docs/                    # Documentação detalhada da solução
│   ├── 01-documentacao-agente.md # Arquitetura e persona do Sr. EasyWay
│   ├── 02-base-conhecimento.md   # Conhecimento do agente em finanças
│   ├── 03-prompts.md             # System prompts e engenharia de prompt
│   ├── 04-metricas.md            # Métricas de avaliação do agente
│   └── 05-pitch.md               # Apresentação executiva do projeto
└── src/                     # Código-fonte e scripts de execução
    └── README.md
```

---

## 🚀 Funcionalidades Principais

- **Análise de Perfil Financeiro:** Diagnóstico a partir do histórico de transações e perfil de risco do usuário (`data/`).
- **Engenharia de Prompt Avançada:** Prompts estruturados com instruções claras, regras de conduta e restrições de resposta (`docs/03-prompts.md`).
- **Recomendação Inteligente:** Mapeamento entre perfil de investimento e catálogo de produtos financeiros (`data/produtos_financeiros.json`).
- **Avaliação & Métricas:** Acompanhamento contínuo de qualidade da resposta e engajamento do usuário (`docs/04-metricas.md`).

---

## 🛠️ Como Utilizar

1. **Documentação:** Explore a pasta `docs/` para entender a modelagem, os prompts utilizados e a proposta de valor (**Pitch**).
2. **Dados de Teste:** Em `data/`, consulte os modelos de dados e históricos estruturados para alimentação do modelo RAG ou assistente.
3. **Execução:** Consulte os guias em `src/` e `assets/RoteiroLab.md` para instruções de execução da aplicação.

---

## 🎯 Objetivo do Projeto

Desenvolvido no contexto de desafio prático (DIO Lab), o **Sr. EasyWay** demonstra a aplicação prática de agentes de IA Generativa voltados ao setor financeiro, focando em empatia, clareza técnica e precisão no direcionamento financeiro.

# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Para que serve no Sr. EasyWay? |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualiza interações anteriores para acompanhar o progresso do usuário e dar continuidade aos atendimentos.|
| `perfil_investidor.json` | JSON | Personaliza o acompanhamento e explicações ao usuário, aprimorando as análises financeiras e oferecendo orientações cada vez mais direcionadas.|
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente |

---

## Adaptações nos Dados

Expansão do conjunto de dados mockados adicionando a coluna objetivo_cliente, permitindo registrar e mapear as metas financeiras informadas pelos usuários durante as interações com o agente.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Existem duas possibilidades, injetar os dados diretamente no prompt (Ctrl + C, Ctrl + V) ou carregar os arquivos via código, como no exemplo abaixo: 

```python
import pandas as pd
import json

# CSVs
historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

# JSONs
with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
    perfil = json.load(f)

with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
    produtos = json.load(f)

```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Para simplificar, podemos simplesmente "injetar" os dados em nosso prompt. garantindo que o agente tenha o melhor contexto possível. Lembrando que, em soluções mais robustas, o ideal é que essas informações sejam carregadas dinamicamente para que possamos ganhar flexibilidade. 

```text
DADOS  E PERFIL DO USUÁRIO (data/perfil_investidor.json):

{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

HISTÓRICO DE ATENDIMENTO (data/historico_atendimento.csv):

data,canal,tema,resumo,resolvido,objetivo_cliente
2025-09-15,chat,CDB,Cliente perguntou sobre rentabilidade e prazos,sim,Rendimento a Curto Prazo
2025-09-22,telefone,Problema no app,Erro ao visualizar extrato foi corrigido,sim,-
2025-10-01,chat,Tesouro Selic,Cliente pediu explicação sobre o funcionamento do Tesouro Direto,sim,Aprender sobre Investimentos
2025-10-12,chat,Metas financeiras,Cliente acompanhou o progresso da reserva de emergência,sim,Montar Reserva de Emergência (R$ 10.000)
2025-10-25,email,Atualização cadastral,Cliente atualizou e-mail e telefone,sim,-
2025-11-05,chat,Planejamento de Viagem,Cliente solicitou simulação para poupar até o fim do ano,sim,Viagem de Férias (R$ 5.000)

TRANSAÇÕES DO USUÁRIO (data/transacoes.csv:

data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida


PRODUTOS DISPONÍVEIS PARA ENSINO (data/produtos_financeiros.json):

[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Multimercado",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "CDI + 2%",
    "aporte_minimo": 500.00,
    "indicado_para": "Perfil moderado que busca diversificação"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"
  }
]

````

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

O exemplo de contexto montado abaixo, se baseia nos dados originais da base de conhecimento, mas os sintetiza deixando apenas as informações mais relevantes, otimizando assim o consumo de Tokens. Entretanto, vale lembrar que mais importante do que economizar Tokens, é ter todas as informações relevantes disponíveis em seu contexto.  

```
Dados e Perfil do Usuário:
- Nome: João Silva | Idade: 32 anos | Profissão: Analista de Sistemas
- Renda Mensal: R$ 5.000,00 | Patrimônio Total: R$ 15.000,00
- Perfil de Investidor: Moderado | Aceita Risco: Não (false)
- Objetivo Principal: Construir reserva de emergência
- Reserva de Emergência Atual: R$ 10.000,00
- Metas:
  1. Completar reserva de emergência - R$ 15.000,00 (Prazo: 2026-06)
  2. Entrada do apartamento - R$ 50.000,00 (Prazo: 2027-12)

Histórico de Atendimentos:
- 15/09/2025 [Chat] Tema: CDB | Resumo: Cliente perguntou sobre rentabilidade e prazos | Resolvido: Sim | Objetivo: Rendimento a Curto Prazo
- 22/09/2025 [Telefone] Tema: Problema no app | Resumo: Erro ao visualizar extrato foi corrigido | Resolvido: Sim | Objetivo: -
- 01/10/2025 [Chat] Tema: Tesouro Selic | Resumo: Cliente pediu explicação sobre o funcionamento do Tesouro Direto | Resolvido: Sim | Objetivo: Aprender sobre Investimentos
- 12/10/2025 [Chat] Tema: Metas financeiras | Resumo: Cliente acompanhou o progresso da reserva de emergência | Resolvido: Sim | Objetivo: Montar Reserva de Emergência (R$ 10.000)
- 25/10/2025 [E-mail] Tema: Atualização cadastral | Resumo: Cliente atualizou e-mail e telefone | Resolvido: Sim | Objetivo: -
- 05/11/2025 [Chat] Tema: Planejamento de Viagem | Resumo: Cliente solicitou simulação para poupar até o fim do ano | Resolvido: Sim | Objetivo: Viagem de Férias (R$ 5.000)

Transações Recentes:
- 01/10/2025: Salário (Receita - Moradia) | +R$ 5.000,00
- 02/10/2025: Aluguel (Saída - Moradia) | -R$ 1.200,00
- 03/10/2025: Supermercado (Saída - Alimentação) | -R$ 450,00
- 05/10/2025: Netflix (Saída - Lazer) | -R$ 55,90
- 07/10/2025: Farmácia (Saída - Saúde) | -R$ 89,00
- 10/10/2025: Restaurante (Saída - Alimentação) | -R$ 120,00
- 12/10/2025: Uber (Saída - Transporte) | -R$ 45,00
- 15/10/2025: Conta de Luz (Saída - Moradia) | -R$ 180,00
- 20/10/2025: Academia (Saída - Saúde) | -R$ 99,00
- 25/10/2025: Combustível (Saída - Transporte) | -R$ 250,00

Produtos Disponíveis para Ensino:
1. Tesouro Selic | Categoria: Renda Fixa | Risco: Baixo | Rentabilidade: 100% da Selic | Aporte Mínimo: R$ 30,00 | Indicado para: Reserva de emergência e iniciantes
2. CDB Liquidez Diária | Categoria: Renda Fixa | Risco: Baixo | Rentabilidade: 102% do CDI | Aporte Mínimo: R$ 100,00 | Indicado para: Quem busca segurança com rendimento diário
3. LCI/LCA | Categoria: Renda Fixa | Risco: Baixo | Rentabilidade: 95% do CDI | Aporte Mínimo: R$ 1.000,00 | Indicado para: Quem pode esperar 90 dias (isento de IR)
4. Fundo Multimercado | Categoria: Fundo | Risco: Médio | Rentabilidade: CDI + 2% | Aporte Mínimo: R$ 500,00 | Indicado para: Perfil moderado que busca diversificação
5. Fundo de Ações | Categoria: Fundo | Risco: Alto | Rentabilidade: Variável | Aporte Mínimo: R$ 100,00 | Indicado para: Perfil arrojado com foco no longo prazo
```

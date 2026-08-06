# Passo a passo de execução

## Setup do Ollama 

```bash
# 1. Instalar Ollama (ollama.com)

# 2. Baixar um modelo leve
- Modelo escolhido: Ollama pull gpt-oss

# 3. Testar se funciona
Ollama run gpt-oss "Olá!"
```

## Código Completo

Todo código-fonte está no arquivo `app.py`.

## Como Rodar

```bash
# 1. Instalar dependências
pip install streamlit pandas requests

# 2. Garantir que Ollama está rodando
ollama serve

# 3. Rodar a aplicação
streamlit run app.py
```

## Evidência de Execução


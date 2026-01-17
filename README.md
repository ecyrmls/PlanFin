# PlanFin - Sistema de Planejamento Financeiro

Sistema web de planejamento financeiro pessoal desenvolvido como Trabalho de Conclusão de Curso (TCC) do MBA em Engenharia de Software da ESALQ/USP.

## 📋 Descrição

O PlanFin é uma aplicação que auxilia usuários a definir uma estratégia de alocação de investimentos personalizada. O sistema:

1. **Coleta informações do usuário** através de um questionário interativo
2. **Agrega dados de mercado** de múltiplas fontes
3. **Gera uma alocação recomendada** baseada no perfil de investidor
4. **Apresenta projeções visuais** comparando a carteira sugerida com benchmarks

## 🔒 Nota sobre Dados

Este repositório contém dados anonimizados para conformidade com normas acadêmicas:

- **Fontes de dados**: Nomes de corretoras e APIs foram anonimizados
- **Fundos de investimento**: Nomes substituídos por IDs (F_1_XXXX, F_2_XXXX)
- **Títulos de renda fixa**: Nomes substituídos por IDs (T_XXXX)
- **Dados públicos**: Yahoo Finance (ações, índices B3) mantidos sem alteração

O sistema opera em **modo demonstração** utilizando os CSVs pré-processados incluídos no repositório.

## 🏗️ Arquitetura

```
PlanFin/
├── backend/                # API Python + FastAPI
│   ├── analise/            # Módulo de análise e seleção de ativos
│   ├── data/               # Dados de fontes de mercado (anonimizados)
│   │   ├── fonte_1/        # Fundos - Fonte 1
│   │   ├── fonte_2/        # Fundos - Fonte 2
│   │   ├── agregador_rf/   # Títulos de renda fixa
│   │   └── yfinance/       # Ações e índices (dados públicos)
│   ├── main.py             # Servidor FastAPI
│   └── run_global_app.py   # Orquestrador de coleta de dados
├── frontend/               # Interface React + Vite
│   └── src/
│       ├── components/     # Componentes React
│       ├── hooks/          # Custom hooks
│       └── pages/          # Páginas da aplicação
└── docker-compose.yml      # Orquestração dos serviços
```

## 🚀 Como Executar

### Pré-requisitos
- Docker e Docker Compose instalados
- Portas 5173 (frontend) e 8000 (backend) disponíveis
- Navegador Google Chrome (recomendado)

### Execução

```bash
# Clonar o repositório
git clone <repo-url>
cd PlanFin

# Iniciar os serviços
docker-compose up --build

# Acessar a aplicação
# Frontend: http://localhost:5173
# Backend API: http://localhost:8000
# Documentação API: http://localhost:8000/docs
```

Feitas essas etapas com sucesso, todo o aplicativo pode ser acessado e interagido a partir do seu navegador web.

Na etapa de análise ("Carregando..."), o processo pode demorar até alguns minutos. Isso é normal. Aguarde!

## 📊 Perfis de Investimento

O sistema suporta três perfis de investidor:

| Perfil | Renda Fixa | Multimercado | Ações |
|--------|------------|--------------|-------|
| Conservador | 70% | 15% | 15% |
| Moderado | 40% | 20% | 40% |
| Arrojado | 10% | 20% | 70% |

## 🔧 Tecnologias Utilizadas

### Backend
- Python
- FastAPI
- Pandas
- yfinance

### Frontend
- React
- Vite
- Recharts

### Infraestrutura
- Docker

## 📁 Estrutura de Dados

### Fontes de Dados de Ativos
- **Fonte 1** - Fundos de investimento (dados anonimizados)
- **Fonte 2** - Fundos de investimento (dados anonimizados)
- **Agregador RF** - Títulos de renda fixa (dados anonimizados)
- **Yahoo Finance** - Ações e ETFs (dados públicos)

### Formato de Saída

O resultado da análise é um JSON com a seguinte estrutura:

```json
{
  "byAsset": [
    {"label": "ID_Ativo", "class": "RF|MM|ACOES", "weight": 0.133, "rent_12m": 0.15}
  ],
  "byBucket": [
    {"bucket": "RF", "weight": 0.4}
  ],
  "lifeLine": {
    "years": [0, 1, 2, ...],
    "percent": {"carteira": [...], "selic": [...], "ipca": [...], "poupanca": [...]},
    "reais": {"carteira": [...], "selic": [...], ...}
  }
}
```

## 📝 Licença

Este projeto foi desenvolvido para fins acadêmicos.

## 👤 Autor

Desenvolvido como TCC do MBA em Engenharia de Software da ESALQ/USP. Chatbots de IA (Claude e ChatGPT) foram utilizados.

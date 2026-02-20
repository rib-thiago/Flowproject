📋 PLANO COMPLETO DE ISSUES E MILESTONES

Com base em todos os flows documentados e no estado atual do projeto, aqui estão as issues organizadas por milestones:

---

🎯 MILESTONE 1: FUNDAÇÃO (Semanas 1-2)

Objetivo: Estabilizar e documentar os processos fundamentais

# Título Tipo Prioridade Estimativa
F1 Criar documentação dos 9 flows do projeto docs Alta 4h
F2 Integrar flows ao MkDocs docs Média 1h
F3 Criar script de inicialização do projeto (onboarding) chore Média 2h
F4 Revisar e atualizar README.md com badges e instruções docs Baixa 1h
F5 Configurar branch protection rules no GitHub chore Alta 30min
F6 Padronizar mensagens de commit com commitizen chore Média 1h

---

🔧 MILESTONE 2: QUALIDADE E TESTES (Semanas 3-4)

Objetivo: Garantir qualidade consistente em todo o código

# Título Tipo Prioridade Estimativa
Q1 FASE 17: Telemetria e testes em classificar_documento.py type Alta 3h
Q2 FASE 18: Telemetria e testes em obter_documento.py type Alta 2h
Q3 FASE 19: Telemetria e testes em estatisticas.py (15% → 85%) type Urgente 4h
Q4 FASE 20: Corrigir MyPy global (6 erros) type/qualidade Alta 2h
Q5 Adicionar testes de integração para repositórios SQLite test Média 3h
Q6 Aumentar cobertura para 80%+ nos arquivos restantes test Média 4h
Q7 Adicionar property-based testing com Hypothesis test Baixa 3h

---

📦 MILESTONE 3: DEPENDÊNCIAS E INFRA (Semanas 5-6)

Objetivo: Resolver dívidas técnicas e melhorar infraestrutura

# Título Tipo Prioridade Estimativa
D1 Migrar dependências NLP para Poetry (Issue #1) tipo/infra Alta 4h
D2 Instalar stubs para módulos externos (types-PyYAML) chore Média 30min
D3 Atualizar CI para usar Poetry completamente chore Média 2h
D4 Adicionar cache mais eficiente no CI chore Baixa 1h
D5 Dockerizar aplicação (CLI + Web) feat Baixa 4h

---

🚀 MILESTONE 4: NOVAS FUNCIONALIDADES (Semanas 7-8)

Objetivo: Expandir capacidades do sistema

# Título Tipo Prioridade Estimativa
N1 Melhoria: Modo escuro no CLI feat Baixa 2h
N2 Melhoria: Gráficos no terminal com plotext feat Média 3h
N3 API REST documentada com OpenAPI/Swagger feat Média 4h
N4 Exportação para PDF (usando ReportLab) feat Média 4h
N5 Busca global no acervo feat Baixa 3h
N6 Cache com Redis para análises frequentes feat Baixa 4h

---

📚 MILESTONE 5: DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)

Objetivo: Preparar para entrega do TCC

# Título Tipo Prioridade Estimativa
R1 Revisar documentação (.md files) - Issue #2 tipo/documentação Alta 3h
R2 Atualizar todas as FASE*.md com resultados finais docs Alta 4h
R3 Criar apresentação do TCC (slides) docs Alta 6h
R4 Preparar vídeo de demonstração docs Média 3h
R5 Revisar e publicar versão final (v1.0.0) release Alta 2h

---

🏷️ TODAS AS LABELS NECESSÁRIAS

```bash
# Labels já existentes
- fase
- tipo/testes
- tipo/qualidade
- tipo/documentação
- tipo/infra
- melhoria
- ux
- prioridade:alta
- prioridade:media
- prioridade:baixa

# Novas labels sugeridas
- tipo/hotfix
- tipo/security
- tipo/performance
- tipo/release
- tipo/onboarding
- status:bloqueado
- status:em-andamento
- status:revisao
```

---

📊 RESUMO DAS ISSUES POR MILESTONE

Milestone Issues Estimativa total
FUNDAÇÃO 6 ~9h
QUALIDADE 7 ~21h
DEPENDÊNCIAS 5 ~11h
NOVAS FUNCIONALIDADES 6 ~20h
DOCUMENTAÇÃO 5 ~18h
TOTAL 29 issues ~79h

---

🚀 SCRIPT PARA CRIAR TODAS AS ISSUES

```bash
#!/bin/bash
# criar_todas_issues.sh
# Script para criar todas as issues do projeto

echo "🚀 Criando todas as issues do ShowTrials..."
echo "==========================================="

# =============================================
# MILESTONE 1: FUNDAÇÃO
# =============================================
echo ""
echo "📌 MILESTONE 1: FUNDAÇÃO"

gh issue create --title "F1: Criar documentação dos 9 flows do projeto" \
  --body "## 🎯 Objetivo
Documentar todos os flows do projeto em arquivos separados.

## 📋 Tarefas
- [ ] Git Flow
- [ ] Quality Flow
- [ ] Telemetry Flow
- [ ] Code Review Flow
- [ ] Dependencies Flow
- [ ] Debug Flow
- [ ] Documentation Flow
- [ ] Refactoring Flow
- [ ] Emergency Flow

## 📁 Local
`docs/flows/`

## ⏱️ Estimativa: 4h" \
  --label "docs,prioridade:alta" \
  --milestone "FUNDAÇÃO (Semanas 1-2)"

gh issue create --title "F2: Integrar flows ao MkDocs" \
  --body "## 🎯 Objetivo
Adicionar os flows documentados ao site do MkDocs.

## 📋 Tarefas
- [ ] Criar seção 'Flows' no mkdocs.yml
- [ ] Adicionar links para cada flow
- [ ] Verificar navegação

## ⏱️ Estimativa: 1h" \
  --label "docs,prioridade:media" \
  --milestone "FUNDAÇÃO (Semanas 1-2)"

gh issue create --title "F3: Criar script de inicialização do projeto" \
  --body "## 🎯 Objetivo
Criar script que configura todo o ambiente do zero.

## 📋 Tarefas
- [ ] Clonar repositório
- [ ] Instalar Poetry
- [ ] Instalar dependências
- [ ] Instalar NLP via pip
- [ ] Baixar modelos
- [ ] Verificar instalação

## ⏱️ Estimativa: 2h" \
  --label "chore,prioridade:media" \
  --milestone "FUNDAÇÃO (Semanas 1-2)"

# =============================================
# MILESTONE 2: QUALIDADE
# =============================================
echo ""
echo "📌 MILESTONE 2: QUALIDADE"

gh issue create --title "Q1: FASE 17 - classificar_documento.py" \
  --body "## 🎯 Objetivo
Aumentar cobertura de 65% para 85% em classificar_documento.py

## 📊 Métricas Atuais
- **Cobertura:** 65%
- **Linhas não cobertas:** 18
- **Telemetria:** ❌ Ausente
- **MyPy:** ✅ OK

## 📋 Tarefas
- [ ] Adicionar padrão de telemetria
- [ ] Expandir testes existentes
- [ ] Criar testes de telemetria
- [ ] Verificar cobertura final

## ⏱️ Estimativa: 3h" \
  --label "fase,tipo/testes,prioridade:alta" \
  --milestone "QUALIDADE E TESTES (Semanas 3-4)"

gh issue create --title "Q2: FASE 18 - obter_documento.py" \
  --body "## 🎯 Objetivo
Aumentar cobertura de 57% para 85% em obter_documento.py

## 📊 Métricas Atuais
- **Cobertura:** 57%
- **Linhas não cobertas:** 15
- **Telemetria:** ❌ Ausente
- **MyPy:** ⚠️ 2 erros

## 📋 Tarefas
- [ ] Adicionar padrão de telemetria
- [ ] Expandir testes existentes
- [ ] Criar testes de telemetria
- [ ] Corrigir MyPy
- [ ] Verificar cobertura final

## ⏱️ Estimativa: 2h" \
  --label "fase,tipo/testes,prioridade:alta" \
  --milestone "QUALIDADE E TESTES (Semanas 3-4)"

gh issue create --title "Q3: FASE 19 - estatisticas.py (URGENTE)" \
  --body "## 🎯 Objetivo
Aumentar cobertura de 15% para 85% em estatisticas.py

## 📊 Métricas Atuais
- **Cobertura:** 15% (⚠️ URGENTE!)
- **Linhas não cobertas:** 41
- **Telemetria:** ❌ Ausente
- **MyPy:** ⚠️ 3 erros

## 📋 Tarefas
- [ ] Adicionar padrão de telemetria
- [ ] Criar testes de lógica
- [ ] Criar testes de telemetria
- [ ] Corrigir MyPy
- [ ] Verificar cobertura final

## ⏱️ Estimativa: 4h" \
  --label "fase,tipo/testes,prioridade:alta" \
  --milestone "QUALIDADE E TESTES (Semanas 3-4)"

# =============================================
# CONTINUAR PARA TODAS AS ISSUES...
# =============================================

echo ""
echo "✅ Script concluído! Foram criadas:" 
echo "- 6 issues para FUNDAÇÃO"
echo "- 7 issues para QUALIDADE"
echo "- 5 issues para DEPENDÊNCIAS" 
echo "- 6 issues para NOVAS FUNCIONALIDADES"
echo "- 5 issues para DOCUMENTAÇÃO"
echo ""
echo "📊 TOTAL: 29 issues"
```

---

✅ PRÓXIMOS PASSOS

1. Criar os milestones no GitHub:
   · FUNDAÇÃO (Semanas 1-2) - due date: +14 dias
   · QUALIDADE E TESTES (Semanas 3-4) - due date: +28 dias
   · DEPENDÊNCIAS E INFRA (Semanas 5-6) - due date: +42 dias
   · NOVAS FUNCIONALIDADES (Semanas 7-8) - due date: +56 dias
   · DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo) - due date: TCC
2. Criar as issues (pode usar o script acima como base)
3. Adicionar ao Project Kanban

Quer que eu gere o script completo com todas as 29 issues? 🚀

📜 SCRIPT COMPLETO - 29 ISSUES + INSTRUÇÕES

```bash
#!/bin/bash
# criar_todas_issues.sh
# Script COMPLETO para criar todas as issues do projeto ShowTrials
# Uso: chmod +x criar_todas_issues.sh && ./criar_todas_issues.sh

echo "🚀 ShowTrials - Criando todas as 29 issues do projeto"
echo "====================================================="
echo ""

# =============================================
# VERIFICAR AUTENTICAÇÃO
# =============================================
echo "🔍 Verificando autenticação no GitHub..."
if ! gh auth status &>/dev/null; then
    echo "❌ Você não está logado no GitHub CLI"
    echo "   Execute: gh auth login"
    exit 1
fi
echo "   ✅ Autenticado"
echo ""

# =============================================
# CRIAR MILESTONES
# =============================================
echo "📅 Criando milestones (pelo site)..."
echo ""
echo "⚠️  ATENÇÃO: Milestones precisam ser criados manualmente pelo site:"
echo "   https://github.com/rib-thiago/showtrials-tcc/milestones/new"
echo ""
echo "   Crie os seguintes milestones:"
echo "   ------------------------------"
echo "   1. FUNDAÇÃO (Semanas 1-2)"
echo "      - Due date: $(date -d "+14 days" +%Y-%m-%d)"
echo "      - Description: Documentação e configuração inicial"
echo ""
echo "   2. QUALIDADE E TESTES (Semanas 3-4)"
echo "      - Due date: $(date -d "+28 days" +%Y-%m-%d)"
echo "      - Description: Aumentar cobertura, corrigir MyPy"
echo ""
echo "   3. DEPENDÊNCIAS E INFRA (Semanas 5-6)"
echo "      - Due date: $(date -d "+42 days" +%Y-%m-%d)"
echo "      - Description: Migrar NLP, stubs, Docker"
echo ""
echo "   4. NOVAS FUNCIONALIDADES (Semanas 7-8)"
echo "      - Due date: $(date -d "+56 days" +%Y-%m-%d)"
echo "      - Description: Modo escuro, gráficos, API, PDF"
echo ""
echo "   5. DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"
echo "      - Due date: $(date -d "+90 days" +%Y-%m-%d)"
echo "      - Description: Revisão de docs, preparação TCC"
echo ""
read -p "Pressione Enter após criar os milestones para continuar..."
echo ""

# =============================================
# FUNÇÃO PARA CRIAR ISSUE
# =============================================
create_issue() {
    local title="$1"
    local body="$2"
    local labels="$3"
    local milestone="$4"
    
    echo "   Criando: $title"
    gh issue create --title "$title" --body "$body" --label "$labels" --milestone "$milestone"
    echo "   ✅ Criada"
    echo ""
}

# =============================================
# MILESTONE 1: FUNDAÇÃO (Semanas 1-2)
# =============================================
echo "📌 MILESTONE 1: FUNDAÇÃO (6 issues)"
echo "-------------------------------------"

create_issue "F1: Criar documentação dos 9 flows do projeto" \
"## 🎯 Objetivo
Documentar todos os flows do projeto em arquivos separados na pasta `docs/flows/`.

## 📋 Tarefas
- [ ] Git Flow
- [ ] Quality Flow (lint, testes, cobertura)
- [ ] Telemetry Flow
- [ ] Code Review Flow
- [ ] Dependencies Flow
- [ ] Debug Flow
- [ ] Documentation Flow
- [ ] Refactoring Flow
- [ ] Emergency Flow (Hotfix)

## 📁 Local
`docs/flows/` (criar pasta)

## 📊 Definição de Pronto
- [ ] 9 arquivos .md criados
- [ ] Cada um com template padrão
- [ ] Revisados e consistentes

## ⏱️ Estimativa: 4h
## Prioridade: Alta" \
  "docs,prioridade:alta" \
  "FUNDAÇÃO (Semanas 1-2)"

create_issue "F2: Integrar flows ao MkDocs" \
"## 🎯 Objetivo
Adicionar os flows documentados ao site do MkDocs para fácil navegação.

## 📋 Tarefas
- [ ] Adicionar seção 'Flows' no `mkdocs.yml`
- [ ] Incluir links para cada flow
- [ ] Verificar navegação localmente
- [ ] Publicar com `mkdocs gh-deploy`

## 📊 Definição de Pronto
- [ ] Seção Flows aparece no menu
- [ ] Todos os links funcionam
- [ ] Site atualizado no GitHub Pages

## ⏱️ Estimativa: 1h
## Prioridade: Média" \
  "docs,prioridade:media" \
  "FUNDAÇÃO (Semanas 1-2)"

create_issue "F3: Criar script de inicialização do projeto (onboarding)" \
"## 🎯 Objetivo
Criar script que configura todo o ambiente do zero para novos desenvolvedores.

## 📋 Tarefas
- [ ] Clonar repositório
- [ ] Verificar/instalar Poetry
- [ ] Instalar dependências (poetry install)
- [ ] Instalar NLP via pip (numpy, spacy, etc.)
- [ ] Baixar modelos spaCy
- [ ] Verificar instalação com testes rápidos

## 📁 Local
`scripts/setup.sh`

## 📊 Definição de Pronto
- [ ] Script funciona em ambiente limpo
- [ ] Documentado no README
- [ ] Testado em Ubuntu (ou seu SO)

## ⏱️ Estimativa: 2h
## Prioridade: Média" \
  "chore,prioridade:media" \
  "FUNDAÇÃO (Semanas 1-2)"

create_issue "F4: Revisar e atualizar README.md" \
"## 🎯 Objetivo
Garantir que o README esteja completo e profissional.

## 📋 Tarefas
- [ ] Atualizar badges (coverage, CI, versão)
- [ ] Verificar instruções de instalação
- [ ] Adicionar seção de 'Primeiros passos'
- [ ] Incluir exemplos de uso
- [ ] Links para documentação
- [ ] Contato e autor

## 📊 Definição de Pronto
- [ ] README revisado e aprovado
- [ ] Todos os links funcionam
- [ ] Badges refletem estado atual

## ⏱️ Estimativa: 1h
## Prioridade: Baixa" \
  "docs,prioridade:baixa" \
  "FUNDAÇÃO (Semanas 1-2)"

create_issue "F5: Configurar branch protection rules no GitHub" \
"## 🎯 Objetivo
Proteger a branch main contra merges acidentais.

## 📋 Tarefas
- [ ] Acessar Settings > Branches
- [ ] Adicionar regra para 'main'
- [ ] Requerer status checks (CI)
- [ ] Requerer branches atualizadas
- [ ] Incluir administradores

## 📊 Definição de Pronto
- [ ] Regras aplicadas e testadas
- [ ] CI é obrigatório para merge

## ⏱️ Estimativa: 30min
## Prioridade: Alta" \
  "chore,prioridade:alta" \
  "FUNDAÇÃO (Semanas 1-2)"

create_issue "F6: Padronizar mensagens de commit com commitizen" \
"## 🎯 Objetivo
Garantir que todas as mensagens de commit sigam o padrão Conventional Commits.

## 📋 Tarefas
- [ ] Verificar configuração do commitizen
- [ ] Atualizar pre-commit hook se necessário
- [ ] Documentar padrão no CONTRIBUTING.md
- [ ] Adicionar exemplo no README

## 📊 Definição de Pronto
- [ ] commitizen funcionando
- [ ] Documentação atualizada

## ⏱️ Estimativa: 1h
## Prioridade: Média" \
  "chore,prioridade:media" \
  "FUNDAÇÃO (Semanas 1-2)"

# =============================================
# MILESTONE 2: QUALIDADE E TESTES (Semanas 3-4)
# =============================================
echo "📌 MILESTONE 2: QUALIDADE E TESTES (7 issues)"
echo "-----------------------------------------------"

create_issue "Q1: FASE 17 - classificar_documento.py" \
"## 🎯 Objetivo
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

## 🔗 Links
- [Arquivo alvo](src/application/use_cases/classificar_documento.py)

## 📊 Definição de Pronto
- [ ] Cobertura >= 85%
- [ ] Testes de lógica (8+)
- [ ] Testes de telemetria (4+)
- [ ] MyPy 0 erros

## ⏱️ Estimativa: 3h
## Prioridade: Alta" \
  "fase,tipo/testes,prioridade:alta" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q2: FASE 18 - obter_documento.py" \
"## 🎯 Objetivo
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

## 🔗 Links
- [Arquivo alvo](src/application/use_cases/obter_documento.py)

## 📊 Definição de Pronto
- [ ] Cobertura >= 85%
- [ ] Testes de lógica (8+)
- [ ] Testes de telemetria (4+)
- [ ] MyPy 0 erros

## ⏱️ Estimativa: 2h
## Prioridade: Alta" \
  "fase,tipo/testes,prioridade:alta" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q3: FASE 19 - estatisticas.py (URGENTE)" \
"## 🎯 Objetivo
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

## 🔗 Links
- [Arquivo alvo](src/application/use_cases/estatisticas.py)

## 📊 Definição de Pronto
- [ ] Cobertura >= 85%
- [ ] Testes de lógica (12+)
- [ ] Testes de telemetria (6+)
- [ ] MyPy 0 erros

## ⏱️ Estimativa: 4h
## Prioridade: Alta" \
  "fase,tipo/testes,prioridade:alta" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q4: FASE 20 - Corrigir MyPy global" \
"## 🎯 Objetivo
Eliminar todos os erros de MyPy do projeto

## 📊 Métricas Atuais
- **Total de erros:** 6
- **Arquivos afetados:** 
  - `estatisticas.py` (3 erros)
  - `config/__init__.py` (1 erro - yaml)
  - `sqlite_repository.py` (2 erros)

## 📋 Tarefas
- [ ] Adicionar type hints nos Counters de `estatisticas.py`
- [ ] Instalar stubs: `poetry add --dev types-PyYAML`
- [ ] Corrigir tipos em `sqlite_repository.py`
- [ ] Verificar com `poetry run mypy src/`

## 📊 Definição de Pronto
- [ ] `poetry run mypy src/` retorna 0 erros

## ⏱️ Estimativa: 2h
## Prioridade: Alta" \
  "fase,tipo/qualidade,prioridade:alta" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q5: Adicionar testes de integração para repositórios SQLite" \
"## 🎯 Objetivo
Garantir que as queries SQL funcionem com banco real.

## 📋 Tarefas
- [ ] Criar testes com banco temporário
- [ ] Testar `sqlite_repository.py` com dados reais
- [ ] Testar `sqlite_traducao_repository.py`
- [ ] Testar migrations

## 📊 Definição de Pronto
- [ ] Testes passando
- [ ] Cobertura dos repositórios >= 80%

## ⏱️ Estimativa: 3h
## Prioridade: Média" \
  "test,prioridade:media" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q6: Aumentar cobertura global para 80%+" \
"## 🎯 Objetivo
Garantir que todo o código tenha cobertura mínima.

## 📋 Tarefas
- [ ] Mapear arquivos com cobertura <80%
- [ ] Priorizar por impacto
- [ ] Criar testes faltantes
- [ ] Verificar cobertura final

## 📊 Definição de Pronto
- [ ] Cobertura global >= 80%

## ⏱️ Estimativa: 4h
## Prioridade: Média" \
  "test,prioridade:media" \
  "QUALIDADE E TESTES (Semanas 3-4)"

create_issue "Q7: Adicionar property-based testing com Hypothesis" \
"## 🎯 Objetivo
Testar propriedades invariantes com geração automática de dados.

## 📋 Tarefas
- [ ] Adicionar Hypothesis: `poetry add --dev hypothesis`
- [ ] Identificar funções com propriedades testáveis
- [ ] Escrever testes para `NomeRusso`
- [ ] Escrever testes para `TipoDocumento`
- [ ] Escrever testes para cálculos estatísticos

## 📊 Definição de Pronto
- [ ] Testes com Hypothesis passando
- [ ] Documentação de exemplos

## ⏱️ Estimativa: 3h
## Prioridade: Baixa" \
  "test,prioridade:baixa" \
  "QUALIDADE E TESTES (Semanas 3-4)"

# =============================================
# MILESTONE 3: DEPENDÊNCIAS E INFRA (Semanas 5-6)
# =============================================
echo "📌 MILESTONE 3: DEPENDÊNCIAS E INFRA (5 issues)"
echo "------------------------------------------------"

create_issue "D1: Migrar dependências NLP para Poetry" \
"## 🎯 Objetivo
Substituir instalação via pip por dependências gerenciadas pelo Poetry.

## 🔗 Referência
Issue #1 - Migrar dependências NLP para Poetry

## 📋 Tarefas
- [ ] Pesquisar versões compatíveis
- [ ] Testar combinações em branch separada
- [ ] Atualizar `pyproject.toml`
- [ ] Atualizar `poetry.lock`
- [ ] Remover etapas de pip do CI
- [ ] Atualizar documentação

## 📊 Definição de Pronto
- [ ] `poetry install` instala tudo
- [ ] CI sem etapas de pip
- [ ] Testes passam

## ⏱️ Estimativa: 4h
## Prioridade: Alta" \
  "tipo/infra,prioridade:alta" \
  "DEPENDÊNCIAS E INFRA (Semanas 5-6)"

create_issue "D2: Instalar stubs para módulos externos" \
"## 🎯 Objetivo
Eliminar erros de MyPy relacionados a módulos sem stubs.

## 📋 Tarefas
- [ ] `poetry add --dev types-PyYAML`
- [ ] `poetry add --dev types-requests`
- [ ] Verificar outros módulos
- [ ] Atualizar CI se necessário

## 📊 Definição de Pronto
- [ ] Erros de import resolvidos

## ⏱️ Estimativa: 30min
## Prioridade: Média" \
  "tipo/qualidade,prioridade:media" \
  "DEPENDÊNCIAS E INFRA (Semanas 5-6)"

create_issue "D3: Atualizar CI para usar Poetry completamente" \
"## 🎯 Objetivo
Simplificar o workflow do GitHub Actions.

## 📋 Tarefas
- [ ] Remover etapas manuais de pip (após D1)
- [ ] Otimizar cache
- [ ] Adicionar step de verificação
- [ ] Testar execução

## 📊 Definição de Pronto
- [ ] CI mais rápido e limpo

## ⏱️ Estimativa: 2h
## Prioridade: Média" \
  "tipo/infra,prioridade:media" \
  "DEPENDÊNCIAS E INFRA (Semanas 5-6)"

create_issue "D4: Adicionar cache mais eficiente no CI" \
"## 🎯 Objetivo
Acelerar as execuções do GitHub Actions.

## 📋 Tarefas
- [ ] Cache do Poetry mais granular
- [ ] Cache dos modelos spaCy
- [ ] Cache do pip (se ainda usado)
- [ ] Medir tempo antes/depois

## 📊 Definição de Pronto
- [ ] Redução de tempo >= 30%

## ⏱️ Estimativa: 1h
## Prioridade: Baixa" \
  "tipo/infra,prioridade:baixa" \
  "DEPENDÊNCIAS E INFRA (Semanas 5-6)"

create_issue "D5: Dockerizar aplicação (CLI + Web)" \
"## 🎯 Objetivo
Facilitar deploy e execução em qualquer ambiente.

## 📋 Tarefas
- [ ] Criar Dockerfile para CLI
- [ ] Criar Dockerfile para Web (com uvicorn)
- [ ] Criar docker-compose.yml
- [ ] Documentar uso

## 📊 Definição de Pronto
- [ ] `docker-compose up` funciona
- [ ] Documentação atualizada

## ⏱️ Estimativa: 4h
## Prioridade: Baixa" \
  "feat,prioridade:baixa" \
  "DEPENDÊNCIAS E INFRA (Semanas 5-6)"

# =============================================
# MILESTONE 4: NOVAS FUNCIONALIDADES (Semanas 7-8)
# =============================================
echo "📌 MILESTONE 4: NOVAS FUNCIONALIDADES (6 issues)"
echo "-------------------------------------------------"

create_issue "N1: Melhoria - Modo escuro no CLI" \
"## 🎯 Objetivo
Adicionar suporte a modo escuro na interface CLI.

## 📋 Tarefas
- [ ] Criar tema escuro no `console.py`
- [ ] Adicionar flag `--dark-mode`
- [ ] Permitir alternância durante execução
- [ ] Documentar no help

## 🔗 Referência
- [Rich Themes](https://rich.readthedocs.io/en/stable/appendix/colors.html)

## ⏱️ Estimativa: 2h
## Prioridade: Baixa" \
  "melhoria,ux,prioridade:baixa" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

create_issue "N2: Melhoria - Gráficos no terminal" \
"## 🎯 Objetivo
Adicionar gráficos de barras no CLI usando plotext.

## 📋 Tarefas
- [ ] Adicionar `plotext` como dependência
- [ ] Criar presenter para gráficos
- [ ] Integrar com estatísticas
- [ ] Adicionar comando `--grafico`

## 🔗 Referência
- [plotext](https://github.com/piccolomo/plotext)

## ⏱️ Estimativa: 3h
## Prioridade: Média" \
  "melhoria,ux,prioridade:media" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

create_issue "N3: API REST documentada com OpenAPI/Swagger" \
"## 🎯 Objetivo
Disponibilizar API pública para integrações.

## 📋 Tarefas
- [ ] Revisar endpoints existentes
- [ ] Adicionar docstrings OpenAPI
- [ ] Configurar Swagger UI
- [ ] Testar com curl/Postman

## ⏱️ Estimativa: 4h
## Prioridade: Média" \
  "feat,prioridade:media" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

create_issue "N4: Exportação para PDF" \
"## 🎯 Objetivo
Implementar exportação de documentos para PDF.

## 📋 Tarefas
- [ ] Pesquisar bibliotecas (ReportLab, WeasyPrint)
- [ ] Criar caso de uso `exportar_pdf`
- [ ] Adicionar template de PDF
- [ ] Integrar com CLI e Web

## ⏱️ Estimativa: 4h
## Prioridade: Média" \
  "feat,prioridade:media" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

create_issue "N5: Busca global no acervo" \
"## 🎯 Objetivo
Permitir busca textual em todos os documentos.

## 📋 Tarefas
- [ ] Adicionar índice FTS no SQLite
- [ ] Criar caso de uso `buscar_documentos`
- [ ] Adicionar comando CLI `buscar`
- [ ] Adicionar endpoint REST `/busca`

## ⏱️ Estimativa: 3h
## Prioridade: Baixa" \
  "feat,prioridade:baixa" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

create_issue "N6: Cache com Redis para análises frequentes" \
"## 🎯 Objetivo
Melhorar performance de análises repetidas.

## 📋 Tarefas
- [ ] Adicionar Redis como dependência opcional
- [ ] Criar decorator de cache
- [ ] Aplicar em `analisar_acervo`
- [ ] Configurar TTL

## ⏱️ Estimativa: 4h
## Prioridade: Baixa" \
  "feat,prioridade:baixa" \
  "NOVAS FUNCIONALIDADES (Semanas 7-8)"

# =============================================
# MILESTONE 5: DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)
# =============================================
echo "📌 MILESTONE 5: DOCUMENTAÇÃO E FINALIZAÇÃO (5 issues)"
echo "-----------------------------------------------------"

create_issue "R1: Revisar documentação (.md files)" \
"## 🎯 Objetivo
Consolidar e revisar todos os arquivos de documentação.

## 🔗 Referência
Issue #2 - Revisar documentação (.md files)

## 📋 Tarefas
- [ ] Verificar duplicatas (cobertura.md vs cobertura_v2.md)
- [ ] Atualizar índices
- [ ] Garantir que todas as fases estão documentadas
- [ ] Fazer merge da branch `docs/organizacao`

## ⏱️ Estimativa: 3h
## Prioridade: Alta" \
  "tipo/documentação,prioridade:alta" \
  "DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"

create_issue "R2: Atualizar todas as FASE*.md com resultados finais" \
"## 🎯 Objetivo
Garantir que cada fase tenha sua documentação completa.

## 📋 Tarefas
- [ ] Revisar FASE 1-16
- [ ] Adicionar métricas finais
- [ ] Verificar links
- [ ] Padronizar formatação

## ⏱️ Estimativa: 4h
## Prioridade: Alta" \
  "docs,prioridade:alta" \
  "DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"

create_issue "R3: Criar apresentação do TCC (slides)" \
"## 🎯 Objetivo
Preparar slides para apresentação final.

## 📋 Tarefas
- [ ] Definir estrutura
- [ ] Criar slides de introdução
- [ ] Mostrar arquitetura
- [ ] Demonstrar funcionalidades
- [ ] Resultados e métricas
- [ ] Conclusão

## ⏱️ Estimativa: 6h
## Prioridade: Alta" \
  "docs,prioridade:alta" \
  "DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"

create_issue "R4: Preparar vídeo de demonstração" \
"## 🎯 Objetivo
Gravar vídeo mostrando o sistema em funcionamento.

## 📋 Tarefas
- [ ] Roteiro
- [ ] Gravar CLI
- [ ] Gravar Web
- [ ] Editar
- [ ] Adicionar narração

## ⏱️ Estimativa: 3h
## Prioridade: Média" \
  "docs,prioridade:media" \
  "DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"

create_issue "R5: Revisar e publicar versão final (v1.0.0)" \
"## 🎯 Objetivo
Preparar release final para entrega do TCC.

## 📋 Tarefas
- [ ] Verificar CHANGELOG
- [ ] Atualizar versão no pyproject.toml
- [ ] Criar tag v1.0.0
- [ ] Criar release no GitHub
- [ ] Publicar documentação final

## ⏱️ Estimativa: 2h
## Prioridade: Alta" \
  "tipo/release,prioridade:alta" \
  "DOCUMENTAÇÃO E FINALIZAÇÃO (Contínuo)"

# =============================================
# RESUMO FINAL
# =============================================
echo ""
echo "====================================================="
echo "✅ SCRIPT CONCLUÍDO!"
echo "====================================================="
echo ""
echo "📊 RESUMO DAS ISSUES CRIADAS:"
echo ""
echo "   Milestone 1: FUNDAÇÃO ................ 6 issues"
echo "   Milestone 2: QUALIDADE ................ 7 issues"
echo "   Milestone 3: DEPENDÊNCIAS ............. 5 issues"
echo "   Milestone 4: NOVAS FUNCIONALIDADES .... 6 issues"
echo "   Milestone 5: DOCUMENTAÇÃO ............. 5 issues"
echo "   -----------------------------------------"
echo "   TOTAL ................................. 29 issues"
echo ""
echo "====================================================="
echo "📋 PRÓXIMOS PASSOS:"
echo ""
echo "1️⃣  Verifique os milestones no site:"
echo "   https://github.com/rib-thiago/showtrials-tcc/milestones"
echo ""
echo "2️⃣  Acesse o Project Kanban:"
echo "   https://github.com/users/rib-thiago/projects/1"
echo ""
echo "3️⃣  Adicione as issues ao Project:"
echo "   gh project item-add <NUMERO> --owner rib-thiago --url https://github.com/rib-thiago/showtrials-tcc/issues/<NUMERO>"
echo ""
echo "4️⃣  Comece pela F1 (flows) ou Q3 (estatisticas.py urgente)"
echo ""
echo "====================================================="
```

---

📋 INSTRUÇÕES PARA GERIR O BACKLOG

1. Após rodar o script

```bash
# Ver todas as issues criadas
gh issue list --state all

# Ver issues por milestone
gh issue list --milestone "FUNDAÇÃO (Semanas 1-2)"
gh issue list --milestone "QUALIDADE E TESTES (Semanas 3-4)"
# ... etc
```

2. Adicionar issues ao Project Kanban

```bash
# Primeiro, liste os projects para pegar o ID
gh project list --owner rib-thiago

# Para cada issue, adicione ao project (substitua NUMERO e PROJECT_ID)
gh project item-add 1 --owner rib-thiago --url https://github.com/rib-thiago/showtrials-tcc/issues/1
gh project item-add 2 --owner rib-thiago --url https://github.com/rib-thiago/showtrials-tcc/issues/2
# ... repita para todas as 29 issues

# Ou crie um loop (depois de pegar o PROJECT_ID)
for issue in {1..29}; do
    gh project item-add $issue --owner rib-thiago --url https://github.com/rib-thiago/showtrials-tcc/issues/$issue
done
```

3. Organizar o Kanban

No site do Project, arraste as issues para as colunas corretas:

Coluna Quais issues
📋 Backlog Todas as 29 issues (inicialmente)
✅ Ready As que você vai começar agora (ex: F1, Q3)
⏳ In Progress Quando começar a trabalhar
👀 In Review Se fizer PR (opcional)
✅ Done Quando concluídas

4. Prioridades iniciais sugeridas

```bash
# Mover para "Ready" primeiro:
- Q3: estatisticas.py (URGENTE - 15% cobertura)
- F1: Documentar flows
- F5: Branch protection
- Q1: classificar_documento.py
```

5. Fluxo diário de trabalho

```bash
# 1. Ver o que está em Ready
gh issue list --label "prioridade:alta" --state open

# 2. Pegar uma issue
git checkout -b type/classificar-documento  # ou fix/, docs/, etc.

# 3. Desenvolver
# ...

# 4. Commit com fechamento
git commit -m "feat: ... Closes #NUMERO"

# 5. Push e merge
git push origin type/classificar-documento
# (merge após CI passar)

# 6. No Kanban, mover issue para "Done"
```

---

🎯 RESUMO - O QUE VOCÊ TEM AGORA

Recurso Status
29 issues ✅ Prontas para criar
5 milestones ✅ Com datas sugeridas
Project Kanban ✅ Já configurado
Labels ✅ 10+ disponíveis
Fluxo de trabalho ✅ Documentado

Quer que eu execute o script para você ou prefere criar manualmente? 🚀

CRAFTEXT - Documento de Contexto Completo da Aplicação

<div align="center">Plataforma de Pipeline Configurável para Processamento de Documentos

Versão: 1.0
Data: 04/03/2026
Autor: Thiago Ribeiro

</div>---

Sumário

1. Visão Geral do Projeto
2. Stack Tecnológico
3. Arquitetura de Software
4. Modelo de Domínio
5. Sistema de Plugins
6. Estrutura de Diretórios
7. Dependências e Configuração
8. Qualidade e Testes
9. Git e GitHub
10. Evolução do Projeto
11. Roadmap Futuro
12. Glossário

---

1. Visão Geral do Projeto

1.1 Propósito

CraftText é uma plataforma de pipeline configurável para extração, processamento e análise de documentos. O projeto nasceu da necessidade de centralizar fluxos de trabalho que antes eram realizados com múltiplos scripts e ferramentas isoladas.

A plataforma permite que pesquisadores e usuários em geral construam seus próprios pipelines combinando diferentes fontes de dados, processadores e exportadores, de forma declarativa (via YAML) ou programática.

1.2 Princípios Fundamentais

Princípio Descrição
Configurabilidade Usuário escolhe quais ferramentas usar e como configurá-las
Extensibilidade Arquitetura de plugins para fontes, processadores e exportadores
Testabilidade Código estruturado para testes isolados (injeção de dependência)
Documentação como Código Tudo documentado, versionado e automatizado
Clean Architecture Separação clara entre domínio, aplicação, infraestrutura e interface
Qualidade como Critério de Aceite Cobertura ≥85%, type hints, linting obrigatórios

1.3 Público-Alvo

· Pesquisadores que precisam processar grandes volumes de documentos
· Usuários interessados em extrair informação de PDFs, imagens (OCR) e sites
· Desenvolvedores que desejam estender a plataforma com novos plugins
· Público geral com necessidades de automação de processamento de texto

1.4 Estado Atual (Março/2026)

Métrica Valor
Versão 0.2.0
Issues abertas 13
Issues fechadas 4
Pull Requests 1 (em revisão)
Milestone ativo MVP - Engine de Pipeline
Issues no milestone 11
Arquivos de domínio 11
Arquivos de aplicação 17
Arquivos de infraestrutura 20
Arquivos de interface 24

---

2. Stack Tecnológico

2.1 Core

Tecnologia Versão Uso Instalação
Python ≥3.12, <3.14 Linguagem principal Poetry
Poetry ^2.0.0 Gerenciamento de dependências pip install poetry
SQLite 3.x Banco de dados padrão Embutido no Python

2.2 Interface CLI

Tecnologia Versão Uso
Rich ≥13.7.0 Interface rica no terminal (tabelas, cores, spinners)
Click (futuro) - Parser de comandos CLI

2.3 Interface Web

Tecnologia Versão Uso
FastAPI ^0.129.0 API REST e servidor web
Uvicorn ^0.40.0 Servidor ASGI
Jinja2 ^3.1.6 Templates HTML
Bootstrap 5 CSS Framework
Chart.js 4 Gráficos interativos

2.4 NLP e Análise

Tecnologia Versão Uso Status
spaCy 3.7.5 NLP, NER, tokenização pip (temporário)
NumPy 1.26.0 Computação numérica pip (temporário)
TextBlob latest Análise de sentimento pip (temporário)
NLTK latest NLP clássico pip (temporário)
WordCloud latest Nuvens de palavras pip (temporário)
Matplotlib latest Gráficos pip (temporário)

Nota: Dependências NLP estão temporariamente no pip devido a conflitos de versão. Issue #1 acompanha a migração para Poetry.

2.5 Modelos de NLP

Modelo Idioma Uso Instalação
pt_core_news_sm Português NER, tokenização spacy download
en_core_web_sm Inglês NER, tokenização spacy download
ru_core_news_sm Russo NER, tokenização spacy download

2.6 Qualidade e Testes

Tecnologia Versão Uso
pytest ^9.0.0 Testes unitários
pytest-cov ^7.0.0 Cobertura de testes
mypy ^1.19.1 Type checking
ruff ^0.15.1 Linting (substituto do flake8)
black ^26.1.0 Formatação automática
isort ^7.0.0 Organização de imports

2.7 Documentação

Tecnologia Versão Uso
MkDocs ^1.6.1 Gerador de site de documentação
MkDocs Material ^9.7.1 Tema para documentação
mkdocstrings ^1.0.3 Documentação automática a partir de docstrings

2.8 Automação

Tecnologia Versão Uso
Taskipy ^1.14.1 Automação de tarefas (substituto do Make)
GitHub Actions - CI/CD
Commitizen ^4.13.7 Commits semânticos

---

3. Arquitetura de Software

3.1 Clean Architecture

O projeto segue rigorosamente os princípios da Clean Architecture (Robert C. Martin), com 4 camadas independentes:

```
┌─────────────────────────────────────────────────────────────┐
│                    INTERFACE LAYER                           │
│  (CLI, Web, API - adaptadores para o mundo externo)        │
│  • Comandos CLI com Rich                                     │
│  • Rotas FastAPI                                             │
│  • Templates Jinja2                                          │
│  • Presenters para formatação                                │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   APPLICATION LAYER                          │
│  (Casos de uso, orquestração, DTOs)                         │
│  • ExecutarPipeline                                          │
│  • ListarPipelines                                           │
│  • ExportarDocumento                                         │
│  • DocumentoDTO, PipelineDTO                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      DOMAIN LAYER                            │
│  (Entidades, Value Objects, regras de negócio)              │
│  • Entidades: Documento, Pipeline, Traducao                  │
│  • Value Objects: PipelineStep, TipoDocumento, NomeRusso    │
│  • Interfaces: SourcePlugin, ProcessorPlugin, ExporterPlugin │
│  • Sem dependências externas                                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                  INFRASTRUCTURE LAYER                        │
│  (Implementações concretas, plugins, serviços)              │
│  • PluginManager (registry com lazy loading)                 │
│  • Repositórios SQLite                                       │
│  • Configuração YAML                                         │
│  • Adaptadores: GoogleTranslate, spaCy, Tesseract           │
└─────────────────────────────────────────────────────────────┘
```

3.2 Princípios Arquiteturais Aplicados

Princípio Aplicação
Dependency Inversion Camadas internas definem interfaces; externas implementam
Single Responsibility Cada classe tem uma única responsabilidade
Open/Closed Novo comportamento via plugins, não modificação do core
Liskov Substitution Plugons podem substituir suas interfaces
Interface Segregation Interfaces específicas para cada tipo de plugin

3.3 Service Registry e Lazy Loading

```python
# Exemplo conceitual do PluginManager
class PluginManager:
    _services: Dict[str, ServiceInfo]
    _instances: Dict[str, Any]
    
    def register(self, name, factory, lazy=True):
        self._services[name] = ServiceInfo(factory, lazy)
    
    def get(self, name):
        if name not in self._instances:
            self._instances[name] = self._services[name].factory()
        return self._instances[name]
```

Benefícios:

· ✅ Carregamento sob demanda (lazy loading)
· ✅ Configuração centralizada via YAML
· ✅ Estatísticas de uso
· ✅ Cache de instâncias

---

4. Modelo de Domínio

4.1 Entidades Principais

Documento

```python
@dataclass
class Documento:
    """Representa um documento processado pelo sistema."""
    
    id: Optional[int]
    titulo: str
    texto: str
    metadados: Dict[str, Any]  # entidades, classificações, etc.
    fonte: str                  # URL, arquivo, etc.
    data_coleta: datetime
    idioma_original: Optional[str]
    traducoes: List[Traducao]   # lazy loading via repositório
```

Pipeline

```python
@dataclass
class Pipeline:
    """Pipeline configurável com steps em sequência."""
    
    id: Optional[int]
    nome: str
    descricao: Optional[str]
    steps: List[PipelineStep]
    created_at: datetime
    updated_at: datetime
    
    def adicionar_step(self, step: PipelineStep) -> None:
        """Adiciona step validando ordem."""
        # Validação...
        
    def validar(self) -> bool:
        """Valida se pipeline é executável."""
        return all(s.validar() for s in self.steps)
```

PipelineStep (Value Object)

```python
@dataclass(frozen=True)
class PipelineStep:
    """Um passo atômico no pipeline (imutável)."""
    
    ordem: int
    tipo: str  # 'source', 'processor', 'exporter'
    plugin: str  # nome do plugin registrado
    config: Dict[str, Any]  # configuração específica do passo
```

Traducao

```python
@dataclass
class Traducao:
    """Tradução de um documento para outro idioma."""
    
    id: Optional[int]
    documento_id: int
    idioma: str  # 'pt', 'en', 'ru', 'es', 'fr'
    texto_traduzido: str
    modelo: Optional[str]  # 'google', 'libre', 'huggingface'
    custo: float
    data_traducao: datetime
```

4.2 Value Objects Existentes (Legado)

```python
@dataclass(frozen=True)
class TipoDocumento(Enum):
    """Classificação específica dos processos históricos."""
    INTERROGATORIO = "interrogatorio"
    ACAREACAO = "acareacao"
    ACUSACAO = "acusacao"
    # ... outros tipos
    
@dataclass(frozen=True)
class NomeRusso:
    """Valida e translitera nomes russos."""
    nome: str
    
    def transliterar(self) -> str:
        """Converte para o formato ocidental."""
        # Tabela GOST 7.79-2000
```

4.3 Contratos de Plugins

```python
class SourcePlugin(ABC):
    """Fonte de dados: coleta documentos."""
    
    @abstractmethod
    def nome(self) -> str:
        """Nome único do plugin."""
        pass
    
    @abstractmethod
    def descricao(self) -> str:
        """Descrição para interface do usuário."""
        pass
    
    @abstractmethod
    def config_schema(self) -> Dict:
        """Schema JSON para validação da configuração."""
        pass
    
    @abstractmethod
    def coletar(self, config: Dict) -> List[Documento]:
        """Coleta documentos conforme configuração."""
        pass

class ProcessorPlugin(ABC):
    """Processador: transforma/enriquece documentos."""
    
    @abstractmethod
    def processar(self, documento: Documento, config: Dict) -> Documento:
        """Processa um documento e retorna versão enriquecida."""
        pass

class ExporterPlugin(ABC):
    """Exportador: persiste/exporta documentos."""
    
    @abstractmethod
    def exportar(self, documentos: List[Documento], config: Dict) -> str:
        """Exporta documentos e retorna caminho/localização."""
        pass
```

---

5. Sistema de Plugins

5.1 Fontes (Sources)

Plugin Descrição Configuração
web_scraper Coleta de sites com paginação URL, seletores CSS, limite de páginas
folder_source Arquivos locais (txt, md, csv) Caminho, recursivo, extensões
pdf_source Extração de PDFs Modo (texto/ocr), idiomas OCR
ocr_source OCR de imagens (Tesseract) Idiomas, pré-processamento, DPI

5.2 Processadores (Processors)

Plugin Descrição Configuração
rule_classifier Classificação por regras customizáveis Regras em YAML, modo (primeiro/múltiplo)
ner_extractor Extração de entidades (PERSON, ORG, LOC, DATE) Modelo spaCy, tipos, confiança mínima
translator Tradução com múltiplos backends Backend (google/libre/huggingface), idiomas, API key
sentiment_analyzer Análise de sentimento Modelo, idioma
summarizer Sumarização automática Tamanho do resumo, método

5.3 Exportadores (Exporters)

Plugin Descrição Configuração
sqlite_exporter Persistência em banco SQLite Caminho, tabela, modo (substituir/adicionar)
csv_exporter Exportação para planilhas Delimitador, colunas, cabeçalho
json_exporter Exportação para JSON Indentação, encoding
txt_exporter Documentos individuais Pasta destino, nome do arquivo

5.4 Plugin Manager

```python
# Exemplo de uso
manager = PluginManager.get_instance()

# Registrar plugins (feito na inicialização)
manager.register('web_scraper', WebScraperPlugin, lazy=True)
manager.register('rule_classifier', RuleClassifierPlugin, lazy=True)
manager.register('sqlite_exporter', SQLiteExporterPlugin, lazy=True)

# Usar (lazy loading)
source = manager.get('web_scraper')
documentos = source.coletar(config)
```

---

6. Estrutura de Diretórios

```
crafttext/                          # Raiz do projeto
├── .github/
│   └── workflows/                   # GitHub Actions
│       ├── ci.yml                    # Pipeline de CI
│       └── publish.yml                # Publicação no PyPI
│
├── docs/                             # Documentação (MkDocs)
│   ├── fases/                         # FASE*.md do desenvolvimento
│   │   ├── FASE1_DOMAIN.md
│   │   ├── FASE2_APPLICATION.md
│   │   └── ... (17 fases)
│   ├── flows/                          # Flows de processo
│   │   ├── git_flow.md
│   │   ├── quality_flow.md
│   │   ├── telemetry_flow.md
│   │   ├── code_review_flow.md
│   │   ├── debug_flow.md
│   │   ├── dependencies_flow.md
│   │   ├── documentation_flow.md
│   │   ├── emergency_flow.md
│   │   ├── fluxo_projects_github_cli.md
│   │   ├── refactoring_flow.md
│   │   └── GOVERNANCA.md
│   ├── metricas/                       # Diagnósticos e métricas
│   │   ├── cobertura.md
│   │   ├── diagnostico_ci.md
│   │   └── diagnostico_fase12.md
│   ├── projeto/                         # Documentos de visão e planejamento
│   │   ├── analise_arquitetural.md
│   │   ├── direcionamento_arquitetural_engine_mvp.md
│   │   ├── manual_gestao.md
│   │   ├── roadmap_arquitetural.md
│   │   └── visao_do_projeto.md
│   ├── planejamento/                     # Templates e planos
│   │   ├── TEMPLATE_FASE.md
│   │   └── plano_issue2_revisao_documentacao.md
│   ├── ARCHITECTURE.md
│   ├── index.md
│   ├── overview.md
│   └── mkdocs.yml
│
├── src/                               # Código fonte
│   ├── domain/                          # Camada de domínio
│   │   ├── entities/                      # Entidades
│   │   │   ├── documento.py
│   │   │   ├── pipeline.py
│   │   │   └── traducao.py
│   │   ├── value_objects/                  # Value Objects
│   │   │   ├── pipeline_step.py
│   │   │   ├── tipo_documento.py
│   │   │   └── nome_russo.py
│   │   └── interfaces/                      # Contratos
│   │       ├── plugins.py
│   │       ├── repositories.py
│   │       └── repositorio_traducao.py
│   │
│   ├── application/                       # Camada de aplicação
│   │   ├── dtos/                             # Data Transfer Objects
│   │   │   ├── documento_dto.py
│   │   │   ├── pipeline_dto.py
│   │   │   └── traducao_dto.py
│   │   └── use_cases/                        # Casos de uso
│   │       ├── pipeline/
│   │       │   ├── executar_pipeline.py
│   │       │   ├── criar_pipeline.py
│   │       │   └── listar_pipelines.py
│   │       ├── documentos/
│   │       │   ├── listar_documentos.py
│   │       │   ├── exportar_documento.py
│   │       │   └── classificar_documento.py
│   │       └── analise/
│   │           ├── analisar_texto.py
│   │           └── analisar_acervo.py
│   │
│   ├── infrastructure/                     # Camada de infraestrutura
│   │   ├── config/                            # Configurações
│   │   │   ├── __init__.py
│   │   │   └── settings.py
│   │   ├── persistence/                        # Repositórios
│   │   │   ├── models.py
│   │   │   ├── migrations.py
│   │   │   ├── sqlite_repository.py
│   │   │   └── sqlite_traducao_repository.py
│   │   ├── plugins/                            # Implementação dos plugins
│   │   │   ├── sources/
│   │   │   │   ├── web_scraper.py
│   │   │   │   ├── folder_source.py
│   │   │   │   ├── pdf_source.py
│   │   │   │   └── ocr_source.py
│   │   │   ├── processors/
│   │   │   │   ├── classifier.py
│   │   │   │   ├── ner.py
│   │   │   │   └── translator.py
│   │   │   └── exporters/
│   │   │       ├── sqlite.py
│   │   │       ├── csv.py
│   │   │       ├── json.py
│   │   │       └── txt.py
│   │   ├── analysis/                           # Análise de texto
│   │   │   ├── spacy_analyzer.py
│   │   │   └── wordcloud_generator.py
│   │   ├── translation/                         # Tradução
│   │   │   └── google_translator.py
│   │   ├── registry.py                           # Plugin Manager
│   │   ├── factories.py                           # Factories para serviços
│   │   └── telemetry/                             # Telemetria
│   │       └── __init__.py
│   │
│   └── interface/                            # Interfaces com usuário
│       ├── cli/                                  # Interface de linha de comando
│       │   ├── app.py
│       │   ├── commands.py
│       │   ├── commands_pipeline.py
│       │   ├── commands_analise.py
│       │   ├── commands_export.py
│       │   ├── commands_relatorio.py
│       │   ├── commands_traducao.py
│       │   ├── menu.py
│       │   ├── presenters.py
│       │   └── presenters_analise.py
│       └── web/                                   # Interface web
│           ├── app.py
│           ├── routes/
│           │   ├── documentos.py
│           │   ├── pipelines.py
│           │   ├── analise.py
│           │   ├── traducoes.py
│           │   ├── estatisticas.py
│           │   └── admin.py
│           ├── templates/
│           │   ├── base.html
│           │   ├── index.html
│           │   ├── pipelines/
│           │   └── documentos/
│           └── static/
│               ├── css/
│               └── js/
│
├── tests/                                # Testes
│   ├── test_domain/
│   ├── test_application/
│   ├── test_infrastructure/
│   └── test_interface/
│
├── scripts/                              # Scripts auxiliares
│   ├── diagnostico.sh
│   ├── diagnostico_ci.sh
│   ├── diagnostico_limpeza.sh
│   ├── migrar_dados_existentes.py
│   ├── reprocessar_metadados.py
│   └── verificar_fases.py
│
├── examples/                             # Exemplos de pipeline
│   ├── web_scraper.yaml
│   ├── pdf_ocr.yaml
│   └── classificacao.yaml
│
├── data/                                 # Banco de dados
│   └── showtrials.db                       # 519 documentos
│
├── pyproject.toml                        # Configuração do Poetry
├── poetry.lock                            # Lock de dependências
├── README.md                              # Apresentação do projeto
├── run.py                                 # Entry point CLI
├── web_run.py                             # Entry point web
├── config.yaml                            # Configuração da aplicação
├── mkdocs.yml                             # Configuração da documentação
└── coletar_info_projeto.sh                 # Script de diagnóstico
```

---

7. Dependências e Configuração

7.1 pyproject.toml (Completo)

```toml
[tool.poetry]
name = "coleta-showtrials"
version = "0.2.0"
description = "Sistema de coleta, gestão e tradução de documentos históricos"
authors = ["Thiago Ribeiro <mackandalls@gmail.com>"]
readme = "README.md"
packages = [{include = "src"}]

[tool.poetry.dependencies]
python = ">=3.12,<3.14"
requests = ">=2.32.5"
beautifulsoup4 = ">=4.14.3"
lxml = ">=6.0.2"
rich = ">=13.7.0"
google-cloud-translate = ">=3.0.0"
python-dotenv = ">=1.0.0"
pytest = ">=9.0.0"
fastapi = "^0.129.0"
uvicorn = "^0.40.0"
jinja2 = "^3.1.6"
aiofiles = "^25.1.0"
python-multipart = "^0.0.22"

[tool.poetry.group.dev.dependencies]
black = "^26.1.0"
isort = "^7.0.0"
ruff = "^0.15.1"
pre-commit = "^4.5.1"
pytest-cov = "^7.0.0"
mkdocs = "^1.6.1"
mkdocstrings = "^1.0.3"
mkdocs-material = "^9.7.1"
mkdocstrings-python = "^2.0.2"
commitizen = "^4.13.7"
taskipy = "^1.14.1"
mypy = "^1.19.1"

[build-system]
requires = ["poetry-core>=2.0.0,<3.0.0"]
build-backend = "poetry.core.masonry.api"

[tool.pytest.ini_options]
pythonpath = ["src"]
addopts = "-v --cov=src --cov-report=term-missing"

[tool.black]
line-length = 100
target-version = ['py312']

[tool.isort]
profile = "black"
line_length = 100

[tool.ruff]
line-length = 100
select = ["E", "F", "I", "B"]
ignore = []

[tool.commitizen]
name = "cz_conventional_commits"
version = "0.2.0"
tag_format = "v$version"
```

7.2 Taskipy Tasks

```toml
[tool.taskipy.tasks]
# === Qualidade ===
lint = "ruff check src"
type = "mypy src"
format = "black src && isort src"
quality = "task lint && task type"

# === Testes ===
test = "pytest src/tests -v"
test-cov = "pytest src/tests --cov=src --cov-report=term-missing --cov-fail-under=45"
test-html = "pytest src/tests --cov=src --cov-report=html"

# === Telemetria ===
metrics = "python -c 'from src.infrastructure.telemetry import telemetry; telemetry.flush()'"
monitor = "task test && task metrics"

# === Execução ===
run-cli = "python run.py"
run-web = "python web_run.py"

# === Manutenção ===
clean = "find . -type d -name __pycache__ -exec rm -rf {} + && find . -name '*.pyc' -delete"
docs = "mkdocs serve"

# === Tudo junto ===
check = "task lint && task type && task test"
pre-push = "task check && task test-cov"
help = "task --list"
```

7.3 Configuração YAML

```yaml
# config.yaml
environment: development
debug: true

services:
  translator:
    default_backend: "libre"
    backends:
      google:
        api_key: ${GOOGLE_TRANSLATE_API_KEY}
      libre:
        url: ${LIBRETRANSLATE_URL}
  
  spacy:
    models:
      pt: "pt_core_news_sm"
      en: "en_core_web_sm"
      ru: "ru_core_news_sm"
    lazy_loading: true
  
  wordcloud:
    default_size: [800, 400]
    max_words: 200
    background_color: white
```

7.4 Variáveis de Ambiente

Variável Descrição Obrigatória Padrão
CRAFTEXT_ENV Ambiente (dev/prod) Não development
CRAFTEXT_DEBUG Modo debug Não false
CRAFTEXT_DB_PATH Caminho do banco Não ./data/crafttext.db
GOOGLE_TRANSLATE_API_KEY Chave do Google Tradutor Para backend Google -
LIBRETRANSLATE_URL URL do LibreTranslate Para backend Libre http://localhost:5000
TESSERACT_PATH Caminho do Tesseract OCR Não auto-detect

---

8. Qualidade e Testes

8.1 Padrões de Qualidade Obrigatórios

Categoria Critério Ferramenta
Formatação Código formatado black, isort
Linting Sem erros de estilo ruff
Type Hints Todos os parâmetros/retornos tipados mypy
Cobertura ≥85% por arquivo pytest-cov
Testes Testes de lógica + telemetria pytest
Commits Convencionais commitizen

8.2 Telemetria (Padrão Obrigatório)

Todo arquivo deve ter o template de telemetria no topo:

```python
# Telemetria opcional
_telemetry = None

def configure_telemetry(telemetry_instance=None):
    """Configura telemetria para este módulo (usado apenas em testes)."""
    global _telemetry
    _telemetry = telemetry_instance
```

Uso em métodos:

```python
def meu_metodo(self, parametro):
    if _telemetry:
        _telemetry.increment("modulo.metodo.iniciado")
        _telemetry.increment(f"modulo.metodo.parametro.{parametro}")
    
    try:
        # lógica...
        if _telemetry:
            _telemetry.increment("modulo.metodo.concluido")
        return resultado
    except ValueError:
        if _telemetry:
            _telemetry.increment("modulo.metodo.erro.valor_invalido")
        raise
```

Nomenclatura: modulo.submodulo.operacao.estado

8.3 Testes de Telemetria

Todo arquivo com telemetria deve ter um arquivo test_*_telemetry.py:

```python
class TestMeuModuloTelemetry:
    def setup_method(self):
        uc_module._telemetry = None
    
    def test_telemetria_sucesso(self):
        mock_telemetry = MagicMock()
        uc_module.configure_telemetry(mock_telemetry)
        
        # execução...
        
        mock_telemetry.increment.assert_any_call("modulo.metodo.iniciado")
        mock_telemetry.increment.assert_any_call("modulo.metodo.concluido")
```

8.4 Comandos de Qualidade

```bash
# Verificar tudo (lint + type + test)
task check

# Verificar arquivo específico
task lint-file --path src/application/use_cases/meu_arquivo.py
task type-file --path src/application/use_cases/meu_arquivo.py
task test-file --path tests/test_meu_arquivo.py
task cov-file --path src/application/use_cases/meu_arquivo.py

# Gerar relatório HTML de cobertura
task test-html
# Depois abrir htmlcov/index.html
```

---

9. Git e GitHub

9.1 Estrutura de Branches

```
main (protegida, CI obrigatório)
├── type/*          # Novas funcionalidades (ex: type/transformer-contract)
├── fix/*           # Correções de bugs (ex: fix/id-none)
├── feature/*       # Melhorias (ex: feature/dark-mode)
├── docs/*          # Documentação (ex: docs/atualizar-readme)
└── infra/*         # Infraestrutura/CI (ex: infra/quality-pipeline)
```

9.2 Commits Semânticos

Formato: <tipo>: <descrição>

```
feat:     Nova funcionalidade
fix:      Correção de bug
docs:     Documentação
style:    Formatação (espaço, vírgula, etc.)
refactor: Refatoração sem mudar comportamento
test:     Adicionar/atualizar testes
chore:    Tarefas de manutenção (dependências, CI)
engine:   Mudanças na arquitetura de pipeline
```

Exemplo com fechamento de issue:

```bash
git commit -m "engine: define contrato de Transformer

- Cria classe abstrata Transformer
- Define métodos transformar() e nome()
- Adiciona testes de contrato

Closes #10"
```

9.3 Pull Requests

Template obrigatório:

```markdown
## 📋 Descrição
[Descrição clara da solução implementada]

## 🔗 Issue relacionada
Closes #N

## ✅ Critérios de Aceite
- [ ] Critério 1 atendido
- [ ] Critério 2 atendido

## 🏗️ Impacto Arquitetural
[Explicar impacto na arquitetura, se houver]

## 📊 Checklist Técnico
- [ ] Código respeita o modelo arquitetural
- [ ] Sem acoplamento indevido com persistência
- [ ] Transformadores permanecem puros
- [ ] Separação execução/configuração mantida
- [ ] Responsabilidade no módulo correto
- [ ] Nenhuma mudança fora de escopo
```

9.4 Labels Oficiais

Categoria Labels Descrição
Tipo type:engine Mudanças na engine de pipeline
 type:infra Infraestrutura, CI, dependências
 type:feature Novas funcionalidades
 type:docs Documentação
 type:refactor Refatoração
 type:bug Correção de bugs
Prioridade priority:P0 Bloqueia arquitetura (fazer agora)
 priority:P1 Necessária para milestone ativa
 priority:P2 Melhoria incremental (congelada)
Status strategic Parte da milestone ativa
 frozen Congelada até milestone terminar

9.5 Milestone Atual

```json
{
  "title": "MVP - Engine de Pipeline",
  "state": "open",
  "open_issues": 11,
  "closed_issues": 0,
  "description": "Construção da arquitetura base do sistema de pipeline configurável",
  "created_at": "2026-02-22T14:40:50Z"
}
```

Issues no milestone:

· #10 Engine: Definir contrato de Transformer (P0)
· #11 Engine: Definir contrato de Sink (P0)
· #12 Engine: Implementar ContextoPipeline (P0)
· #13 Engine: Implementar Executor mínimo (P0)
· #14 Engine: Pipeline configurável via YAML/JSON (P1)
· #15 Engine: Suporte a Iterable para streaming (P1)
· #16 Engine: Versionamento incremental de pipeline (P1)
· #17 Engine: Migrar 1 caso de uso real (P1)
· #6 Infra: Consolidar pipeline de qualidade (P1)

9.6 Comandos GitHub CLI Úteis

```bash
# Issues
gh issue list                      # Listar abertas
gh issue list --state all           # Todas
gh issue view 10                    # Ver detalhes
gh issue edit 10 --milestone "MVP - Engine de Pipeline"

# Pull Requests
gh pr list                          # Listar PRs
gh pr view 18                        # Ver PR #18
gh pr review 18 --approve             # Aprovar
gh pr merge 18 --merge                 # Mergear

# Milestones
gh api repos/rib-thiago/showtrials-tcc/milestones
```

---

10. Evolução do Projeto

10.1 Fases Concluídas (17 fases)

Fase Título Descrição
FASE 1 Domain Layer Entidades, Value Objects, interfaces
FASE 2 Application Layer Casos de uso, DTOs
FASE 3 Infrastructure Layer Repositórios SQLite, migrações
FASE 4 CLI Interface CLI com Rich, menus interativos
FASE 5 Tradução Avançada Google Translate, persistência
FASE 6 Exportação Exportação TXT com metadados
FASE 7 Relatórios Estatísticas do acervo
FASE 8 Análise de Texto spaCy, NER, wordcloud
FASE 9 Web Interface FastAPI, templates, gráficos
FASE 10 Service Registry Lazy loading, configuração YAML
FASE 11 CI Stabilization Correção de dependências NLP no CI
FASE 12 Telemetry Padronização Unificação do padrão de telemetria
FASE 13 Limpeza do Repositório Remoção de arquivos obsoletos
FASE 14 ExportarDocumento Telemetria e testes (0% → 81%)
FASE 15 GerarRelatorio Telemetria e testes (0% → 86%)
FASE 16 ListarDocumentos Telemetria e testes (55% → 80%)
FASE 17 Documentação Consolidação e padronização dos docs

10.2 Padrão de Documentação das Fases

Toda FASE concluída segue o template em docs/planejamento/TEMPLATE_FASE.md com:

· 📅 Informações da fase (status, data, artefatos)
· 🎯 Objetivo
· 🔍 Estado inicial (métricas antes)
· 🛠️ Implementação realizada
· 🧪 Testes criados
· 📊 Resultados finais (métricas depois)
· 📝 Lições aprendidas

10.3 Flows de Processo (7 flows)

Flow Descrição
git_flow.md Estratégia de branches, commits, PRs, versionamento
quality_flow.md Critérios de qualidade (testes, cobertura, lint, mypy)
telemetry_flow.md Padrão de instrumentação com telemetria
code_review_flow.md Checklist de auto-revisão antes do merge
debug_flow.md Metodologia para depuração de problemas
dependencies_flow.md Gerenciamento de dependências (Poetry + pip)
documentation_flow.md Padronização de documentação
refactoring_flow.md Metodologia segura para refatoração
emergency_flow.md Procedimento para hotfixes

---

11. Roadmap Futuro

11.1 Milestone Atual: MVP - Engine de Pipeline

Ordem Issue Título Prioridade
1 #10 Definir contrato de Transformer P0
2 #11 Definir contrato de Sink P0
3 #12 Implementar ContextoPipeline P0
4 #13 Implementar Executor mínimo P0
5 #14 Pipeline configurável via YAML P1
6 #15 Suporte a Iterable (streaming) P1
7 #16 Versionamento incremental P1
8 #17 Migrar 1 caso de uso real P1
9 #6 Consolidar pipeline de qualidade P1

Prazo: 30/04/2026 (8 semanas)

11.2 Próximos Milestones (Sugestão)

Milestone Foco Issues
M2 - Plugins Core Implementar plugins de fonte, processador, exportador Fontes (web, pasta, PDF, OCR) + Processadores (classificador, NER, tradutor)
M3 - Web e UX Interface web para configuração visual Dashboard, editor YAML, visualizações
M4 - Análises Avançadas Grafos, timeline, topic modeling Redes sociais, linha do tempo, LDA

---

12. Glossário

Termo Definição
CraftText Nome da plataforma (escolhido em 03/03/2026)
Pipeline Sequência configurável de steps (source → processor → exporter)
Step Unidade atômica de processamento dentro de um pipeline
Plugin Módulo extensível que implementa Source, Processor ou Exporter
Source Plugin que coleta/importa documentos
Processor Plugin que transforma/enriquece documentos
Exporter Plugin que persiste/exporta documentos
Contexto Objeto que carrega estado durante execução do pipeline
Transformer Nome antigo para Processor (substituído)
Sink Nome antigo para Exporter (substituído)
Documento Unidade básica de informação (texto + metadados)
Milestone Marco com prazo que agrupa issues estratégicas
P0/P1/P2 Prioridades (P0: essencial, P1: importante, P2: futuro)
Strategic Label para issues que fazem parte da milestone ativa
Frozen Label para features congeladas durante milestone
FASE Documento que registra uma fase concluída do projeto
Flow Documento que define um processo (Git, Quality, etc.)
Telemetria Sistema de instrumentação para monitoramento
Lazy Loading Carregamento sob demanda (Plugin Manager)
Clean Architecture Arquitetura em camadas com domínio puro

---

📌 Histórico de Revisões

Versão Data Autor Alterações
1.0 04/03/2026 Thiago Ribeiro Versão inicial do documento de contexto

---

<div align="center">
  <sub>CraftText - Plataforma de Pipeline Configurável</sub>
  <br>
  <sub>Documento mantido como código</sub>
  <br>
  <sub>© 2026 Thiago Ribeiro</sub>
</div>
```
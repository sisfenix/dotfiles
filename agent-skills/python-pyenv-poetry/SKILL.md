---
name: python-pyenv-poetry
description: Diretrizes para gerenciar ambientes Python usando pyenv e poetry para manter o Python core limpo ao criar ou executar scripts Python e gerenciar pacotes.
---

# Gerenciamento de Ambiente Python com Pyenv e Poetry

Este skill orienta sobre como criar, gerenciar e executar scripts Python mantendo o ambiente do Python global (core) limpo e isolado. Ele utiliza o `pyenv` para gerenciar as versões do interpretador Python e o `poetry` para o gerenciamento de pacotes e ambientes virtuais.

## Diretrizes Gerais

> [!IMPORTANT]
> **Nunca** instale pacotes diretamente no Python global/sistema (e.g., com `pip install <pacote>` sem um ambiente ativo). Sempre utilize o Poetry para gerenciar as dependências do seu projeto dentro de um ambiente virtual isolado.

> [!TIP]
> Configure o Poetry para criar o ambiente virtual (`.venv`) na raiz do próprio projeto. Isso facilita a identificação do ambiente pela IDE e simplifica a limpeza.

---

## Fluxo de Trabalho Passo a Passo

### 1. Definição da Versão do Python com Pyenv

Antes de inicializar o projeto, defina a versão do Python que será utilizada.

1. **Listar versões instaladas do Python**:
   ```bash
   pyenv versions
   ```
2. **Instalar uma versão recente (se necessário)**:
   Escolha uma versão estável recente (e.g., `3.11.x` ou `3.12.x`):
   ```bash
   pyenv install 3.12.3
   ```
3. **Definir a versão local do projeto**:
   No diretório raiz do projeto, configure a versão desejada. Isso criará um arquivo `.python-version`:
   ```bash
   pyenv local 3.12.3
   ```

### 2. Inicialização do Projeto com Poetry

Com a versão do Python definida pelo `pyenv`, inicialize o gerenciamento de pacotes.

1. **Inicializar o Poetry**:
   Se o projeto já existe ou está sendo iniciado:
   ```bash
   poetry init --no-interaction
   ```
   *Nota: Isso criará o arquivo `pyproject.toml`.*

2. **Forçar ambiente virtual no diretório do projeto**:
   Execute esta configuração local para garantir que o diretório `.venv` seja criado na raiz do seu projeto:
   ```bash
   poetry config virtualenvs.in-project true --local
   ```

3. **Vincular o Poetry à versão correta do Python**:
   Instrua o Poetry a usar a versão do Python configurada pelo `pyenv`:
   No Windows (PowerShell):
   ```powershell
   poetry env use ((pyenv which python).Trim())
   # Ou aponte para a versão específica instalada pelo pyenv se o comando acima falhar
   poetry env use python
   ```
   No Linux/macOS (bash/zsh):
   ```bash
   poetry env use $(pyenv which python)
   ```

### 3. Gerenciamento de Dependências

Toda e qualquer dependência necessária para rodar seus scripts deve ser adicionada pelo Poetry.

- **Adicionar pacotes de produção**:
  ```bash
  poetry add nome-do-pacote
  ```
- **Adicionar pacotes de desenvolvimento** (linters, formatadores, testes):
  ```bash
  poetry add --group dev black flake8 pytest
  ```
- **Instalar dependências existentes**:
  Se o projeto já possui um `pyproject.toml` or `poetry.lock`:
  ```bash
  poetry install
  ```

### 4. Execução de Scripts Python

Para executar qualquer script Python, certifique-se de que ele roda dentro do contexto do ambiente virtual criado.

- **Executar um script diretamente**:
  ```bash
  poetry run python caminho/para/script.py
  ```
- **Executar comandos de ferramentas instaladas**:
  ```bash
  poetry run pytest
  ```
- **Ativar o shell do ambiente virtual** (se necessário realizar múltiplas interações):
  ```bash
  poetry shell
  ```

---

## Verificação e Resolução de Problemas

### Como verificar se o ambiente está limpo e correto?

- **Verificar o Python ativo**:
  ```bash
  poetry run python -c "import sys; print(sys.executable)"
  ```
  O caminho retornado deve apontar para o diretório `.venv` do projeto, e não para o diretório do pyenv global ou do sistema.

- **Verificar pacotes instalados**:
  ```bash
  poetry show
  ```
  Isso listará apenas os pacotes declarados no `pyproject.toml` e suas dependências.

### O que adicionar ao `.gitignore`?
Sempre garanta que os seguintes itens estão no `.gitignore` para evitar incluir arquivos desnecessários no controle de versão:
```text
.venv/
.poetry/
__pycache__/
*.pyc
.python-version
```

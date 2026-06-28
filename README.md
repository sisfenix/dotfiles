# 🛠️ Alan's Dotfiles

Repositório centralizado de configurações personalizadas (*dotfiles*) para otimizar e padronizar ambientes de desenvolvimento e análise. Este repositório contém configurações ajustadas para produtividade, depuração de baixo nível, análise de rede, modelagem 3D e desenvolvimento geral.

---

## 📁 Estrutura do Repositório

Aqui está uma visão geral dos programas configurados e seus respectivos diretórios:

| Programa | Diretório | Arquivos Principais | Descrição |
| :--- | :--- | :--- | :--- |
| **Zsh** | [`zsh/`](./zsh) | `zshrc` | Configuração de shell com Oh My Zsh, plugins e aliases de segurança. |
| **Git** | [`git/`](./git) | `gitconfig` | Identidade do desenvolvedor, cores personalizadas e aliases de produtividade. |
| **Vim** | [`vim/`](./vim) | `vimrc` | Editor leve com tabulação consistente, busca inteligente e tema para terminais. |
| **GDB** | [`gdb/`](./gdb) | `gdbinit` | Depurador otimizado para engenharia reversa com a sintaxe Intel e PEDA. |
| **Wireshark** | [`wireshark/`](./wireshark) | `profiles/` | Perfis específicos de análise de tráfego de rede (WLAN, DHCP, DNS, etc). |
| **FreeCAD** | [`freecad/`](./freecad) | `system.cfg`, `user.cfg` | Preferências de interface e bancadas de trabalho (Workbenches). |
| **Agent Skills** | [`agent-skills/`](./agent-skills) | `python-pyenv-poetry/` | Diretrizes e instruções personalizadas para assistentes de IA (e.g., Pyenv + Poetry). |

---

## ⚙️ Detalhes das Configurações

### 🐚 Zsh (`zsh/`)
Configuração focada em produtividade no terminal utilizando o **Oh My Zsh**.
*   **Tema:** `xiong-chiamiov-plus`
*   **Plugins Ativos:**
    *   `git`: Atalhos integrados para Git.
    *   `aws`: Autocompletar e utilitários para AWS CLI.
    *   `zsh-autosuggestions`: Sugestões inteligentes baseadas no histórico.
*   **Melhorias de Usabilidade:**
    *   Mapeamento completo do teclado numérico (*keypad*) e das teclas `Home`/`End`.
    *   *Aliases* de segurança ativos por padrão: `rm`, `mv` e `cp` pedem confirmação (`-i`) para evitar perda acidental de dados.

### 🐙 Git (`git/`)
Configuração global do Git adaptada para o fluxo de trabalho de Alan Lopes.
*   **Identidade:** Alan Lopes (`desenv.alanlopes@gmail.com`)
*   **Branches:** Rastreamento padrão para `upstream` no push; branch padrão definido como `master`.
*   **Aparência:** Cores customizadas no terminal para diferenciar branches locais (amarelo), remotos (verde) e destaques de diff.
*   **Ferramenta de Merge:** Integrado com `vimdiff`.
*   **Aliases Úteis:**
    *   `git logs`: Log formatado e colorido com hash abreviado e autor.
    *   `git glogs`: Visualização do histórico em grafo estruturado.
    *   `git changes`: Lista compacta dos arquivos modificados por commit.
    *   `git s`: Atalho rápido para `status`.
    *   `git b`: Exibição detalhada de ramificações.

### 📝 Vim (`vim/`)
Uma configuração limpa e eficiente para edição rápida diretamente pelo terminal.
*   **Indentação:** Configurado com 2 espaços de espaçamento (sem tabs reais) para máxima compatibilidade.
*   **Navegação:** Exibição combinada de `number` (número absoluto da linha atual) e `relativenumber` (distâncias relativas para facilitar saltos com comandos Vim).
*   **Busca Avançada:** Busca incremental (`incsearch`), destaque de resultados (`hlsearch`) e sensibilidade inteligente a maiúsculas/minúsculas (`smartcase`).
*   **Compatibilidade de Cores:** Esquema de cores `darkblue` ativado para garantir boa legibilidade mesmo em conexões SSH via PuTTY.

### 🐞 GDB (`gdb/`)
Otimizado para análise de binários e engenharia reversa.
*   **Sintaxe de Disassembly:** Define a exibição padrão de instruções em assembly usando a sintaxe **Intel** (mais legível que a sintaxe AT&T).
*   **Integração:** Carrega automaticamente o **PEDA** (Python Exploit Development Assistance), enriquecendo o GDB com visualização em tempo real de registradores, pilha e código.

### 🌐 Wireshark (`wireshark/`)
Perfis personalizados para agilizar a filtragem e análise de protocolos em pacotes capturados. Contém layouts e filtros prontos para:
*   Análise de redes sem fio: `WLAN Detail Security`, `WLAN Timing`, `WLAN-detail` e `Wireless-N`.
*   Redes cabeadas e roteamento: `BGP Default`, `DHCPv4` e `DNS`.
*   Armazenamento e fluxos de mídia: `ISCSI` e `Video`.

### 📐 FreeCAD (`freecad/`)
Parâmetros de ambiente pré-definidos para agilizar a modelagem 3D.
*   Armazena configurações das bancadas de trabalho padrão como **Assembly**, **Spreadsheet**, **CAM (Path)** e a tela inicial (**Start**).

### 🤖 Agent Skills (`agent-skills/`)
Instruções e diretrizes de desenvolvimento otimizadas para agentes e assistentes de IA que operam neste repositório.
*   **Python Pyenv Poetry (`python-pyenv-poetry/`):** Diretrizes estruturadas para o gerenciamento correto de ambientes virtuais Python de forma isolada, forçando o uso de `pyenv` para controle de versão do interpretador e `poetry` para dependências (evitando poluição do Python global/sistema).

---

## 🚀 Como Aplicar as Configurações

Para aplicar estas configurações na sua máquina local, você pode criar links simbólicos (recomendado) ou copiar os arquivos para os respectivos locais em sua máquina.

### Linux / macOS

```bash
# Clone o repositório
git clone https://github.com/alanlopes/dotfiles.git ~/dotfiles
cd ~/dotfiles

# Zsh
ln -sf ~/dotfiles/zsh/zshrc ~/.zshrc

# Git
ln -sf ~/dotfiles/git/gitconfig ~/.gitconfig

# Vim
ln -sf ~/dotfiles/vim/vimrc ~/.vimrc

# GDB
ln -sf ~/dotfiles/gdb/gdbinit ~/.gdbinit

# Wireshark (copiar perfis para a pasta de configuração local)
mkdir -p ~/.config/wireshark/profiles
cp -r ~/dotfiles/wireshark/profiles/* ~/.config/wireshark/profiles/

# Agent Skills (configura o skill de IA no diretório global do Gemini)
mkdir -p ~/.gemini/config/skills
ln -sf ~/dotfiles/agent-skills/python-pyenv-poetry ~/.gemini/config/skills/python-pyenv-poetry
```

### Windows (PowerShell - Administrador)

```powershell
# Acesse o diretório do repositório clonado antes de rodar os comandos
# cd caminho\para\dotfiles

# Git (cria link simbólico no diretório home do usuário)
New-Item -ItemType SymbolicLink -Path "$HOME\.gitconfig" -Value "$PWD\git\gitconfig" -Force

# Vim
New-Item -ItemType SymbolicLink -Path "$HOME\.vimrc" -Value "$PWD\vim\vimrc" -Force

# FreeCAD (configurações do usuário no AppData)
Copy-Item -Path "$PWD\freecad\*" -Destination "$env:APPDATA\FreeCAD\" -Recurse -Force

# Agent Skills (configura o skill de IA no diretório global do Gemini)
if (!(Test-Path "$HOME\.gemini\config\skills")) { New-Item -ItemType Directory -Path "$HOME\.gemini\config\skills" -Force }
New-Item -ItemType SymbolicLink -Path "$HOME\.gemini\config\skills\python-pyenv-poetry" -Value "$PWD\agent-skills\python-pyenv-poetry" -Force
```

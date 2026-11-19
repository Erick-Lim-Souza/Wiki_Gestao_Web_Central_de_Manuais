# Wiki Gestão Web – Central de Manuais B.I.

Portal web responsivo para consulta, treinamento e download em PDF dos **8 manuais passo a passo das telas de B.I. (Business Intelligence)** do Gestão Web. Desenvolvido em arquivo único (`index.html`), sem necessidade de banco de dados ou backend.

---

## Principais Funcionalidades

- **Catálogo por Módulos:** Organização dos 8 manuais em 3 categorias — *Comercial & Vendas*, *Financeiro* e *Produção*.
- **Busca Global Inteligente:** Pesquisa simultânea em títulos, filtros, cards, gráficos, regras de negócio e dúvidas de clientes. Quando há correspondência no FAQ, o card exibe um atalho direto para a aba de dúvidas já filtrada.
- **Leitura Completa em 4 Abas:**
  1. **Passo a Passo Completo:** Sumário lateral fixo, caminho de acesso (`OUT11`), visão geral, tabela de filtros, regras de dados, fórmulas dos cards, explicação dos gráficos, filtro cruzado e roteiros de uso no dia a dia.
  2. **Dúvidas Comuns (Suporte):** FAQ pesquisável em formato de acordeão com respostas padronizadas para a equipe de suporte.
  3. **Roteiro Prático Interativo:** Checklist passo a passo para treinamento em base de teste, com progresso salvo automaticamente no navegador (`localStorage`).
  4. **Visualizar PDF:** Leitor embutido (`iframe`) que carrega o PDF oficial anexado localmente ou hospedado na pasta `pdfs/`.
- **Gerenciador / Upload de PDFs Locais:** Permite arrastar e soltar os arquivos `.pdf` do computador para teste imediato, com identificação automática pelo número (`01` a `08`) ou nome do arquivo.
- **Download Inteligente com Fallback (`jsPDF`):**
  1. Se o PDF oficial foi anexado no gerenciador, baixa o arquivo anexado.
  2. Se o site estiver hospedado e o arquivo existir na pasta `./pdfs/`, baixa o PDF oficial do servidor.
  3. Caso o arquivo ainda não esteja disponível, gera e baixa automaticamente um PDF formatado com todo o conteúdo do manual via `jsPDF` (sem erro 404).
- **Tema Escuro & Claro:** Padrão em Dark Mode (grafite `#0B0F14` com destaque verde `#00E676`) e alternância para Light Mode salva no navegador.

---

## Manuais Incluídos (Permissão `OUT11`)

| Nº | Manual | Módulo | Arquivo PDF Esperado |
| :--- | :--- | :--- | :--- |
| **01** | B.I – Análise de Vendas | Comercial & Vendas | `01 - BI Analise de Vendas - Passo a passo.pdf` |
| **02** | B.I – Geolocalização | Comercial & Vendas | `02 - BI Geolocalizacao - Passo a passo.pdf` |
| **03** | B.I – Análise Clientes e Vendedores | Comercial & Vendas | `03 - BI Clientes e Vendedores - Passo a passo.pdf` |
| **04** | B.I – Análise de Produtos | Comercial & Vendas | `04 - BI Produtos - Passo a passo.pdf` |
| **05** | B.I – Fluxo de Caixa - Anual | Financeiro | `05 - BI Fluxo de Caixa Anual - Passo a passo.pdf` |
| **06** | B.I – Análise de DRE | Financeiro | `06 - BI Analise de DRE - Passo a passo.pdf` |
| **07** | B.I – Posição da Produção | Produção | `07 - BI Posicao da Producao - Passo a passo.pdf` |
| **08** | B.I – Ordem de Produção | Produção | `08 - BI Ordem de Producao - Passo a passo.pdf` |

---

## Estrutura de Pastas para Hospedagem

Após converter seus arquivos `.docx` para `.pdf`, coloque-os dentro de uma pasta chamada `pdfs/` no mesmo diretório do `index.html`:

```text
wiki-bi-gestao-web/
├── index.html
├── README.md
└── pdfs/
    ├── 01 - BI Analise de Vendas - Passo a passo.pdf
    ├── 02 - BI Geolocalizacao - Passo a passo.pdf
    ├── 03 - BI Clientes e Vendedores - Passo a passo.pdf
    ├── 04 - BI Produtos - Passo a passo.pdf
    ├── 05 - BI Fluxo de Caixa Anual - Passo a passo.pdf
    ├── 06 - BI Analise de DRE - Passo a passo.pdf
    ├── 07 - BI Posicao da Producao - Passo a passo.pdf
    └── 08 - BI Ordem de Producao - Passo a passo.pdf
```

> **Importante:** Mantenha os nomes dos arquivos exatamente como listados acima para que o portal detecte e exiba os PDFs oficiais automaticamente.

---

## Como Usar

### 1. Testar Localmente (sem servidor)
1. Abra o arquivo `index.html` diretamente no navegador (Chrome, Edge ou Firefox).
2. Clique no botão **Gerenciar / Subir PDFs** no canto superior direito.
3. Arraste seus arquivos `.pdf` para a área de upload para testar a visualização embutida e o download dos originais.

> *Observação:* Por política de segurança dos navegadores (`CORS`), a detecção automática da pasta `./pdfs/` funciona apenas via protocolo `http://` ou `https://` (servidor local ou hospedagem). Abrindo via `file://`, utilize o botão **Gerenciar / Subir PDFs** ou o gerador automático embutido.

### 2. Rodar com Servidor Local (opcional)
Se quiser testar com a pasta `./pdfs/` carregando automaticamente na sua máquina:

```bash
# Usando Python 3
python -m http.server 8080

# Ou usando Node.js (npx)
npx serve .
```
Depois, acesse `http://localhost:8080` no navegador.

### 3. Publicar na Web ou Intranet
Como o projeto é 100% estático, basta subir a pasta com o `index.html` e a subpasta `pdfs/` para qualquer servidor web:
- **Hospedagem gratuita:** Netlify, Vercel, GitHub Pages ou Cloudflare Pages.
- **Servidor interno / Intranet:** IIS (Windows Server), Nginx ou Apache.

---

## Como Atualizar ou Adicionar Manuais

Todo o conteúdo estruturado fica concentrado na constante `MANUALS` dentro da tag `<script>` no arquivo `index.html`. Para editar um texto, incluir uma nova dúvida frequente no FAQ ou adicionar o manual `09`, basta editar ou duplicar um objeto dentro de `MANUALS` seguindo a mesma estrutura de campos (`num`, `id`, `title`, `module`, `pdfPath`, `pdfName`, `filters`, `cards`, `charts`, `faq`, `practice`).

---

## Tecnologias Utilizadas

- **HTML5 & JavaScript (Vanilla ES6+)** — Arquitetura leve em arquivo único, sem dependências de build.
- **Tailwind CSS (via CDN)** — Estilização responsiva e suporte nativo a Dark/Light Mode.
- **jsPDF (via CDN)** — Geração dinâmica de PDFs no navegador como fallback inteligente.
- **Google Fonts** — Tipografia *Inter* (leitura) e *JetBrains Mono* (códigos e permissões).
- **Web Storage API (`localStorage`)** — Persistência local do tema escolhido e do progresso nos roteiros práticos.

---

**Versão da Documentação:** 1.0 — Novembro de 2026
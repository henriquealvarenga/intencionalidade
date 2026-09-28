# Intencionalidade, Vontade, Impulsividade e Livre Arbítrio

Material educacional em neuropsiquiatria que explora intencionalidade, impulsividade, vontade, tomada de decisão e a questão do livre arbítrio. Direcionado a estudantes de medicina e psiquiatria, integra questões filosóficas, neurobiológicas e clínicas.

Livro (Quarto Book, HTML) publicado em: <https://henriquealvarenga.com/intencionalidade>

As atividades interativas e as apresentações ficam em outro repositório: [`intencionalidade-atividades`](https://github.com/henriquealvarenga/intencionalidade-atividades).

## Estrutura do projeto

```
Intencionalidade_Project/
├── _quarto.yml                  # Configuração do livro (book: capa, capítulos, apêndices, rodapé)
├── _metadata.yml                # Opções de citação
├── theme-editorial.scss         # Tema editorial (Sass) — paper, Playfair, brand laranja
├── styles.css                   # CSS pós-processamento + @font-face das fontes self-hosted
│
├── index.qmd                    # Capa + Prefácio
├── about.qmd                    # Créditos: autor, metodologia, licença, citação sugerida
├── referencias.qmd              # Referências bibliográficas
│
├── capitulos/                   # Parte I — Fundamentos (capítulos 1–10: 1.0 a 1.9)
├── casos/                       # Parte II — Casos Clínicos (5.0 abre a parte; capítulos 11–23)
├── apendices/                   # Apêndices A–D (10.1 a 10.4)
│
├── images/                      # Capa: cover.jpg (web) e cover.png (original em alta)
├── fonts/                       # Fontes self-hosted (WOFF2): Playfair, Inter, JetBrains Mono
├── _includes/                   # Trechos injetados no <head> (JSON-LD do autor, ajuste do rodapé)
├── PDF_version/                 # Versão PDF antiga do conteúdo
├── references/                  # Bibliografia (references.bib) e estilos de citação (ABNT, Vancouver)
│
├── .github/workflows/publish.yml  # Publicação automática (GitHub Actions)
├── AGENTS.md                    # Notas para agentes (CLAUDE.md aponta para ele)
└── README.md
```

## Publicação — GitHub Actions (modo moderno)

A publicação é feita automaticamente pelo workflow em `.github/workflows/publish.yml`. A cada push para `main` o GitHub Actions roda `quarto render` e faz deploy direto no GitHub Pages (modo "GitHub Actions", sem branch `gh-pages`).

Sequência de publicação:

```bash
quarto render        # opcional, só pra checar local antes do push
git add -A
git commit -m "mensagem"
git push origin main
```

Pré-requisitos no GitHub (uma vez só):

- Em **Settings → Pages** do repositório, definir **Source: GitHub Actions**.

## Estratégia escolhida

Este projeto **não tem código executável** (nenhum chunk `{r}` ou `{python}` nos `.qmd`), só Markdown. Por isso o CI é simples: instala o Quarto, roda `quarto render`, empacota o output como Pages artifact e faz deploy. **Não há `_freeze/` pra versionar** e o CI não precisa de R nem Python.

A pasta `docs/` deixou de ser versionada (entrou no `.gitignore`). É um diretório de output regenerável — quem publica é o Actions.

## Autor

Henrique Alvarenga

## Licença

Creative Commons Atribuição-NãoComercial-CompartilhaIgual 4.0 Internacional (CC BY-NC-SA 4.0).

Detalhes completos em [`about.qmd`](about.qmd) (página *Créditos* do site).

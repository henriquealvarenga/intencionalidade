# Intencionalidade, Vontade, Impulsividade e Livre Arbítrio

Material educacional em neuropsiquiatria que explora intencionalidade, impulsividade, vontade, tomada de decisão e a questão do livre arbítrio. Direcionado a estudantes de medicina e psiquiatria, integra questões filosóficas, neurobiológicas e clínicas.

Site publicado em: <https://henriquealvarenga.com/intencionalidade>

## Estrutura do projeto

```
Intencionalidade_Project/
├── _quarto.yml                          # Configuração principal do Quarto (website)
├── _metadata.yml                        # Metadados e bibliografia
├── theme-editorial.scss                 # Tema editorial (Sass) — paper, Playfair, brand laranja
├── styles.css                           # CSS pós-processamento + @font-face das fontes self-hosted
│
├── index.qmd                            # Landing page (hero + Prefácio + CTA para Introdução)
├── about.qmd                            # Créditos: autor, metodologia, licença, citação sugerida
│
├── 1.0-introducao.qmd                   # Introdução
├── 1.1-liberdade-coordenação.qmd        # Da liberdade à coordenação
├── 1.2-vontade.qmd                      # Vontade
├── 1.3-davidson.qmd                     # De Tomás de Aquino a Davidson
├── 1.4-intencionalidade-pratica.qmd     # Intencionalidade
├── 1.5-impulsividade.qmd                # Impulsividade
├── 1.6-graus-de-liberdade.qmd           # Graus de liberdade
├── 1.7-neuroquimica.qmd                 # Neuroquímica
├── 1.8-conclusao.qmd                    # Conclusão
│
├── 5.0-casos_clinicos.qmd               # Casos clínicos (índice)
├── 5.1-lobotomia.qmd                    # Lobotomia
├── 5.2-agressividade.qmd                # Agressividade
├── 5.3-pedofilia.qmd                    # Pedofilia
├── 5.4-hipersexualidade.qmd             # Hipersexualidade
├── 5.5-cleptomania.qmd                  # Cleptomania
├── 5.6-toc.qmd                          # TOC
├── 5.7-tricotilomania.qmd               # Tricotilomania
│
├── 10.0-apendices.qmd                   # Apêndices (índice)
├── 10.1-sistemas-dinamicos.qmd          # Sistemas dinâmicos
├── 10.2-apendice-vontade-religioes.qmd  # Vontade nas tradições religiosas
├── 10.3-glossario.qmd                   # Glossário
├── referencias.qmd                      # Referências
│
├── fonts/                               # Fontes self-hosted (WOFF2): Playfair, Inter, JetBrains Mono
├── images/                              # Imagens usadas no site
├── PDF_version/                         # Versão PDF do conteúdo
├── old files/                           # Arquivos antigos / backup
├── references/                          # Bibliografia e estilos de citação
│   ├── referencias.bib                  # BibTeX
│   └── csl_styles/                      # ABNT, Vancouver
│
├── .github/workflows/publish.yml        # Publicação automática (GitHub Actions)
├── .gitignore
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

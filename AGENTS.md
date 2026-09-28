# Notas para o agente Claude

Este arquivo é lido automaticamente por agentes Claude que trabalham nesse repositório (via Claude Code, Cowork ou similares). Contém preferências do autor e contexto do projeto que devem orientar qualquer modificação futura.

## Princípios do autor (não negociáveis)

1. **Best practices acima de soluções rápidas.** Antes de propor um fix, perguntar: "isso é a solução certa ou é uma gambiarra que vou acumular?" Se for gambiarra, oferecer a alternativa limpa.

2. **Navalha de Ockham.** A solução mais simples que resolve o problema é a melhor. Não empilhar seletores defensivos, não criar abstrações antecipadamente, não codar pra "talvez precise".

3. **Tratar causa-raiz, não sintomas.** Se um bug força um patch local, parar e perguntar: existe uma causa estrutural? Vale corrigir a estrutura, não o sintoma.

4. **Evitar `!important`, `!force`, override pesado.** Resolver via especificidade CSS e ordem de cascade. `!important` só quando não há outro caminho — e nesse caso, documentar com comentário explicando *por quê*.

5. **Inspecionar antes de escrever.** Em CSS especialmente: olhar o HTML real renderizado antes de criar seletores. Seis seletores empilhados "por garantia" é sinal de que faltou inspecionar.

6. **Documentar hacks com comentário no código.** Se uma gambiarra for inevitável (por exemplo, contornar bug conhecido de uma lib), explicar no comentário: *por quê* está aqui, *quando* pode sair, qual a causa raiz.

7. **Pensar no futuro.** Antes de aceitar uma estrutura, perguntar: "como isso envelhece em 6 meses? Em 2 anos? Alguém entrando no projeto vai entender por quê está assim?"

## Contexto técnico do projeto

- **Tipo:** Quarto Book, só HTML (`type: book`, `output-dir: docs`). Publicado em <https://henriquealvarenga.com/intencionalidade/>. Sem ISBN por enquanto (previsto para depois da revisão).
- **Só renderiza o que está no `_quarto.yml`:** `book.chapters` / `book.appendices` (mais os links em lista do `page-footer`, como `about.qmd`). Página nova = entrada nova lá, senão ela não é gerada.
- **Tema:** editorial puro (`theme-editorial.scss`), sem Bootswatch (cosmo). Paleta paper off-white com acento laranja queimado (`#b45309`), tipografia Playfair Display serif + Inter sans + JetBrains Mono.
- **Fontes:** self-hosted em `fonts/` (WOFF2). Não usar CDN do Google Fonts.
- **Publicação:** GitHub Actions (`.github/workflows/publish.yml`), Pages nativo. `docs/` não é versionado (gerado no CI).
- **Sem código executável.** Markdown puro nos `.qmd`. Não há chunks `{r}` ou `{python}`. Estratégia de CI simples — sem `_freeze/`.
- **Capa (index):** título, subtítulo, autor, data, descrição e imagem (`images/cover.jpg`) vêm de `book:` no `_quarto.yml` e só aparecem no `index.qmd`, que contém o Prefácio (`# Prefácio {.unnumbered}`). `images/cover.png` é o original em alta, versionado e não publicado.
- **Data do livro (`book.date`):** data da última edição do **texto** (hoje 19/06/2026), não do deploy. Mudou conteúdo → atualizar `book.date` e a linha "Última atualização" de `about.qmd`. Ajustes de layout, infra, estrutura ou de referências/navegação (ex.: números de capítulo desatualizados) não mudam a data — decisão do autor em 28/09/2026.
- **Créditos:** `about.qmd`, linkado no footer (texto "Créditos").

## Convenções do projeto

- **Autoria:** `book.author` no `_quarto.yml` (aparece só na capa) + detalhes em `about.qmd`. Não declarar `author:` no `_metadata.yml` nem no topo do `_quarto.yml` — iria para o título de todas as páginas.
- **Stubs / capítulos não escritos:** título real + uma linha `*Em construção.*` (ex.: `# Impulsividade`). O título é obrigatório: no livro ele vira o nome do capítulo na barra lateral e na numeração.
- **Numeração:** automática (Capítulo 1–23, Apêndice A–D), só no nível de capítulo (`number-depth: 1`). Não escrever números de capítulo no texto — para citar outro capítulo/caso, use link Markdown para o `.qmd` (ex.: `[caso EVR](5.13-evr-marcador-somatico.qmd)`).
- **Um título de capítulo por arquivo:** se o título vem do YAML (`title:`), as seções internas começam em `##`. Um `#` no corpo vira outro capítulo.
- **Âncoras `sec-`:** IDs com prefixo `sec-` (ex.: `{#sec-vontade-religiao}`). As âncoras `#sec-parks`, `#sec-whitman`, `#sec-evr` e `#sec-nomes-do-fenomeno` são usadas pelas atividades (outro repositório) — não renomear sem atualizar lá.
- **`code-tools` desativado.** Site é livro, não documento técnico.
- **`bread-crumbs` desativado.** Sidebar já indica posição na hierarquia.
- **Licença:** CC BY-NC-SA 4.0.

## Estrutura de arquivos relevante

- `_quarto.yml` — config principal (`book:` com capa, capítulos, apêndices, navbar, rodapé; theme, format, lang, bibliografia)
- `_metadata.yml` — metadados globais (opções de citação)
- `theme-editorial.scss` — tema (defaults + rules)
- `styles.css` — overrides pós-Quarto + `@font-face` self-hosted + variáveis CSS expostas
- `index.qmd` — capa + Prefácio
- `images/` — capa do livro (`cover.jpg` web, `cover.png` original) e `favicon.png` (recorte da capa)
- `about.qmd` — créditos
- `capitulos/1.*.qmd` — Parte I, Fundamentos (capítulos 1–10)
- `casos/5.*.qmd` — Parte II, Casos Clínicos (5.0 abre a parte; capítulos 11–23)
- `apendices/10.*.qmd` — apêndices A–D
- `referencias.qmd` — referências (não numerado)
- `references/references.bib` — bibliografia BibTeX
- `references/csl_styles/` — estilos de citação (ABNT, Vancouver)

## Fluxo de publicação

```bash
quarto render          # opcional, conferir antes do push
git add -A
git commit -m "..."
git push origin main   # GitHub Actions cuida do resto
```

## Atividades e apresentações

As atividades interativas, o painel do professor (Supabase) e as apresentações (revealjs)
foram para o repositório `intencionalidade-atividades` em setembro de 2026
(<https://henriquealvarenga.com/intencionalidade-atividades/>), com histórico preservado.
As lições de engenharia de áudio, painel, Supabase e deploy moram no `CLAUDE.md` e em
`atividades/_specs/ENGENHARIA-modos-campeonato.md` de lá. As que valem aqui também:

- **Cache de deploy:** no Safari o hard refresh é `Cmd+Option+R` (`Cmd+Shift+R` é Modo
  Leitura!). Valide deploy com cache-bust (`?cb=`) e conferindo o `headSha` do run.
- **Renomear arquivo:** `git mv` + `grep -rn`; atualize referência viva (`chapters:`, `href`).
  Os endereços dos capítulos são públicos (e usados pelas atividades) — evite renomear.

---

*Última atualização: setembro de 2026.*

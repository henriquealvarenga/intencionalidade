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

- **Tipo:** Quarto website (`type: website`, `output-dir: docs`)
- **Tema:** editorial puro (`theme-editorial.scss`), sem Bootswatch (cosmo). Paleta paper off-white com acento laranja queimado (`#b45309`), tipografia Playfair Display serif + Inter sans + JetBrains Mono.
- **Fontes:** self-hosted em `fonts/` (WOFF2). Não usar CDN do Google Fonts.
- **Publicação:** GitHub Actions (`.github/workflows/publish.yml`), Pages nativo. `docs/` não é versionado (gerado no CI).
- **Sem código executável.** Markdown puro nos `.qmd`. Não há chunks `{r}` ou `{python}`. Estratégia de CI simples — sem `_freeze/`.
- **Landing page:** `index.qmd` é a página de entrada (hero + Prefácio + CTA "Começar a leitura"). Usa `pagetitle:` em vez de `title:` no YAML pra suprimir o título block do Quarto.
- **Créditos:** `about.qmd`, linkado no footer (texto "Créditos").

## Convenções do projeto

- **Autoria:** centralizada em `about.qmd`. Não declarar `author:` no `_metadata.yml` global — polui o título block de todas as páginas. Se for necessário em uma página específica, declarar no YAML daquela página.
- **Stubs / capítulos não escritos:** arquivo contém uma única linha `# Em construção`, sem YAML title. Visual obviamente incompleto, evita esquecer de voltar.
- **Cross-references entre seções:** usar IDs com prefixo `sec-` (ex.: `::: {#sec-vontade-religiao}`). Referenciar com `@sec-...`.
- **`code-tools` desativado.** Site é livro, não documento técnico.
- **`bread-crumbs` desativado.** Sidebar já indica posição na hierarquia.
- **Licença:** CC BY-NC-SA 4.0.

## Estrutura de arquivos relevante

- `_quarto.yml` — config principal (navbar, sidebar, theme, format)
- `_metadata.yml` — metadados globais (bibliografia, CSL, lang)
- `theme-editorial.scss` — tema (defaults + rules)
- `styles.css` — overrides pós-Quarto + `@font-face` self-hosted + variáveis CSS expostas
- `index.qmd` — landing
- `about.qmd` — créditos
- `1.*.qmd` — capítulos principais
- `5.*.qmd` — casos clínicos
- `10.*.qmd` — apêndices
- `references/references.bib` — bibliografia BibTeX
- `references/csl_styles/` — estilos de citação (ABNT, Vancouver)

## Fluxo de publicação

```bash
quarto render          # opcional, conferir antes do push
git add -A
git commit -m "..."
git push origin main   # GitHub Actions cuida do resto
```

## Lições de engenharia (reutilizáveis — valem para os outros sites do autor)

Diário detalhado em `atividades/_specs/ENGENHARIA-modos-campeonato.md`. Antes de mexer
em áudio, painel ou deploy, leia o checklist (§11) de lá. Armadilhas que já custaram tempo:

- **Web Audio mudo no Safari:** nunca use `exponentialRampToValueAtTime` no ganho (o
  WebKit não aplica → som inaudível, mas o indicador de áudio da aba acende). Use
  **rampas lineares**; espere o `resume()` (assíncrono) resolver antes de agendar;
  destrave o `AudioContext` no 1º gesto. (ENGENHARIA §7)
- **Ordem das abas do painel = ordem dos `<script>`** em `painel.html` (auto-registro
  via `registrarPainel`). Reordenar UI = reordenar `<script>`, não mexer no JS. (§3)
- **Uma tela, uma responsabilidade:** não repita o mesmo dado (ex.: placar) numa tela
  de gabarito *e* numa tela de pódio dedicada. (§4)
- **Cache de deploy:** no Safari o hard refresh é `Cmd+Option+R` (`Cmd+Shift+R` é Modo
  Leitura!). Valide deploy com cache-bust (`?cb=`) e conferindo o `headSha` do run. (§8)
- **Renomear arquivo:** `git mv` + `grep -rn`; atualize referência viva (`rota:`, `href`),
  preserve registro histórico nas specs. A ordem do fluxo mora num registry, não no nome. (§2)
- **Identidade compartilhada:** uma chave única de `localStorage` + boot-guard; sem
  re-login por página. (§5)
- **Agregar escalas diferentes:** normalize /100 + **clamp**; confira `maxPontos` contra
  a constante de score real. (§6)

---

*Última atualização: junho de 2026.*

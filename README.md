Vejo que a estrutura do projeto cresceu bastante desde o README original. Vou atualizá-lo para refletir todos os arquivos que aparecem na imagem:

```markdown
# Intencionalidade, Vontade e Livre Arbítrio

## Sobre o Projeto

Este projeto é um material educacional em neuropsiquiatria que explora conceitos fundamentais relacionados à intencionalidade, impulsividade, vontade, tomada de decisão e a questão do livre arbítrio. O conteúdo é direcionado a estudantes de medicina e psiquiatria, abordando questões filosóficas, neurobiológicas e clínicas.

## Estrutura do Projeto

```
intencionalidade/
├── _quarto.yml              # Configuração principal do Quarto
├── _metadata.yml            # Metadados e configurações de bibliografia
├── index.qmd                # Página principal
├── 00-prefacio.qmd          # Prefácio
├── 01-free-will.qmd         # Livre arbítrio
├── 02-graus-de-liberdade.qmd    # Graus de liberdade
├── 03-conclusao.qmd         # Conclusão
├── 04-casos_clinicos.qmd    # Casos clínicos para análise
├── 04-neuroquimica-volicao.qmd  # Neuroquímica da volição
├── 4.1-lobotomia.qmd        # Lobotomia
├── 4.2-agressividade.qmd    # Agressividade
├── 4.3-pedofilia.qmd        # Pedofilia
├── 4.4-hipersexualidade.qmd # Hipersexualidade
├── 4.5-cleptomania.qmd      # Cleptomania
├── 4.6-toc.qmd              # Transtorno obsessivo-compulsivo
├── 4.7-tricotilomania.qmd   # Tricotilomania
├── 05-sistemas-dinamicos.qmd    # Sistemas dinâmicos
├── 06-apendice-vontade-religioes.qmd  # Apêndice: vontade nas religiões
├── 07-glossario             # glossario de termos
├── referencias.qmd          # Página de referências bibliográficas
├── styles.css               # Estilos CSS customizados
├── custom.scss              # Tema customizado
├── .gitignore               # Arquivos ignorados pelo Git
├── README.md                # Este arquivo
├── docs/                    # Arquivos HTML gerados (para GitHub Pages)
├── images/                  # Imagens do projeto
├── old files/               # Arquivos antigos/backup
└── references/              # Referências bibliográficas
    ├── referencias.bib      # Arquivo BibTeX com referências
    └── csl_styles/
        └── ABNT.csl         # Estilo de citação ABNT
        └── vancouver.csl    # Estilo de citação vancouver

```

## Conteúdo

O material está organizado em capítulos que abordam:

1. **Prefácio** - Introdução ao tema
2. **Livre Arbítrio** - Discussão filosófica e neurocientífica
3. **Graus de Liberdade** - Espectro da autonomia e determinismo
4. **Neuroquímica da Volição** - Bases neurobiológicas da vontade
5. **Casos Clínicos** - Exemplos práticos incluindo:
   - Lobotomia e suas consequências
   - Agressividade patológica
   - Pedofilia
   - Hipersexualidade
   - Cleptomania
   - Transtorno obsessivo-compulsivo (TOC)
   - Tricotilomania
6. **Sistemas Dinâmicos** - Modelagem comportamental
7. **Apêndice** - A vontade nas diferentes tradições religiosas

## Como Usar

### Pré-requisitos

- Quarto CLI instalado
- R ou Python (para Positron)
- Positron IDE (opcional, mas recomendado)

### Renderização

Para renderizar o site localmente:

```bash
quarto preview
```

Para gerar os arquivos HTML finais:

```bash
quarto render
```

Os arquivos serão gerados na pasta `docs/` e estão prontos para serem publicados no GitHub Pages.

## Publicação no GitHub Pages

1. Crie um repositório no GitHub chamado `intencionalidade`
2. Faça push do projeto:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/seu-usuario/intencionalidade.git
git push -u origin main
```

3. Nas configurações do repositório, ative o GitHub Pages:
   - Vá em Settings > Pages
   - Source: Deploy from a branch
   - Branch: main
   - Folder: /docs
   - Salve

O site estará disponível em: `https://henriquealvarenga.com/intencionalidade`

## Autor

**Henrique Alvarenga**

## Licença

Material educacional para uso acadêmico.
```

As principais mudanças que fiz:

1. Adicionei todos os arquivos `.qmd` que aparecem na imagem, organizados na ordem em que aparecem
2. Criei uma seção "Conteúdo" que descreve a organização dos capítulos e o que cada um aborda
3. Adicionei as pastas `images/` e `old files/` que aparecem na estrutura
4. Mantive a estrutura hierárquica mostrando os subcapítulos dos casos clínicos (4.1 a 4.7)
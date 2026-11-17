# Revela.com

> Seu talento merece ser visto.

Trabalho final de semestre do curso de Ciências da Computação: interface de uma plataforma esportiva feita somente com **HTML5 e CSS3**.

## 1. Sobre o projeto

O Revela.com é uma plataforma que conecta **jovens atletas** a **clubes e olheiros**. O atleta encontra peneiras (testes de seleção para categorias de base), se inscreve, acompanha as avaliações recebidas e troca mensagens com profissionais do esporte. O olheiro busca talentos, avalia atletas, cadastra peneiras e gerencia os inscritos.

### Objetivo

Reunir em um só lugar as informações que hoje ficam espalhadas entre redes sociais, grupos de mensagens e indicações pessoais, de forma que:

- o atleta saiba **quais peneiras existem perto dele** e **como está evoluindo** (Overall e Potencial);
- o olheiro encontre **atletas com o perfil que procura** e registre suas avaliações de forma organizada.

### Problema que o projeto procura resolver

Muitos jovens com potencial não são vistos por clubes porque moram longe dos grandes centros, não sabem quando acontecem as peneiras ou não têm como mostrar seu desempenho. Do outro lado, olheiros gastam tempo procurando atletas sem informações padronizadas. O Revela.com propõe um perfil esportivo com notas, atributos e histórico, além de um canal direto entre atleta, responsável e clube.

## 2. Tecnologias utilizadas

| Tecnologia | Uso no projeto |
|---|---|
| HTML5 | Estrutura e conteúdo das páginas, com elementos semânticos (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`), formulários, tabelas, `meter` para as notas e `details`/`summary` para os esportes recolhíveis da avaliação |
| CSS3 | Aparência, layout com Flexbox e Grid, variáveis CSS e responsividade com media queries |
| SVG | Imagens de exemplo (avatar e foto) |

O projeto **não usa** JavaScript, frameworks, bibliotecas externas, banco de dados nem servidor.

## 3. Estrutura de pastas

```
Revela.com/
├── index.html            ponto de entrada: abre o login automaticamente
├── css/
│   ├── base.css          variáveis, reset, tipografia e regras gerais
│   ├── componentes.css   peças reutilizáveis (botões, cards, formulários...)
│   └── telas.css         ajustes específicos de cada tela
├── html/                 as 16 páginas do sistema
├── img/
│   ├── avatar-padrao.svg     foto de perfil padrão
│   └── foto-placeholder.svg  foto de exemplo da galeria
└── README.md
```

## 4. Organização do CSS

Todas as páginas carregam os três arquivos nesta ordem: `base.css` → `componentes.css` → `telas.css`. Cada arquivo pode complementar o anterior.

- **`base.css`** — define as **variáveis** (cores, arredondamentos, sombras, espaçamentos, contorno de foco), o reset, a tipografia, os links, o estilo de foco para quem navega pelo teclado, o link "Pular para o conteúdo", a classe `.texto-leitor` (texto lido apenas por leitores de tela) e o respeito à preferência de **menos movimento** (`prefers-reduced-motion`).
- **`componentes.css`** — peças que aparecem em várias telas: cabeçalho e menu, área de conteúdo, rodapé, cards, botões (`.botao-primario` e `.botao-secundario`), campos de formulário, etiquetas, status (aprovado, em análise, não aprovado, encerrada), barras de notas, listas, tabelas com rolagem própria, fotos e o aviso das páginas de demonstração (`.aviso-demo`).
- **`telas.css`** — ajustes de cada página (login, cadastro, painéis, perfil, peneiras, mensagens, avaliação e inscritos), separados por comentários. Todo `<body>` tem a classe da sua tela (ex.: `.pagina-login`); ela só é usada no CSS quando uma regra precisa valer apenas naquela página.

O CSS estiliza apenas classes e elementos, nunca IDs. Os IDs do HTML existem só para ligar rótulos e descrições aos campos (`for`, `aria-labelledby`, `aria-describedby`) e para as âncoras internas.

### Paleta de cores

| Variável | Cor | Uso |
|---|---|---|
| `--verde` | `#1f5e3b` | cor principal, botões e destaques |
| `--verde-escuro` | `#154429` | hover dos botões |
| `--verde-claro` | `#e6efe9` | fundos de destaque |
| `--branco` | `#ffffff` | cards |
| `--fundo` | `#f4f6f5` | fundo da página |
| `--texto` | `#1d2b24` | texto principal |
| `--texto-suave` | `#5b6b62` | textos de apoio |
| `--borda` | `#d5dfd9` | bordas |

### Responsividade

O CSS é escrito primeiro para o celular (*mobile first*) e ganha colunas conforme a tela aumenta:

| Largura | O que muda |
|---|---|
| até 767px | uma coluna; menu quebra em mais de uma linha; botões dos formulários ocupam a largura |
| a partir de 768px | cabeçalho em linha, login com benefícios em três colunas e os dois formulários lado a lado, perfil com foto ao lado do nome, mensagens em duas colunas, textos das tabelas podem quebrar linha (a tabela cabe sem rolagem lateral) |
| a partir de 900px | painéis com coluna lateral (início, peneiras e talentos) e lista de conversas mais larga |

As grades de cards, filtros e galeria usam `repeat(auto-fill, minmax(...))`, então o próprio navegador decide quantas colunas cabem. No celular, as tabelas ficam dentro de uma área com rolagem horizontal própria (`.tabela-rolagem`), sem fazer a página inteira rolar para o lado. O layout foi conferido nas larguras 320, 375, 768, 1024, 1366 e 1920px.

## 5. Tipos de usuário

### Atleta (talento)

Jovem que quer ser descoberto. Vê peneiras perto de onde mora, se inscreve, acompanha seu **Overall (OVR, de 0 a 70)** e seu **Potencial (de 0 a 100)**, consulta as avaliações recebidas e conversa com olheiros. Menores de 18 anos informam um responsável, que recebe cópia das mensagens.

### Olheiro

Profissional ligado a um clube (olheiro, coordenador da base, treinador...). Busca talentos com filtros, abre o perfil dos atletas, registra avaliações, cadastra peneiras, acompanha os inscritos e envia convites.

## 6. Páginas

Todas as páginas ficam na pasta `html/`.

| Página | Usuário | Descrição |
|---|---|---|
| `login.html` | todos | Apresentação da plataforma, formulário de entrada e de criação de conta |
| `formulario.html` | atleta | Cadastro do atleta: esportes, experiência, cidade e responsável |
| `formulario-olheiro.html` | olheiro | Cadastro do olheiro: vínculo com o clube, esportes e região |
| `main.html` | atleta | Painel inicial: desempenho, peneiras abrindo em breve, aviso de mensagens, notícias e dicas |
| `peneiras.html` | atleta | Busca de peneiras, inscrições do atleta e lista de peneiras próximas |
| `peneira-detalhe.html` | atleta | Detalhes de uma peneira, organizador e inscrição |
| `mensagens.html` | atleta | Conversas com olheiros e convite para peneira |
| `perfil.html` | atleta | Perfil com notas, atributos, dados esportivos, fotos, avaliações e histórico |
| `main-olheiro.html` | olheiro | Painel inicial: números de resumo, avaliações pendentes, próximas peneiras e talentos em destaque |
| `talentos.html` | olheiro | Busca de atletas com filtros |
| `atleta.html` | olheiro | Perfil de um atleta visto pelo olheiro, com convite para peneira |
| `avaliar.html` | olheiro | Formulário de avaliação por atributos de cada esporte |
| `peneiras-olheiro.html` | olheiro | Peneiras do clube e cadastro de nova peneira |
| `inscritos.html` | olheiro | Inscritos em uma peneira, com presença, desempenho e resultado |
| `mensagens-olheiro.html` | olheiro | Conversas com atletas, com opção de anexar convite |
| `perfil-olheiro.html` | olheiro | Perfil do olheiro, atividade e últimas avaliações |

### Fluxo de navegação

```
login.html ──Entrar──────────────► main.html (atleta)
    │                                  ├─ peneiras.html ─► peneira-detalhe.html
    │                                  ├─ mensagens.html
    │                                  └─ perfil.html
    │
    └──Criar conta──► formulario.html ◄──► formulario-olheiro.html
                          │                     │
                          ▼                     ▼
                      main.html          main-olheiro.html (olheiro)
                                               ├─ talentos.html ─► atleta.html ─► avaliar.html
                                               ├─ peneiras-olheiro.html ─► inscritos.html
                                               ├─ mensagens-olheiro.html
                                               └─ perfil-olheiro.html
```

O menu de cada experiência só leva a páginas daquele tipo de usuário, e o item da seção atual fica destacado (`aria-current`).

## 7. Acessibilidade

- Todos os campos têm `<label>` associado por `for` e `id`.
- Grupos de opções usam `fieldset` e `legend`; dicas de preenchimento são ligadas aos campos com `aria-describedby`.
- Imagens têm texto alternativo (`alt`).
- Link "Pular para o conteúdo" no início de cada página e contorno de foco visível para navegação pelo teclado.
- Tabelas com cabeçalhos de coluna (`scope="col"`) e de linha (`scope="row"`).
- Cores com contraste adequado entre texto e fundo; o status nunca depende só da cor, pois sempre traz o texto ("Aprovado", "Em análise"...).

## 8. Como executar

Não é preciso instalar nada.

1. Baixe ou clone o repositório.
2. Dê dois cliques em **`index.html`**, na raiz do projeto (ou arraste o arquivo para o navegador). Ele abre a tela de login (`html/login.html`) automaticamente.
3. Navegue pelos menus. Para ver a experiência do olheiro, vá em **Criar conta** e escolha **Sou Olheiro**, ou abra diretamente `main-olheiro.html`.

Também é possível usar uma extensão de servidor local, como o Live Server do VS Code.

## 9. Limitações da versão atual

Esta versão é uma **implementação de interface**. Por isso:

- **Não há autenticação real.** O botão "Entrar" apenas leva ao painel do atleta; nenhuma senha é conferida nem guardada.
- **Não há banco de dados nem servidor.** Nomes, notas, peneiras e mensagens são dados de demonstração escritos no HTML; nada do que é digitado fica salvo.
- **Os formulários só demonstram o fluxo.** Eles validam os campos no próprio navegador (`required`, `type="email"`, `min`, `max`, `minlength`...) e depois abrem a próxima página. Como não existe servidor para receber dados, todos usam `method="get"`, que funciona tanto abrindo o arquivo direto quanto em servidores locais (um envio POST para um arquivo `.html` é recusado por esses servidores). Para que senha, e-mail, nome, data de nascimento e contatos do responsável **nunca apareçam na URL**, esses campos ficam sem o atributo `name`: o navegador valida o preenchimento, mas não envia o valor. Os demais campos têm `name`. Com um backend real, esses formulários passariam a usar `method="post"` e todos os campos receberiam `name`.
- **Sem JavaScript**, nada muda dinamicamente: o OVR da tela de avaliação não é calculado, os filtros de busca não filtram os cards, a troca de foto não mostra a nova imagem e as conversas da lista abrem sempre a mesma conversa de exemplo.
- A página de detalhes mostra uma única peneira de exemplo, o perfil de atleta visto pelo olheiro é sempre o de Lucas Andrade e a lista de inscritos é sempre a da Peneira Sub-17 de 28/11. As páginas `atleta.html`, `avaliar.html` e `inscritos.html` deixam isso claro com um aviso de demonstração (`.aviso-demo`).

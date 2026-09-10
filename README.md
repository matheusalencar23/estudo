# 📚 Estudo

Repositório pessoal de anotações de estudo, organizado como um **vault do [Obsidian](https://obsidian.md/)**. As notas combinam texto em Markdown com diagramas feitos no **[Excalidraw](https://excalidraw.com/)** (via [obsidian-excalidraw-plugin](https://github.com/zsviczian/obsidian-excalidraw-plugin)), permitindo explicar conceitos de forma visual junto com o texto.

O versionamento e backup automático do vault é feito com o plugin [obsidian-git](https://github.com/denolehov/obsidian-git).

## 🗂️ Estrutura

```
.
├── Estrutura de dados e algoritmos/   # Notas sobre ED&A
│   ├── Índice.md                      # Ponto de entrada do tópico
│   └── Stack (pilha).md
└── Excalidraw/                        # Desenhos/diagramas usados nas notas
    ├── stack_pilha.md
    ├── stack_pilha_add.md
    └── stack_pilha_remove.md
```

Cada tópico de estudo tem sua própria pasta, com um arquivo `Índice.md` funcionando como sumário e ponto de partida para navegar pelas notas daquele assunto. Os desenhos do Excalidraw ficam centralizados na pasta `Excalidraw/` e são referenciados dentro das notas por meio de embeds (`![[nome_do_desenho]]`).

### Tópicos atuais

- **Estrutura de dados e algoritmos**
  - [Stack (pilha)](<Estrutura de dados e algoritmos/Stack (pilha).md>) — conceito de LIFO, inserção e remoção de elementos, com diagramas ilustrativos.

## 🛠️ Como usar

1. Instale o [Obsidian](https://obsidian.md/).
2. Clone este repositório:
   ```bash
   git clone https://github.com/matheusalencar23/estudo.git
   ```
3. Abra a pasta clonada como um vault no Obsidian (*Open folder as vault*).
4. Os plugins necessários (`obsidian-excalidraw-plugin` e `obsidian-git`) já estão configurados em `.obsidian/community-plugins.json` — basta habilitá-los em *Settings → Community plugins*, caso não sejam ativados automaticamente.

## ✍️ Convenções

- Cada assunto novo vira uma pasta na raiz do vault, com um arquivo `Índice.md` listando as notas daquele tópico.
- Diagramas ficam na pasta `Excalidraw/` e são embutidos nas notas de texto.
- Commits são feitos automaticamente pelo plugin `obsidian-git` como backups periódicos do vault.

## 🎯 Objetivo

Manter um registro pessoal de estudos, priorizando compreensão visual dos conceitos através de diagramas, com fácil expansão para novos tópicos conforme o aprendizado avança.

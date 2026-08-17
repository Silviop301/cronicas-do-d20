# Publicando as Crônicas do D20 no seu domínio

O jogo é um arquivo só (`index.html`), sem servidor, sem banco de dados e sem
dependências. Publicar é copiar arquivo.

## Subindo na Hostinger

1. Entre no **hPanel** → **Sites** → seu domínio → **Gerenciador de Arquivos**.
2. Abra a pasta `public_html`.
3. Envie o `index.html` deste repositório para dentro dela.
   Se já existir um `index.html` da Hostinger lá, apague ou renomeie antes.
4. Abra o domínio no navegador. É isso.

Dá para fazer o mesmo por FTP, se preferir: os dados de acesso estão em
hPanel → Arquivos → Contas FTP.

## Colocando as imagens

O jogo procura as imagens em dois lugares e, quando não encontra, mostra o
emoji no lugar. Isso quer dizer que você pode subir a arte aos poucos, uma
criatura por vez, sem quebrar nada.

```
public_html/
├── index.html
└── img/
    ├── rato.png          ← criaturas: img/<id>.png
    ├── goblin.png
    ├── dragonete.png
    └── itens/
        ├── espada.png    ← itens: img/itens/<id>.png
        ├── sorte.png
        └── mat-ferro.png
```

Os nomes de arquivo exatos estão no guia de prompts de arte. Use PNG quadrado
com fundo transparente.

## Sobre o save

O progresso (relíquias, bestiário, conquistas, recordes) fica guardado no
`localStorage` do navegador de quem joga. Não some ao fechar a aba, mas é por
navegador e por aparelho.

Para levar o progresso de um aparelho a outro, o jogo tem
**💾 Salvar / trocar de aparelho** na tela inicial: ele gera um código que você
copia e cola no outro aparelho. Também dá para baixar como arquivo `.txt`.

Save em nuvem de verdade — a pessoa entra com uma conta e acha o progresso em
qualquer lugar — precisa de PHP e MySQL. A Hostinger oferece os dois no plano
compartilhado, então é possível: são um endpoint PHP para gravar e ler o JSON
do save e uma tabela com duas colunas. Não está feito ainda.

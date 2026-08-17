# Publicando o Climbix em climbix.app

O jogo não tem servidor, banco de dados nem dependências. Publicar é copiar
arquivo — não precisa build, não precisa Node, não precisa nada instalado.

## O que subir

| Arquivo | Obrigatório? | Para quê |
|---|---|---|
| `index.html` | sim | o jogo inteiro |
| `icone-180.png` | recomendado | ícone ao adicionar à tela de início |
| `climbix.webmanifest` | recomendado | faz abrir em tela cheia no Android |
| `img/` | opcional | arte das criaturas e itens |

Sem os dois do meio o jogo funciona igual — só fica sem ícone bonito quando
alguém salva na tela de início.

## Passo a passo na Hostinger

1. **hPanel** → **Sites**. Se `climbix.app` ainda não aparece como site,
   clique em **Adicionar site** e aponte para o domínio.
2. Entre no site → **Gerenciador de Arquivos**.
3. Abra a pasta `public_html`. Se houver um `index.html` de exemplo da
   Hostinger (a página "Website coming soon"), **apague antes** — senão ele
   continua sendo servido no lugar do jogo.
4. Envie `index.html`, `icone-180.png` e `climbix.webmanifest` para dentro
   de `public_html`.
5. Abra `https://climbix.app`. É isso.

Dá para fazer o mesmo por FTP: hPanel → **Arquivos** → **Contas FTP**.

### Confira o HTTPS

Em hPanel → **Segurança** → **SSL**, o certificado do `climbix.app` precisa
estar ativo. Ative também o redirecionamento para HTTPS — sem ele, quem
digitar `climbix.app` cai no `http://` e o navegador mostra "Não seguro".

O certificado leva alguns minutos para emitir se o domínio acabou de apontar
para a hospedagem.

### Quando atualizar o jogo depois

O navegador guarda o `index.html` em cache. Depois de subir uma versão nova,
se você ainda vir a antiga: recarregue segurando **Shift** (ou aba anônima no
celular). Quem entrar pela primeira vez sempre pega a versão nova.

## Jogar em tela cheia no celular

Vale divulgar isso junto com o link — é uma diferença grande no celular,
porque a barra do Safari come uns 15% da altura, justo onde fica o tabuleiro.

- **iPhone:** abrir `climbix.app` no Safari → botão de compartilhar →
  **Adicionar à Tela de Início**.
- **Android:** abrir no Chrome → menu de três pontos → **Instalar aplicativo**
  (ou **Adicionar à tela inicial**).

Depois disso o jogo abre como aplicativo, sem barra de endereço.

## Colocando as imagens

O jogo procura as imagens em dois lugares e, quando não encontra, mostra o
emoji no lugar. Ou seja: dá para subir a arte aos poucos, uma criatura por
vez, sem quebrar nada.

```
public_html/
├── index.html
├── icone-180.png
├── climbix.webmanifest
└── img/
    ├── rato.png          ← criaturas: img/<id>.png
    ├── goblin.png
    ├── dragonete.png
    └── itens/
        ├── espada.png    ← itens: img/itens/<id>.png
        ├── sorte.png
        └── mat-ferro.png
```

Os nomes de arquivo exatos estão no guia de prompts de arte (`arte.html`).
Use PNG quadrado com fundo transparente.

## Sobre o save

O progresso (relíquias, bestiário, conquistas, recordes) fica no
`localStorage` do navegador de quem joga. Não some ao fechar a aba, mas é por
navegador e por aparelho.

Para levar o progresso de um aparelho a outro, o jogo tem
**💾 Salvar / trocar de aparelho** na tela inicial: ele gera um código que
você copia e cola no outro aparelho.

Save em nuvem de verdade — a pessoa entra com uma conta e acha o progresso em
qualquer lugar — precisa de PHP e MySQL. A Hostinger oferece os dois no plano
compartilhado, então é possível: são um endpoint PHP para gravar e ler o JSON
do save e uma tabela com duas colunas. Não está feito ainda.

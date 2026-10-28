# Casa Mães de Coração — Landing page

Landing page institucional para uma associação sem fins lucrativos de Taboão da Serra (SP) que acolhe mulheres vítimas de violência doméstica e seus dependentes. Projeto voluntário: o conteúdo veio de material impresso e PDFs da própria ONG, e o objetivo foi dar a ela uma presença web simples, leve e fácil de manter.

**Demo:** _adicionar link do deploy_

## Stack

HTML5, CSS3 e JavaScript puro. Sem framework, sem build e sem dependências de runtime. A única requisição externa é o Google Fonts (Young Serif e Figtree, com `display=swap` e fallbacks).

## Destaques técnicos

- **Carrossel sem biblioteca:** feito com `scroll-snap` nativo, então o deslize no toque e o teclado funcionam de graça. O JS só cuida das setas (`scrollBy` de um slide mais o `gap`) e do estado `disabled` nas pontas. Há duas instâncias, uma para fotos e outra para vídeos.
- **Lightbox com `<dialog>`:** `showModal()` entrega foco preso, `Esc` e `::backdrop` sem código extra. Usa delegação de eventos no `document` e a legenda sai do `alt` da imagem.
- **Botão "Sair rápido":** fixo na tela, usa `location.replace()` para trocar a página sem deixá-la no histórico. Foi pensado para quem acessa em um ambiente onde alguém pode estar olhando.
- **Aviso de emergência:** faixa no topo com 190 e 180, visível antes de qualquer outro conteúdo.
- **Hero animado em SVG:** fitas desenhadas com `stroke-dashoffset` e coração com `scale`. Tudo respeita `prefers-reduced-motion`, assim como o scroll suave e o carrossel.
- **Tratamento de erro em vídeo:** listener em fase de captura no `document`, porque o evento `error` de `<source>` não borbulha. Mostra um aviso ao visitante e registra o caminho no console.
- **Contato direto:** links `wa.me` com mensagem pré-preenchida por tipo de ajuda (voluntariado, alimentos, roupas etc.), `tel:` e mapa do Google embutido com `loading="lazy"`.
- **Acessibilidade e semântica:** `lang="pt-BR"`, landmarks, skip link, `aria-expanded` no menu, `role="region"` com `aria-roledescription` nos carrosséis, `:focus-visible` visível e `alt` em todas as imagens.

## Design

- Paleta tirada dos materiais da ONG (magenta, azul e ciano das fitas, ameixa no lugar do preto), definida como custom properties no `:root`.
- Estrutura de página única inspirada em duas referências: o cabeçalho fixo com CTA e a hierarquia de seções de sites institucionais de ONGs.
- Componentes variados em vez de cards idênticos: linha do tempo para a história, três colunas com filete para missão, visão e causa, lista com marcadores em coração para objetivos e faixa escura para contato.
- Mobile-first, com breakpoints em 700 px (carrossel) e 860 px (menu e grades).

## Estrutura

```
index.html
script.js
css/style.css
img/      fotos (acao-N.jpg), logo.png
video/    video-N.mp4 e capas video-N.jpg
```

## Executando

Não há build. Abra o `index.html` ou sirva a pasta com qualquer servidor estático:

```bash
npx serve .
```

O deploy foi pensado para o Netlify (arraste a pasta ou conecte o repositório).

## Tratamento de mídia

- Fotos redimensionadas para no máximo 1100 px no lado maior, JPEG com qualidade 80, e `loading="lazy"`.
- Vídeos já estavam em H.264 Baseline e AAC com `moov` no início, então não precisaram de recompressão. Usam `preload="none"` e `poster` para não pesar o carregamento.
- Fotos antigas extraídas de um PDF (`pdfimages -j`), uma delas com rotação corrigida.
- Capas dos vídeos geradas com `ffmpeg -ss 1 -i video-N.mp4 -vframes 1 -vf scale=480:-2 video-N.jpg`.
- Logo provisório recortado de uma foto de camiseta e transformado em PNG transparente, normalizando o fundo pela iluminação local (filtro de máximo mais blur) e aplicando uma cor sólida.

## Privacidade

O público do site inclui mulheres em situação de vulnerabilidade, então a curadoria das imagens tentou evitar close de crianças e de pessoas atendidas. Legendas descrevem só o que se vê nas fotos, sem afirmar datas ou autoria dos eventos. A publicação de imagens com pessoas depende de autorização da ONG.


## Autor

Kauã Santos Simplício

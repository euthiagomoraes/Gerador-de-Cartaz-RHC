# Gerador de Cartaz RHC

Gerador de placas de oferta para loja de material de construção. Você informa a **descrição**, o **valor antigo** e o **valor atual**, e a placa é gerada na hora:

> **Cimento CP II 50kg** — De R$ 45,00 por **R$ 40,00**

Tudo roda no navegador, em um único arquivo `index.html`, sem servidor e sem instalação.

## Como usar

1. Abra o `index.html` no Chrome ou no Edge.
2. Na aba **Oferta**, preencha a descrição, a unidade, o valor "De" e o valor "Por".
3. Escolha o modelo e o tamanho.
4. Use **Baixar PNG**, **Baixar JPG**, **Baixar PDF** ou **Imprimir**.

Imprima sempre em **100% / tamanho real**.

## Recursos

- **5 modelos prontos:** Oferta Clássica, Faixa de Obra, Splash Vermelho, Gôndola Horizontal e Preto e Amarelo.
- **Editor de modelos:** clique numa camada da placa para movê-la, redimensioná-la, girá-la e mudar fonte, cor, alinhamento e forma. Camadas disponíveis: texto, preço, forma (retângulo, elipse, estrela/splash, faixa listrada), imagem e logo da loja.
- **Campos automáticos nos textos:** `{descricao}`, `{unidade}`, `{de}`, `{por}`, `{economia}`, `{pct}`, `{validade}`, `{extra}`, `{loja}`, `{contato}`.
- **Ajuste automático:** o texto encolhe e quebra linhas para caber no espaço reservado.
- **Valor antigo opcional:** camadas marcadas como "só aparece com valor antigo" somem quando não há preço "De".
- **Qualquer tamanho:** de A6 a A2, cartazes 33×48, 45×63 e 66×96 cm, ou medida personalizada em mm.
- **Montagem para impressão:**
  - placas menores que a folha são encaixadas várias por folha A4, A3, Carta ou Ofício, com marcas de corte;
  - placas maiores são divididas em partes com sobreposição, para colar.
- **Lote:** cole uma lista no formato `descrição ; valor antigo ; valor atual ; unidade` (ou colunas copiadas do Excel) e gere um PDF único ou um `.zip` com as imagens PNG.
- **Resolução:** 150, 200 ou 300 dpi.
- **Exportar e importar modelos** em `.json`.

Modelos personalizados, logo, dados da loja e a lista do lote ficam salvos no próprio navegador (localStorage). Para levar um modelo para outro computador, use **Exportar .json** e **Importar .json**.

## Exemplo de lista para o lote

```
Cimento CP II 50kg ; 45,00 ; 40,00 ; Saco 50 kg
Argamassa AC-II 20kg ; 22,90 ; 18,90 ; Saco 20 kg
Tijolo baiano 9 furos ; 890,00 ; 799,00 ; Milheiro
Vergalhão CA-50 10mm ; 54,90 ; 47,90 ; Barra 12 m
```

## Estrutura de um modelo

Cada modelo é um JSON com fundo e camadas. Posições e tamanhos ficam em **% da placa**, então o mesmo modelo se adapta a qualquer formato.

```json
{
  "name": "Oferta Clássica",
  "orient": "retrato",
  "bg": { "c1": "#FFD400", "c2": "#FFB800", "gradient": false, "img": "" },
  "layers": [
    { "type": "shape", "shape": "rect", "x": 0, "y": 0, "w": 100, "h": 18, "fill": "#D6001C" },
    { "type": "text", "text": "OFERTA", "x": 4, "y": 2, "w": 92, "h": 14, "font": "Anton", "color": "#FFFFFF" },
    { "type": "text", "text": "De R$ {de}", "strike": true, "requireDe": true, "x": 5, "y": 44, "w": 60, "h": 7 },
    { "type": "price", "field": "por", "x": 4, "y": 58, "w": 92, "h": 29, "color": "#D6001C" }
  ]
}
```

## Tecnologia

- HTML, CSS e JavaScript puro, com renderização em `<canvas>`.
- [jsPDF](https://github.com/parallax/jsPDF) para PDF e [JSZip](https://github.com/Stuk/jszip), ambos via CDN.
- Fontes do Google Fonts: Anton, Archivo Black, Oswald, Bebas Neue, Barlow Condensed e Roboto Condensed.

Requer internet na primeira abertura para carregar fontes e bibliotecas.

## Próximos passos

- Cadastro de produtos com preço base e busca.
- Campanhas com histórico para reimprimir.
- Foto do produto e QR code na placa.
- PDF com texto vetorial.

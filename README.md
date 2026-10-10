# Jogo da Vida Ternário

Uma variação do Jogo da Vida de Conway com **três estados** em vez de dois. Além de vivo e morto, existe um estado intermediário, o *fraco*, que funciona como camada de proteção: uma célula forte precisa falhar duas vezes antes de morrer. O projeto inclui um simulador que roda direto no navegador, em um único arquivo HTML, sem dependências.

Autor: Yudhi Gerson

## Estados

| Estado | Nome | Símbolos | Cor |
|---|---|---|---|
| 0 | Morto | `•` / `D` / `0` | Branco (célula sem pintura) |
| 1 | Fraco | `□` / `W` / `1` | Cinza |
| 2 | Forte | `■` / `S` / `2` | Preto |

## Regras

A vizinhança é de 8 células (Moore) e as bordas da grade são mortas.

1. **Nascimento.** Uma célula morta com exatamente 3 vizinhos vivos (fracos ou fortes) nasce **fraca**.
2. **Forte.** Se tiver menos de 2 ou mais de 3 vizinhos fortes, vira fraca. Caso contrário, continua forte.
3. **Fraco.**
   - Com 3 ou mais vizinhos fortes, faz *upgrade* e vira forte.
   - Senão, com menos de 2 ou mais de 3 vizinhos fracos, morre.
   - Senão, continua fraco.
4. **Escudo (Still Life).** Um fraco no centro que **já era fraco na geração anterior** forma um escudo se estiver cercado por um destes padrões:

   ```
   ■■■     ■•■     •■•
   ■□■     •□•     ■□■
   ■■■     ■•■     •■•
   ```

   (8 fortes, 4 fortes nas diagonais com os retos mortos, ou 4 fortes em cruz com as diagonais mortas.)

   Enquanto o padrão existir, o quadrado 3×3 inteiro fica congelado e nenhuma célula morta encostada no escudo pode nascer. Os escudos aparecem com contorno laranja.

## O que não existe no Conway

- Três estados, com a morte acontecendo em dois passos (forte, depois fraco, depois morto).
- Promoção: uma célula pode melhorar de fraco para forte.
- Memória: o escudo exige que o centro já tenha sido fraco antes.
- Contagem por tipo de vizinho, e não só por quantidade.
- Padrões geométricos: no escudo, a posição dos vizinhos importa.
- Regiões congeladas e protegidas contra nascimentos.

## Simulador

Abra `jogo-da-vida-ternario.html` em qualquer navegador moderno.

- **Pincel:** escolha Apagar, □ ou ■ e toque ou arraste na grade para pintar. Célula sem pintura é morta.
- **Iniciar / Pausar, Passo, Voltar:** controlam a simulação. Voltar desfaz até 300 gerações.
- **Aleatório e Limpar:** preenchem a grade com um sorteio ou a esvaziam.
- **Exemplo de escudo:** carrega os três padrões do escudo para você conferir que ficam parados.
- **Salvar / Carregar:** guarda padrões no navegador (`localStorage`), no aparelho onde você salvou.
- **Velocidade:** controla o intervalo entre gerações.

### Comparação com o Conway binário

O simulador roda o Conway clássico em paralelo, em segundo plano, a partir do mesmo desenho (fraco e forte contam como vivo). O texto abaixo da grade informa se o padrão é igual ao binário ou desde qual geração ele diverge. Com a caixa de seleção ativa, células vivas que o binário não teria ganham um ponto rosa.

Uma divergência só é contada quando muda vivo contra morto; uma diferença só de tipo (forte contra fraco) não conta.

## Limitações conhecidas

- A grade é fixa, de 28×28, com bordas mortas (não é toroidal).
- A regra do forte conta só vizinhos fortes, e a do fraco conta só vizinhos fracos para morrer.
- O escudo congela por decreto, em vez de o Still Life surgir da própria dinâmica; é a parte que mais se afasta de um autômato celular puro.
- Ainda não foram feitos experimentos longos para catalogar osciladores ou naves próprios do ternário.

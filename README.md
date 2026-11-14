# Maré Dourada

Jogo de surf em 3D numa baía ao pôr do sol. Ande pela praia, pegue a prancha, reme até o pico e surfe ondas que abrem em tubo, fecham tudo ou quebram na beira.

## Baixar e jogar (Windows)

1. Vá em **[Releases](../../releases/latest)** e baixe `MareDourada-win64.exe`.
2. Dê dois cliques. Não precisa instalar nem de internet.
3. Se o Windows mostrar "O Windows protegeu o computador", clique em **Mais informações → Executar assim mesmo** (o arquivo não é assinado digitalmente).

Precisa do Microsoft Edge WebView2, que já vem no Windows 10 e 11.

## Comandos

| Tecla | O que faz |
| --- | --- |
| W A S D | andar, remar e virar |
| Shift | correr |
| E | pegar ou largar a prancha · sair da onda |
| Espaço | ficar de pé na onda · aéreo subindo a parede |
| A / D | manobras (cavada, rasgada, batida, cutback) |
| W surfando | bombear (só rende na descida) |
| S surfando | estolar (ficar fundo no tubo) |
| Mouse / roda | girar a câmera / zoom |
| T | fim de tarde ou meio-dia |
| O | ajustes de gráficos, efeitos e ondas |
| R | voltar para a areia |

## O que tem

- Sete tipos de onda: pico, direita, esquerda, fechadeira, cheia, laje e beira.
- O lábio do tubo cai em queda livre (tempo ≈ √(2H/g)) e explode em spray quando bate na água.
- Espraiamento, refluxo, maré e areia molhada baseados em Stockdon et al. (2006).
- Manobras reconhecidas pela posição na parede, com pontos que premiam variedade.
- Ajustes de gráficos (Baixo a Ultra), efeitos de câmera e tamanho das ondas.

## Rodar a partir do código

O jogo é um único `resources/index.html` com three.js r128 em `resources/js/`. Para gerar o executável com [Neutralinojs](https://neutralino.js.org):

```bash
npx @neutralinojs/neu@11.8.0 update
npx @neutralinojs/neu@11.8.0 build --embed-resources
```

O `.exe` sai em `dist/mare-dourada/`.

# Maré Dourada

Jogo de surf em 3D numa baía ao pôr do sol. Ande pela praia, pegue a prancha, reme até o pico e surfe ondas que abrem em tubo, fecham tudo ou quebram na beira.

## Jogar no navegador

**[heitorcoser.github.io/mare-dourada](https://heitorcoser.github.io/mare-dourada/)** — funciona no PC e no celular.

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
| Espaço remando para o fundo | duck dive: fura a onda (segure para ficar embaixo) |
| W na vaca | nadar para cima |
| A / D | manobras (cavada, rasgada, batida, cutback) |
| W surfando | bombear (só rende na descida) |
| S surfando | estolar (ficar fundo no tubo) |
| Mouse / roda | girar a câmera / zoom |
| T | fim de tarde ou meio-dia |
| O | ajustes de gráficos, efeitos e ondas |
| R | voltar para a areia |

## O que tem

- Doze tipos de onda: pico, direita, esquerda, fechadeira, cheia, laje, beira, ponta (point break), dupla (double-up), cunha (wedge do molhe), de fora (a bomba rara da série) e surgente (sobe a areia sem quebrar, pelo número de Iribarren).
- O lábio é o topo da própria onda: a parede do tubo nasce na face, é arremessado em queda livre (tempo ≈ √(2H/g)) e desaba em espuma quando bate na água.
- Vaca com mini ragdoll: o corpo solto (juntas bola-e-soquete) é levado pela água, com empuxo, arrasto, espuma empurrando para a praia e o redemoinho da água branca. A prancha fica presa na cordinha.
- Duck dive para furar a espuma e o lábio quando você rema para o fundo.
- Regras de tubo justas: dá para estolar lá dentro; a vaca só vem se o lábio cair em você ou se o tubo desabar com você dentro.
- Câmera que nunca entra embaixo d'água e maré contínua, sem saltos.
- Multiplayer online quando o jogo é aberto como artefato no claude.ai: todo mundo na mesma praia e no mesmo mar, com placar. No site e no `.exe` o jogo roda em modo de um jogador.
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

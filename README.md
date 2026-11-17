# Maré Dourada

Jogo de surf em 3D numa baía ao pôr do sol. Ande pela praia, pegue a prancha, reme até o pico e surfe ondas que abrem em tubo, fecham tudo ou quebram na beira.

## Jogar no navegador

**[heitorcoser.github.io/mare-dourada](https://heitorcoser.github.io/mare-dourada/)** — funciona no PC e no celular.

## Baixar o app (Android e Windows)

Em **[Releases](../../releases/latest)**:

- **Android:** baixe `MareDourada.apk` no celular e abra. Se pedir, permita "instalar apps desconhecidos" para o navegador.
- **Windows:** baixe `MareDourada-win64.exe` e dê dois cliques. Se aparecer "O Windows protegeu o computador", clique em **Mais informações → Executar assim mesmo** (o arquivo não é assinado digitalmente). Precisa do Microsoft Edge WebView2, que já vem no Windows 10 e 11.

**Atualização automática:** com internet, os apps abrem a versão mais nova do jogo direto deste site, então toda novidade chega sozinha, sem baixar nada. Sem internet, eles abrem a cópia do jogo que vem dentro do app. Quando sair um app novo, o jogo mostra um aviso com o link para baixar.

### Publicar uma versão nova dos apps

Crie e envie uma tag (`git tag v1.2.0 && git push origin v1.2.0`). O workflow `release.yml` monta o APK (Gradle) e o EXE (Neutralinojs) no GitHub e publica a release. O APK é assinado com a chave de debug fixa em `android/debug.keystore`, para cada APK novo instalar por cima do anterior; para usar uma chave privada, crie os segredos `ANDROID_KEYSTORE_B64` (o .jks em base64) e `ANDROID_KEYSTORE_PASS` no repositório.

## Multiplayer

1. Aperte **P** (ou o botão **Multiplayer**), escreva seu nome e clique em **Criar sala**.
2. Passe o **código** (ex.: `K7QXM`) para os amigos, ou clique em **Copiar convite** e mande o link.
3. Os amigos abrem o jogo, apertam **P**, digitam o código e clicam em **Entrar**. Até 8 surfistas por sala.

Funciona pela internet, no PC e no celular, sem VPN e sem estar na mesma rede. É a mesma técnica do [Losters](https://github.com/Heitorcoser/Losters): [PeerJS](https://peerjs.com) (WebRTC), com o servidor gratuito do PeerJS só para os aparelhos se acharem, STUN para atravessar o roteador e um servidor TURN gratuito quando a rede não deixa conectar direto. Cada surfista manda só o próprio estado; o mar é igual para todos porque as ondas são uma conta do tempo, e o relógio e as regras das ondas são de quem criou a sala. Se quem criou a sala sair, ela acaba.

Aberto como artefato no claude.ai, o jogo usa a sala do próprio claude.ai: quem tem acesso ao link e está logado cai na mesma praia automaticamente.

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
| P | multiplayer (criar ou entrar numa sala) |
| R | voltar para a areia |

## O que tem

- Cinco praias, escolhidas por quem criou a sala (o fundo decide como a onda quebra):
  - **Praia do Farol**: areia, de tudo um pouco (até 2,5×).
  - **Baía Mansa**: fundo suave, ondas cheias para treinar (até 1,5×).
  - **Recife da Laje**: pedra rasa, tubos grossos e rápidos (até 3×).
  - **Ponta do Molhe**: promontório e molhe, paredes longas e cunhas (até 2,5×).
  - **Canhão**: um cânion no fundo junta a energia, como em Nazaré. Ondas gigantes de até 5× (o dobro do limite das outras), que passam de 20 m nas séries e quebram lá fora.
- Doze tipos de onda: pico, direita, esquerda, fechadeira, cheia, laje, beira, ponta (point break), dupla (double-up), cunha (wedge do molhe), de fora (a bomba rara da série) e surgente (sobe a areia sem quebrar, pelo número de Iribarren).
- O lábio é o topo da própria onda: a parede do tubo nasce na face, é arremessado em queda livre (tempo ≈ √(2H/g)) e desaba em espuma quando bate na água.
- Vaca com mini ragdoll: o corpo solto (juntas bola-e-soquete) é levado pela água, com empuxo, arrasto, espuma empurrando para a praia e o redemoinho da água branca. A prancha fica presa na cordinha.
- Duck dive para furar a espuma e o lábio quando você rema para o fundo.
- Regras de tubo justas: dá para estolar lá dentro; a vaca só vem se o lábio cair em você ou se o tubo desabar com você dentro.
- Câmera que nunca entra embaixo d'água e maré contínua, sem saltos.
- Multiplayer online sem VPN, no site, no `.exe` e no claude.ai: todo mundo na mesma praia e no mesmo mar, com placar e avisos das manobras e vacas dos outros.
- Espraiamento, refluxo, maré e areia molhada baseados em Stockdon et al. (2006).
- Manobras reconhecidas pela posição na parede, com pontos que premiam variedade.
- Ajustes de gráficos (Baixo a Ultra), efeitos de câmera e tamanho das ondas.

## Rodar a partir do código

O jogo é um único `resources/index.html` com three.js r128 e PeerJS 1.5.4 (licença MIT em `resources/js/PEERJS-LICENSE`) em `resources/js/`. Para gerar o executável com [Neutralinojs](https://neutralino.js.org):

```bash
npx @neutralinojs/neu@11.8.0 update
npx @neutralinojs/neu@11.8.0 build --embed-resources
```

O `.exe` sai em `dist/mare-dourada/`.

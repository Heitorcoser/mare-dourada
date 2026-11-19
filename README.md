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

Aperte **P** (ou o botão **Multiplayer**) e escreva seu nome. Há dois tipos de sala:

**Sala pública** (como no Gorilla Tag)
- **Entrar numa sala pública**: o jogo acha uma sala aberta com gente jogando, ou abre uma nova.
- **Ver salas abertas** mostra a lista com o código e quantos surfistas há em cada uma; dá para entrar também digitando o código público ou por um link `?publica=CÓDIGO`.
- Até 10 surfistas. Tudo passa por um servidor público de mensagens (MQTT: HiveMQ, com o Mosquitto de reserva), então **ninguém vê o IP de ninguém**. Tem chat de texto e não tem voz.
- A segurança é fraca de propósito: qualquer um que souber o código entra. Por isso nada pessoal viaja: só apelido, posição, placar e chat.

**Sala com amigos** (com voz)
1. **Criar sala** gera um código (ex.: `K7QXM`). Passe o código ou clique em **Copiar convite**.
2. Os amigos digitam o código e clicam em **Entrar**. Até 8 surfistas.
3. **Ligar a voz** e segurar **V** para falar. O volume cai com a distância na praia. A voz liga os aparelhos direto (PeerJS/WebRTC, a mesma técnica do [Losters](https://github.com/Heitorcoser/Losters)), então os amigos da sala veem o IP uns dos outros: use só com quem você conhece.

Em qualquer sala: **Enter** abre o chat de texto (120 letras, uma mensagem a cada 1,2 s) e cada jogador pode ser **silenciado** na janela do Multiplayer. Quem entrou primeiro (★) escolhe a praia, o tamanho e os tipos de onda para todos.

Aberto como artefato no claude.ai, o jogo usa a sala do próprio claude.ai: quem tem acesso ao link e está logado cai na mesma praia automaticamente (com chat de texto; salas públicas e voz só no site e nos apps).

## Brechas (F8)

Mods que mudam o jogo **só no seu aparelho**: velocidade, gravidade da Lua, nunca tomar vaca, prancha gigante, andar sobre a água e "minhas ondas" (usar os seus ajustes de onda mesmo sem ser o anfitrião). Os outros veem um selo "mod" no seu nome, mas o jogo deles continua normal. Não existe console para colar código, para ninguém conseguir te enganar e rodar algo que leia os seus dados.

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
| Enter | chat de texto |
| V (segurar) | falar no chat de voz (sala com amigos) |
| F8 | brechas (mods só no seu jogo) |
| R | voltar para a areia |
| G | ir para o pico: deitado na prancha, logo além de onde a próxima onda vai quebrar |
| Q | replay da última onda (Shift: câmera lenta · C: troca a câmera · Esc ou Q: sai) |

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
- Replay de cada onda com câmeras de cinema (atrás, do canal, de lado e drone) e câmera lenta. O mar do replay é o mesmo daquele momento, porque as ondas são uma conta do tempo.
- Botão **Pico (G)** que leva você direto para onde a próxima onda vai quebrar.
- Regras de tubo justas: dá para estolar lá dentro; a vaca só vem se o lábio cair em você ou se o tubo desabar com você dentro.
- Câmera que nunca entra embaixo d'água e maré contínua, sem saltos.
- Multiplayer online sem VPN, no site, no `.exe` e no claude.ai: todo mundo na mesma praia e no mesmo mar, com placar e avisos das manobras e vacas dos outros.
- Espraiamento, refluxo, maré e areia molhada baseados em Stockdon et al. (2006).
- Manobras reconhecidas pela posição na parede, com pontos que premiam variedade.
- Ajustes de gráficos (Baixo a Ultra), efeitos de câmera e tamanho das ondas.

## Rodar a partir do código

O jogo é um único `resources/index.html` com three.js r128 e PeerJS 1.5.4 e mqtt.js 5.10.1 (licenças MIT em `resources/js/PEERJS-LICENSE` e `resources/js/MQTT-LICENSE`) em `resources/js/`. Para gerar o executável com [Neutralinojs](https://neutralino.js.org):

```bash
npx @neutralinojs/neu@11.8.0 update
npx @neutralinojs/neu@11.8.0 build --embed-resources
```

O `.exe` sai em `dist/mare-dourada/`.

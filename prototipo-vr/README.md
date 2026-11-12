# Consultório VR — protótipos de teste

Experiências de realidade virtual para uso no consultório, com a terapeuta presente. Rodam no navegador do celular (testado para o Galaxy S7 em visor tipo Gear VR ou Cardboard), sem depender do app Oculus.

| Página | O que é |
|---|---|
| `index.html` | Página inicial com as experiências |
| `mar.html` | **Mar Passo a Passo**: exposição gradual para fobia de água |
| `praia.html` | **Praia Calma**: relaxamento com respiração guiada |

Os arquivos `mar-passo-a-passo.html` e `praia-calma.html` são as mesmas páginas no formato de página do Claude, sem o cabeçalho HTML. Ao editar, altere esses arquivos e regenere `mar.html` e `praia.html` com o mesmo conteúdo.

## Mar Passo a Passo

Caminhada guiada da areia até dentro do mar em 9 etapas: areia seca, pés na água, joelhos, coxas, cintura, peito, pescoço, desafio debaixo d’água e boiar.

- **Cena 3D realista**: céu com simulação física da luz do sol (modelo de Preetham) e nuvens, ondas de Gerstner andando para a praia, textura real de ondulação, reflexo do céu, transparência que muda com a profundidade, espuma na beira, areia molhada que reflete o céu, cáusticas no fundo, morro com farol, veleiro, gaivotas, peixes e boias.
- **Caminhar pelo olhar**: para avançar, a pessoa olha firme para um círculo e caminha até a próxima etapa, com vinheta suave para reduzir enjoo.
- **Tarefas de atenção**: encontrar o guarda-sol (lugar seguro), olhar para cima, para a esquerda, para a direita e para os pés, ver as ondas nas pernas, achar três peixes, acompanhar uma onda e olhar a boia salva-vidas de apoio.
- **Desafio debaixo d’água**: 1 ou 2 minutos no fundo, com relógio, respiração guiada (4 s inspirando, 6 s soltando), bolhas a cada expiração, raios de luz e um botão “Subir agora” sempre disponível.
- **Avaliação**: escala de medo de 0 a 10 em cada etapa. Se o medo for 7 ou mais, a sessão propõe respirar antes de seguir. O desafio é registrado como concluído, em parte ou não iniciado, com o tempo alcançado, e a pessoa responde se conseguiu manter a respiração calma.
- **Som**: mar com áudio espacial (mar aberto à frente, arrebentação na praia), passos na areia, passos e água nas pernas conforme a profundidade, onda batendo nos pés, som abafado e bolhas debaixo d’água, música de fundo suave (pode ser desligada) e narração em português.

## Créditos

- three.js r128 (MIT), incluindo a textura `assets/waternormals.jpg` e o modelo de céu do `Sky.js`.

## Dicas de teste

- Abra no **Chrome** do celular, com HTTPS, para o giroscópio funcionar.
- Acrescente `#rapido` ao endereço para a sessão correr 10 vezes mais rápido e concluir sozinha as tarefas de olhar.

## Abrir no celular

`qr-celular.png` é um QR code que abre a página inicial do teste no navegador do celular.

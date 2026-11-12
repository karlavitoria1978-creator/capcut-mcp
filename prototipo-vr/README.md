# Protótipo VR — Praia Calma

Teste de uma sessão de relaxamento em realidade virtual para uso clínico, feito para rodar no navegador de um celular comum (testado para o Galaxy S7 em visor tipo Gear VR ou Cardboard). Não depende do app Oculus.

## O que tem no teste

- Praia em 360° desenhada em código (sem arquivos de vídeo), com reflexo do sol e espuma em movimento.
- Som do mar com áudio espacial: o mar fica à frente e o som acompanha o giro da cabeça.
- Narração por voz em português (voz do próprio celular).
- Respiração guiada 4-6 (inspira 4 s, solta 6 s) com um círculo em volta do sol, 6 ciclos.
- Escala de ansiedade de 0 a 10 antes e depois, marcada só com o olhar.
- Botões **Pausar** e **Sair** perto dos pés.
- Modo óculos (tela dividida) e modo celular (olhar arrastando o dedo ou girando o celular).
- Exemplo do aviso que a terapeuta receberia no Slack e do resumo da sessão (ainda simulados, sem envio real).

## Arquivos

- `index.html`: página completa, para abrir direto no navegador do celular.
- `praia-calma.html`: o mesmo conteúdo no formato de página do Claude (sem o cabeçalho HTML).

Ao editar, altere `praia-calma.html` e regenere o `index.html` com o mesmo conteúdo.

## Dicas de teste

- Abra no **Chrome** do celular, com conexão HTTPS, para o giroscópio funcionar.
- Acrescente `#rapido` ao fim do endereço para a sessão correr 10 vezes mais rápido (útil para revisar o fluxo).

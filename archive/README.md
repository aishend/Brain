# Arquivo — código útil removido do projeto oficial

Esta pasta guarda código que **já existiu nos repositórios oficiais ECC-BFMC e foi
removido**, mas que nos pode ser útil na BFMC 2027. Nada disto corre no Brain atual;
é material de referência e reaproveitamento.

Tudo foi extraído do histórico público do GitHub (Brain e Shared). Não contém segredos:
as chaves privadas de teste (`privatekey_*_test.pem`) que acompanhavam os servidores
simulados foram deixadas de fora de propósito — são chaves de teste publicadas no starter
kit, não as chaves reais do servidor da competição. Se precisarem delas para correr os
simuladores antigos, estão no histórico público; não as commitem aqui.

## `v2x-legacy-2d5dc80/` — o V2X anterior (até out 2026)

A versão do submódulo `src/data` que o Brain usava antes de a Bosch passar para WebSocket.

- `Semaphores/` — cliente dos **semáforos por UDP (porta 5007)**. A Bosch removeu o
  processo dos semáforos do Brain em out 2026. Se este ano os semáforos ainda
  transmitirem por UDP, este código pode ser recuperado como componente nosso.
  Confirmar no fórum.
- `TrafficCommunication/` — o cliente antigo por **UDP (descoberta) + TCP**, com
  validação por chave pública RSA (`keyDealer`, `.pem`). Substituído pelo cliente
  WebSocket atual. Útil como referência do protocolo e dos campos enviados.

## `startup-2023/` — o projeto "startup" de 2023

Snapshot de peças úteis da versão antiga do projeto (commit `6f7777d~1`), antes da
reescrita para a arquitetura atual. Muita coisa continua a aplicar-se.

- **`src/hardware/camera/CameraSpooferProcess.py`** — alimenta o pipeline com **vídeo
  gravado** de uma pasta, em vez da câmara real. Peça-chave para desenvolver a visão
  no PC com imagens reais da pista. Adaptar à arquitetura de mensagens atual.
- **`test/localisationsystemSERVER/`** — **servidor de localização simulado** (UWB).
  Simula o que, na pista, dá a posição do carro. Referência para testar o V2X em casa.
- **`test/livetrafficSERVER/`** — **servidor de tráfego simulado** (o "live traffic",
  tipo Waze). Recebe os dados que o carro reporta. Referência do protocolo antigo.
- **`test/trafficlightSIM/Simulator.py`** — **simulador de semáforos**.
- **`test/vehicletovehicleSIM/`** — simulador de V2V (carro-a-carro).
- **`src/utils/remotecontrol/`** — **controlo por teclado** (RcBrain + listener): mapeia
  teclas para comandos de velocidade/direção, com passos de PID. Útil para condução
  manual e para debug rápido sem o dashboard.
- **`src/data/localisationssystem/`**, **`livetraffic/`**, **`trafficlights/`**,
  **`vehicletovehicle/`** — os clientes antigos correspondentes, com exemplos de uso.
- **`src/hardware/IMU/imu.py`** — tratamento antigo da IMU.

## Avisos

- **Protocolos antigos:** os servidores simulados de `startup-2023/` e o cliente de
  `v2x-legacy-2d5dc80/` usam UDP/TCP, não o WebSocket atual. Servem de referência e para
  montar os nossos próprios simuladores; não falam com o servidor real da competição.
- **Nada de comunicação não autorizada:** durante as corridas só é permitido o que o
  regulamento autoriza. Este código é para desenvolvimento e teste em casa.

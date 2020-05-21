# Manual do usuário

How to compile and run:

```
make master
make outstation
./outstation    # in one terminal
./master        # in another terminal
```

Clean up with `make clean`.

At the moment it doesn't do much, just opens a socket and transmits garbage from
one side to another. TODO: update this text.

# Requisitos:
## Objetivo:

- Desenvolver um programa que simule uma remota DNP3 que responda a função FC 01 (Read).
- Ao enviar um telegrama o programa deverá executar as seguintes validações: CRC () e  o endereço da remota.

Segue exemplo um exemplo de FC (01) do mestre a remota:

### Envio do mestre:

    link layer magic: 0x05 0x64
    link layer len: 0x0b
    link layer ctrl: 0xc4
    link layer dst: 0x46 0x00
    link layer src: 0x40 0x00
    link layer crc: 0xa3 0xfe
    transport layer: 0xd0
    APP data chunk:
       |  app layer ctrl:           0xcd
       |  app layer function code:  0x01 (read)
       |  object type group:        0x3c (Object group 60)
       |  object type variation:    0x02 (variation 2)
       |  qualifier field:          0x06 (always 0x06, see A26.1.2.1)
       |  CRC: 0xc2 0x62

### Resposta da remota:

    0x05 0x64 0x33 0x44 0x40 0x00 0x46 0x00 0xe5 0xb4 0xd0 0xed 0x81 0x06 0x00
    0x04 0x02 0x28 0x04 0x00 0xe0 0x00 0x81 0x99 0xd7 0x74 0xbd 0xc2 0x10 0x72
    0x01 0xdc 0x00 0x81 0x99 0xd7 0x74 0x10 0x72 0x01 0xdf 0x00 0x81 0x99 0x1e
    0x9a 0xd7 0x74 0x10 0x72 0x01 0xe1 0x00 0x81 0x99 0xd7 0x74 0x10 0x72 0x01
    0xbd 0xf5

## Entrega:
Publique o aplicativo no github, faça pequenos commits para indicar evolução do trabalho ao longo do tempo, descreva no readme como testar o programa e implemente testes unitários.

## Prazo de entrega:
23:59 22/05/2020

## Referências fornecidas:
- https://www.dnp.org/About/Overview-of-DNP3-Protocol
- https://www.electron.com.br/arquivos/artigos-tecnicos/dnp.pdf

## Referências adicionais:
- https://en.wikipedia.org/wiki/DNP3 (overview)
- https://github.com/ITI/ICS-Security-Tools/tree/master/pcaps (capturas de pacotes DNP3 para facilitar o entendimento)
- https://www.ixiacom.com/company/blog/scada-distributed-network-protocol-dnp3 (diagrama do DNP3 sobre IP)

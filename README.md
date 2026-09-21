# Pintos

Pintos é um sistema operacional de ensino para x86, desenvolvido originalmente na
Stanford. Este repositório partiu do jhu-cs318/pintos e contém as implementações das
atividades da disciplina de Infraestrutura de Software (Cesar School).

## Implementações

- **Alarm Clock (Implementação 4)** — reescrita de timer_sleep() em devices/timer.c sem
  busy wait: threads dormem em uma lista ordenada por tempo de despertar e o manipulador
  da interrupção do temporizador (timer_interrupt()) acorda as que venceram. Adicionado o
  campo wake_time em struct thread (threads/thread.h) e a lista ordenada em timer.c.

## Estrutura

- src/ — código-fonte do Pintos
- evidencias.log — registro das sessões de execução (via script -a)
- vchlm/... — códigos e evidências empacotados para a entrega da atividade

## Compilação e testes

Compilar (na subpasta src/threads, pois ela gera a imagem build/):

    cd src/threads
    make clean && make

Rodar um teste (ex.: alarm-single):

    cd build
    pintos -v -k -T 60 --qemu -- -q run alarm-single

Os seis testes da atividade são alarm-single, alarm-multiple, alarm-simultaneous,
alarm-priority, alarm-zero e alarm-negative.

## Arquivos alterados (Implementação 4)

- src/threads/thread.h — campo int64_t wake_time
- src/devices/timer.c — lista sleeping_list, comparador timer_sleep_less(),
  timer_sleep() sem bloqueio e despertar no timer_interrupt()
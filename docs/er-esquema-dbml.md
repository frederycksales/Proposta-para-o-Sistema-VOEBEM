# Esquema Entidade-Relacionamento (ER) - Sistema VOEBEM

Este documento descreve a estrutura do banco de dados relacional proposto para o sistema VOEBEM, mostrando as entidades principais, seus atributos e os relacionamentos entre elas.

## Diagrama ER

![Diagrama ER - VOEBEM](../assets/er-diagram-voebem.svg)

*(Nota: O diagrama SVG acima representa visualmente o esquema definido abaixo.)*

## Descrição das Entidades e Relacionamentos

### Entidades

#### PASSAGEIRO
Representa uma pessoa que faz uma reserva.
-   `id_passageiro` (INTEGER): Chave primária, auto-incremento.
-   `nome` (VARCHAR): Nome do passageiro, não nulo.

#### RESERVA
Representa uma reserva feita por um passageiro para um ou mais trechos de voo.
-   `id_reserva` (INTEGER): Chave primária, auto-incremento.
-   `codigo_reserva` (VARCHAR): Código único da reserva, não nulo.
-   `data_criacao` (DATETIME): Data e hora de criação da reserva, não nulo (padrão: data/hora atual).
-   `data_emissao` (DATETIME): Data e hora de emissão (confirmação) da reserva, pode ser nulo.
-   `prazo_validade` (DATETIME): Prazo limite para confirmação da reserva, não nulo.
-   `status` (VARCHAR): Status atual da reserva (Ex: Pendente, Confirmada, Cancelada, Emitida), não nulo.
-   `prorrogada` (BOOLEAN): Indica se o prazo de validade foi prorrogado, não nulo (padrão: false).
-   `passageiro_id` (INTEGER): Chave estrangeira referenciando o passageiro que fez a reserva, não nulo.
-   `fonte_reserva` (VARCHAR): Origem da reserva (Ex: Interno, Web, GDS_Amadeus), pode ser nulo.
-   `id_externo_reserva` (VARCHAR): ID da reserva no sistema externo (Ex: GDS PNR), pode ser nulo.
-   `id_transacao_pagamento` (VARCHAR): ID da transação no sistema de pagamento, pode ser nulo.
-   `status_pagamento` (VARCHAR): Status do pagamento (Ex: Pendente, Aprovado, Falhou), pode ser nulo.
-   `valor_pago` (DECIMAL): Valor efetivamente pago pela reserva, pode ser nulo.

#### VOO
Representa um voo como uma sequência de trechos, com origem e destino finais.
-   `id_voo` (INTEGER): Chave primária, auto-incremento.
-   `codigo_voo` (VARCHAR): Código único do voo, não nulo.
-   `aeroporto_origem_final` (INTEGER): Chave estrangeira referenciando o aeroporto de origem final do voo, não nulo.
-   `aeroporto_destino_final` (INTEGER): Chave estrangeira referenciando o aeroporto de destino final do voo, não nulo.

#### TRECHO
Representa um segmento individual de um voo, conectando dois aeroportos com uma aeronave específica.
-   `id_trecho` (INTEGER): Chave primária, auto-incremento.
-   `voo_id` (INTEGER): Chave estrangeira referenciando o voo ao qual este trecho pertence, não nulo.
-   `ordem_trecho` (INTEGER): Ordem do trecho dentro do voo, não nulo (compõe chave única com `voo_id`).
-   `aeroporto_origem_id` (INTEGER): Chave estrangeira referenciando o aeroporto de origem deste trecho, não nulo.
-   `aeroporto_destino_id` (INTEGER): Chave estrangeira referenciando o aeroporto de destino deste trecho, não nulo.
-   `aeronave_id` (INTEGER): Chave estrangeira referenciando a aeronave usada neste trecho, não nulo.

#### VOO_DIA_SEMANA
Indica em quais dias da semana um voo específico opera e seus horários.
-   `voo_id` (INTEGER): Chave primária composta, chave estrangeira referenciando o voo.
-   `dia_semana` (INTEGER): Chave primária composta, dia da semana (0=Domingo, 6=Sábado).
-   `hora_partida` (TIME): Hora de partida neste dia da semana, não nulo.
-   `hora_chegada` (TIME): Hora de chegada neste dia da semana, não nulo.

#### CIDADE
Representa uma cidade.
-   `id_cidade` (INTEGER): Chave primária, auto-incremento.
-   `codigo_cidade` (VARCHAR): Código único da cidade (Ex: SAO), não nulo.
-   `nome` (VARCHAR): Nome da cidade, não nulo.

#### AEROPORTO
Representa um aeroporto.
-   `id_aeroporto` (INTEGER): Chave primária, auto-incremento.
-   `codigo_iata` (VARCHAR): Código IATA único do aeroporto (Ex: GRU), não nulo.
-   `nome` (VARCHAR): Nome do aeroporto, não nulo.
-   `cidade_id` (INTEGER): Chave estrangeira referenciando a cidade onde o aeroporto está localizado, não nulo.

#### AERONAVE
Representa uma aeronave.
-   `id_aeronave` (INTEGER): Chave primária, auto-incremento.
-   `modelo` (VARCHAR): Modelo da aeronave, não nulo.
-   `fabricante` (VARCHAR): Fabricante da aeronave.
-   `capacidade_total` (INTEGER): Capacidade total de passageiros da aeronave, não nulo.

#### ASSENTO
Representa um assento individual em uma aeronave.
-   `id_assento` (INTEGER): Chave primária, auto-incremento.
-   `aeronave_id` (INTEGER): Chave estrangeira referenciando a aeronave à qual o assento pertence, não nulo.
-   `numero_assento` (VARCHAR): Número/identificação do assento (compõe chave única com `aeronave_id`), não nulo.
-   `classe` (VARCHAR): Classe do assento (Ex: Econômica, Executiva), não nulo.

#### RESERVA_TRECHO
Tabela associativa que liga uma RESERVA a um TRECHO específico que faz parte dessa reserva.
-   `reserva_id` (INTEGER): Parte da chave primária composta, chave estrangeira referenciando a RESERVA.
-   `trecho_id` (INTEGER): Parte da chave primária composta, chave estrangeira referenciando o TRECHO.
-   `data_hora_partida` (DATETIME): Data e hora de partida programada para este trecho na reserva, não nulo.
-   `data_hora_chegada` (DATETIME): Data e hora de chegada programada para este trecho na reserva, não nulo.
-   `classe_reservada` (VARCHAR): Classe em que o assento foi reservado para este trecho, não nulo.

#### RESERVA_ASSENTO
Tabela associativa que liga um `RESERVA_TRECHO` a um `ASSENTO` específico reservado para uma data de voo particular.
-   `reserva_id` (INTEGER): Parte da chave primária composta, chave estrangeira referenciando `RESERVA_TRECHO`.
-   `trecho_id` (INTEGER): Parte da chave primária composta, chave estrangeira referenciando `RESERVA_TRECHO`.
-   `assento_id` (INTEGER): Parte da chave primária composta, chave estrangeira referenciando o ASSENTO, não nulo.
-   `data_voo` (DATE): Data específica em que este trecho do voo está sendo reservado para este assento (compõe chave única com `assento_id` e `trecho_id`), não nulo.
-   `status_checkin` (VARCHAR): Status do check-in para este assento/trecho (Ex: Pendente, Realizado), pode ser nulo.

### Relacionamentos

-   `PASSAGEIRO` **faz** uma ou mais (`o{`) `RESERVA`s.
-   `RESERVA` **contem_trecho** um ou mais (`o{`) `RESERVA_TRECHO`s.
-   `TRECHO` **eh_reservado_em** zero ou mais (`o{`) `RESERVA_TRECHO`s.
-   `VOO` **composto_por** um ou mais (`o{`) `TRECHO`s.
-   `AEROPORTO` pode ser a **origem_de** zero ou mais (`o{`) `TRECHO`s.
-   `AEROPORTO` pode ser o **destino_de** zero ou mais (`o{`) `TRECHO`s.
-   `AERONAVE` é **usado_em** zero ou mais (`o{`) `TRECHO`s.
-   `VOO` **opera_em** um ou mais (`o{`) `VOO_DIA_SEMANA`s.
-   `CIDADE` é **localizado_em** zero ou mais (`o{`) `AEROPORTO`s.
-   `AERONAVE` **possui** um ou mais (`o{`) `ASSENTO`s.
-   `AEROPORTO` pode ser a **origem_final_em** zero ou mais (`o{`) `VOO`s.
-   `AEROPORTO` pode ser o **destino_final_em** zero ou mais (`o{`) `VOO`s.
-   `RESERVA_TRECHO` tem um **assento_reservado_para** zero ou mais (`o{`) `RESERVA_ASSENTO`s.
-   `ASSENTO` é **reservado_em** zero ou mais (`o{`) `RESERVA_ASSENTO`s.

## Esquema DBML

Abaixo está o esquema do banco de dados definido usando a sintaxe DBML (Database Markup Language).

```dbml
Table PASSAGEIRO {
  id_passageiro integer [pk, increment]
  nome varchar(255) [not null]
}

Table RESERVA {
  id_reserva integer [pk, increment]
  codigo_reserva varchar(50) [unique, not null]
  data_criacao datetime [default: `now()`, not null]
  data_emissao datetime [null]
  prazo_validade datetime [not null]
  status varchar(50) [not null, note: 'Pendente, Confirmada, Cancelada, Expirada']
  prorrogada boolean [default: false, not null]
  passageiro_id integer [not null]

  Indexes {
    (codigo_reserva)
  }
}

Table VOO {
  id_voo integer [pk, increment]
  codigo_voo varchar(10) [unique, not null]
  aeroporto_origem_final integer [not null]
  aeroporto_destino_final integer [not null]
  Indexes {
    (codigo_voo)
  }
}

Table TRECHO {
  id_trecho integer [pk, increment]
  voo_id integer [not null]
  ordem_trecho integer [not null, note: 'Sequência do trecho dentro do voo (1, 2, ...)']
  aeroporto_origem_id integer [not null]
  aeroporto_destino_id integer [not null]
  aeronave_id integer [not null, note: 'Aeronave planejada para este trecho']

  Indexes {
    (voo_id, ordem_trecho) [unique]
  }
}

Table VOO_DIA_SEMANA {
  voo_id integer [pk]
  dia_semana integer [pk, note: '0=Domingo, 1=Segunda,..., 6=Sábado']
  hora_partida time [not null]
  hora_chegada time [not null]
}

Table CIDADE {
  id_cidade integer [pk, increment]
  codigo_cidade varchar(3) [unique, not null, note: 'Ex: SAO, RIO']
  nome varchar(100) [not null]

  Indexes {
    (codigo_cidade)
  }
}

Table AEROPORTO {
  id_aeroporto integer [pk, increment]
  codigo_iata varchar(3) [unique, not null, note: 'Ex: GRU, GIG, POA']
  nome varchar(150) [not null]
  cidade_id integer [not null]

  Indexes {
    (codigo_iata)
  }
}

Table AERONAVE {
  id_aeronave integer [pk, increment]
  modelo varchar(100) [not null]
  fabricante varchar(100)
  capacidade_total integer [not null]
}

Table ASSENTO {
  id_assento integer [pk, increment]
  aeronave_id integer [not null]
  numero_assento varchar(5) [not null, note: 'Ex: 1A, 20F']
  classe varchar(50) [not null, note: 'Econômica, Executiva, Primeira Classe']

  Indexes {
    (aeronave_id, numero_assento) [unique]
  }
}

Table RESERVA_TRECHO {
  reserva_id integer [pk]
  trecho_id integer [pk]
  data_hora_partida datetime [not null, note: 'Data e hora exatas da partida deste trecho para esta reserva']
  data_hora_chegada datetime [not null, note: 'Data e hora exatas da chegada deste trecho para esta reserva']
  classe_reservada varchar(50) [not null, note: 'Classe específica reservada para este trecho (pode ser diferente da classe do assento)']
}

Table RESERVA_ASSENTO {
  reserva_id integer [pk]
  trecho_id integer [pk]
  assento_id integer [pk, not null]
  data_voo date [not null, note: 'Data específica do voo para esta reserva de assento']

  Indexes {
    (assento_id, trecho_id, data_voo) [unique]
  }
}

Ref: RESERVA.passageiro_id > PASSAGEIRO.id_passageiro
Ref: RESERVA_TRECHO.reserva_id > RESERVA.id_reserva
Ref: RESERVA_TRECHO.trecho_id > TRECHO.id_trecho
Ref: TRECHO.voo_id > VOO.id_voo
Ref: TRECHO.aeroporto_origem_id > AEROPORTO.id_aeroporto
Ref: TRECHO.aeroporto_destino_id > AEROPORTO.id_aeroporto
Ref: TRECHO.aeronave_id > AERONAVE.id_aeronave
Ref: VOO_DIA_SEMANA.voo_id > VOO.id_voo
Ref: AEROPORTO.cidade_id > CIDADE.id_cidade
Ref: ASSENTO.aeronave_id > AERONAVE.id_aeronave
Ref: VOO.aeroporto_origem_final > AEROPORTO.id_aeroporto
Ref: VOO.aeroporto_destino_final > AEROPORTO.id_aeroporto
Ref: RESERVA_ASSENTO.(reserva_id, trecho_id) > RESERVA_TRECHO.(reserva_id, trecho_id)
Ref: RESERVA_ASSENTO.assento_id > ASSENTO.id_assento
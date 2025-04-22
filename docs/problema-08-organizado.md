# Problema 8 - Requisitos Estruturados

## 1. Visão Geral do Sistema

*   **Objetivo:** Desenvolver um sistema de reservas em nuvem para a companhia de aviação VOEBEM.
*   **Arquitetura:**
    *   Banco de dados centralizado.
    *   Acesso por aplicações clientes internas e externas à companhia.

## 2. Entidade Principal: Reserva

*   **Identificação:** Código único gerado pelo sistema.
*   **Passageiro:** Associada a um único passageiro (identificado apenas pelo nome).
*   **Composição:** Conjunto de trechos de voos.
*   **Atributos por Trecho:** Data/hora específica, classe (econômica, executiva, etc.).
*   **Validade:**
    *   Possui prazo de validade.
    *   Cancelada automaticamente se os bilhetes não forem emitidos até o prazo.
    *   Pode ser prorrogada.
*   **Reserva de Assento:**
    *   Permitida devido ao check-in informatizado.
    *   Pode ser feita com até três meses de antecedência.

## 3. Entidade: Voo

*   **Identificação:** Código único.
*   **Rota:** Possui origem e destino definidos.
*   **Composição:** Formado por um ou mais trechos (escalas).
    *   *Exemplo:* Voo 595 (POA -> SP) composto pelos trechos POA -> Londrina e Londrina -> SP.
*   **Operação:**
    *   Pode não operar em todos os dias da semana.
    *   Pode ter pequenas variações de horário em dias específicos.

## 4. Entidade: Trecho de Voo

*   **Definição:** Representa uma etapa de um voo entre duas localidades (escalas).
*   **Aeroportos:** Deve especificar o aeroporto de origem e destino (relevante para cidades com múltiplos aeroportos).
*   **Aeronave:**
    *   Tipo de aeronave associado ao trecho é uma informação relevante para o cliente.
    *   Possibilidade de troca de aeronave em escalas (principalmente voos internacionais).

## 5. Consultas Requeridas pelo Sistema

O sistema deve permitir as seguintes consultas:

a)  **Possibilidades de Viagem:** Buscar opções de voo entre uma cidade/aeroporto de origem e um destino.
b)  **Viagem por Dia da Semana:** Idem ao item (a), mas com filtro por dias específicos da semana.
c)  **Horários de Voo:** Consultar horários de chegada ou saída para voos específicos.
d)  **Disponibilidade de Vagas:** Verificar a disponibilidade geral de vagas em um trecho de voo específico.
e)  **Disponibilidade de Assentos:** Verificar a disponibilidade de assentos específicos em um trecho de voo.
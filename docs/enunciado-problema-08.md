# Problema 8

Precisamos propor uma arquitetura para um sistema em nuvem para a empresa de aviação VOEBEM que precisa de um sistema de reservas para uma companhia de aviação. O sistema contará com um banco de dados central, que será acessado por aplicações clientes, rodando tanto dentro da própria companhia quanto fora dela.

A transação central do sistema é a reserva. Uma reserva é identificada por um código gerado pelo sistema em computador. A reserva é feita para um único passageiro, do qual se conhece apenas o nome. A reserva compreende um conjunto de trechos de voos, que acontecerão em determinada data/hora. Para cada trecho, a reserva é feita em uma classe (econômica, executiva, etc.).

Um voo é identificado por um código e possui uma origem e um destino. Por exemplo, o voo 595 sai de Porto Alegre com destino a São Paulo. Um voo é composto de vários trechos, correspondendo às escalas intermediárias do voo. Por exemplo, o voo 595 é composto de dois trechos, um de Porto Alegre a Londrina, o outro de Londrina a São Paulo.

Cabe salientar que há cidades que são servidas por vários aeroportos. Por isso, é importante informar ao passageiro que faz a reserva, qual é o aeroporto no qual o voo passa. Às vezes os clientes, ao fazer a reserva, querem saber qual é o tipo de aeronave que será utilizada em determinado trecho de voo. Alguns poucos voos, principalmente internacionais, têm troca de aeronave em determinadas escalas.

Nem todos os voos operam em todos os dias das semanas. Inclusive, certos voos têm pequenas mudanças de horário em certos dias da semana.

Cada reserva possui um prazo de validade. Caso os bilhetes não tenham sido emitidos, até esgotar-se o prazo da reserva, ela é cancelada. Reservas podem ser prorrogadas.

Como o check-in de todos os voos está informatizado, a companhia possibilita a reserva de assento para o passageiro. Reservas de assento podem ser feitas com até três meses de antecedência.

Além de efetivar reservas, o sistema deve servir para vários tipos de consultas que os clientes podem querer fazer:
a) Possibilidades de viagem de uma cidade ou de um aeroporto para outro
b) O mesmo, mas restrito a determinados dias da semana
c) Horários de chegada ou de saída em determinados voos
d) Disponibilidade de vagas em um trecho de voo
e) Disponibilidade de determinados assentos em um trecho de voo.

Projetar um esquema ER para essa aplicação e desenhe um diagrama ER para esse esquema. Especifique atributos chaves para cada tipo de entidade e restrições estruturais em cada tipo de relacionamento. Verifique quaisquer requisitos não especificados e realize os pressupostos apropriados para tornar completas as especificações.
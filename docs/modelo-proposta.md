PONTIFÍCIA UNIVERSIDADE CATÓLICA DE MINAS GERAIS
PUC Minas Virtual

ATIVIDADE DE NIVELAMENTO
<nome do Projeto>

<nome(s) do(s) aluno(s)>

Belo Horizonte
<mês e ano>.
NIVELAMENTO SRE

Sumário

NIVELAMENTO SRE
1.	Arquitetura do Sistema - Diagrama C4
2.	Estratégia de Deploy e Resiliência
3.	Plano de Melhoria da Confiabilidade e Percepção do Cliente

 
# 1. Arquitetura do Sistema - Diagrama C4

Os alunos devem mapear a estrutura da solução utilizando a metodologia C4 Model, contemplando:

*   **Nível 1 (Contexto):** Descrever os principais componentes do sistema (usuários, serviços, integrações externas).
*   **Nível 2 (Container):** Definir quais serviços compõem a aplicação (frontend, backend, bancos de dados, APIs, sistemas externos).
*   **Nível 3 (Componentes):** Explicar os principais módulos internos dos serviços críticos e como se relacionam.

**Destaques obrigatórios:** Estratégia de escalabilidade (horizontal, vertical), balanceamento de carga e abordagem para alta disponibilidade.

# 2. Estratégia de Deploy e Resiliência

A equipe deve definir um processo de deploy seguro e automatizado, garantindo que mudanças não comprometam a disponibilidade. Devem ser abordados:

*   **Pipeline CI/CD**
*   **Estratégia de deploy**
*   **Técnicas para rollback seguro**

# 3. Plano de Melhoria da Confiabilidade e Percepção do Cliente

A empresa precisa recuperar a confiança dos clientes.

A equipe deve propor um plano para mitigar falhas e melhorar a experiência de uso.

O planejamento deve incluir:

*   **Monitoramento e Observabilidade:**
    *   Quais métricas (SLIs, SLOs) devem ser implementadas?
    *   Quais ferramentas (Prometheus, Grafana, ELK, Datadog, etc.)?
*   **Automação de recuperação:**
    *   Como a infraestrutura pode reagir automaticamente a falhas?
    *   Uso de auto-healing, escalonamento dinâmico, Chaos Engineering.
*   **Gestão de Incidentes:**
    *   Como reduzir o tempo médio de detecção (MTTD) e tempo médio de recuperação (MTTR)?
*   **Feedback dos clientes:**
    *   Estratégias para coletar e responder a problemas percebidos pelo usuário.
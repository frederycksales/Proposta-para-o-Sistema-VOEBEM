# 2. Estratégia de Deploy e Resiliência

Esta seção detalha as estratégias propostas para garantir entregas de software frequentes, confiáveis e com baixo risco para o Sistema VOEBEM, abordando o pipeline de CI/CD, a metodologia de deploy em produção e o plano de rollback.

## 2.1 Pipeline de CI/CD (Integração Contínua / Entrega Contínua)

Propõe-se um pipeline de CI/CD robusto para automatizar o processo de build, teste e deploy dos diferentes containers (microsserviços, frontend) do sistema, conforme ilustrado abaixo.

*   **Ferramentas Propostas:**
    *   **Controle de Versão:** Git (com repositórios hospedados no GitLab ou GitHub).
    *   **Servidor de CI/CD:** GitLab CI/CD ou GitHub Actions (integrados à plataforma de repositórios).
    *   **Containerização:** Docker (para empacotar as aplicações e suas dependências).
    *   **Registro de Container:** Docker Hub, GitLab Container Registry, AWS ECR ou similar.
    *   **Orquestração de Containers:** Kubernetes (gerenciado na nuvem, Exemplo: AWS EKS, Google GKE, Azure AKS).
    *   **Ferramentas de Teste:** JUnit (para Java/API Reservas), PyTest (para Python/API Voos), Jest/Cypress (para Frontend React).
    *   **Análise de Código (Opcional):** SonarQube (para análise estática de segurança e qualidade).

*   **Fluxo do Pipeline:** O diagrama abaixo ilustra as etapas sequenciais e pontos de decisão do pipeline, desde o commit do código até o deploy em produção, incluindo validações intermediárias.

    ![Diagrama do Pipeline de CI/CD](../assets/diagrama-cicd.svg)

*   **Etapas Detalhadas:**
    1.  **Commit & Trigger:** Desenvolvedor envia código, iniciando o pipeline.
    2.  **Build & Unit Test:** Compilação e testes unitários. Falhas interrompem o pipeline.
    3.  **Code Scan (Opcional):** Análise estática de código.
    4.  **Build da Imagem Docker:** Criação da imagem da aplicação.
    5.  **Push para Registro:** Envio da imagem para o registro.
    6.  **Deploy em Staging:** Implantação em ambiente de homologação.
    7.  **Testes de Integração/Aceitação:** Validação funcional e de integração em Staging. Falhas interrompem o pipeline.
    8.  **Aprovação (Manual/Automática):** Ponto de controle antes da produção.
    9.  **Deploy em Produção:** Implantação em produção usando a estratégia Blue/Green.
    10. **Monitoramento Pós-Deploy:** Observação ativa da nova versão em produção.

## 2.2 Estratégia de Deploy

Considerando a criticidade do sistema e a necessidade de minimizar riscos e downtime, a estratégia de deploy recomendada é **Blue/Green Deployment**, cujo fluxo é apresentado no diagrama a seguir.

*   **Justificativa:**
    *   **Zero Downtime:** Transição suave de tráfego.
    *   **Testes em Produção Isolados:** Validação da nova versão sem impacto no usuário.
    *   **Rollback Instantâneo:** Reversão rápida em caso de problemas.
    *   **Simplicidade Conceitual:** Fluxo claro para deploy e rollback.

*   **Funcionamento (Ilustrado no Diagrama):**

    ![Diagrama da Estratégia Blue/Green](../assets/diagrama-bluegreen.svg)

    1.  **Ambiente Blue Ativo:** Versão atual (v1) recebe o tráfego.
    2.  **Provisionamento Green:** Nova versão (v2) é implantada em um ambiente idêntico (Green).
    3.  **Testes no Green:** Validação da v2 no ambiente Green isolado.
    4.  **Switch de Tráfego:** Se os testes passarem, o tráfego é direcionado para o ambiente Green (v2).
    5.  **Monitoramento do Green:** A v2 é monitorada em produção.
    6.  **Estabilização ou Rollback:** Se a v2 estiver estável, o ambiente Blue (v1) é desativado. Se problemas críticos forem detectados, o tráfego é revertido imediatamente para o Blue (v1) (Rollback).
    7.  **Desativação do Blue:** Após confirmação da estabilidade do Green, o ambiente Blue é liberado.

*   **Benefícios para VOEBEM:** Essa abordagem minimiza o risco de impacto ao usuário durante atualizações e permite reversões imediatas caso surjam problemas inesperados, garantindo assim a continuidade das operações críticas de reserva e a confiança do cliente.

## 2.3 Estratégia de Rollback

A estratégia de rollback é uma parte intrínseca do fluxo Blue/Green, como visualizado no diagrama anterior.

*   **Processo de Rollback (Detalhado):**
    1.  **Detecção de Problema:** Identificação de falha crítica na versão Green (v2) ativa, via monitoramento ou alertas.
    2.  **Acionamento:** Manual pela equipe SRE/Operações ou automático por violação de SLOs.
    3.  **Redirecionamento de Tráfego:** Reconfiguração do Load Balancer/Roteador para enviar 100% do tráfego de volta ao ambiente Blue (v1), que contém a versão estável anterior. Esta é a ação principal e imediata do rollback.
    4.  **Análise de Causa Raiz:** Investigação do problema no ambiente Green (v2), agora isolado.
    5.  **Correção e Novo Deploy:** Após correção, o ciclo de deploy pode ser reiniciado.

*   **Garantias:**
    *   **Velocidade:** MTTR minimizado pela rapidez do redirecionamento.
    *   **Segurança:** Versão estável anterior sempre disponível.
    *   **Consistência:** Processo claro e passível de automação.

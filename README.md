# Proposta de Sistema VOEBEM - Atividade de Nivelamento SRE PUC Minas Virtual

Este repositório contém os artefatos desenvolvidos para a atividade de nivelamento da disciplina de SRE (Site Reliability Engineering) da Pós-Graduação em Arquitetura de Software Distribuído da PUC Minas Virtual.

## Objetivo da Atividade

O objetivo desta atividade foi elaborar uma proposta técnica para um sistema de reservas de uma companhia aérea fictícia, a VOEBEM. A proposta aborda desafios comuns em sistemas distribuídos, focando em arquitetura, resiliência, deploy e confiabilidade, sob a ótica de SRE.

## Conteúdo da Proposta

A proposta detalha os seguintes aspectos principais, conforme solicitado no [modelo da atividade](docs/modelo-proposta.md):

1.  **Arquitetura do Sistema:** Utilizando o C4 Model ([Nível 1](assets/c4-n1-contexto.png), [Nível 2](assets/c4-n2-container.png), [Nível 3](assets/c4-n3-component-api-reservas.png)) para descrever o contexto, containers e componentes da solução.
2.  **Estratégia de Deploy e Resiliência:** Definição de um pipeline CI/CD, estratégias de deploy (como Blue/Green) e técnicas de rollback.
3.  **Plano de Melhoria da Confiabilidade:** Abordagem para monitoramento (SLIs/SLOs), automação de recuperação, gestão de incidentes (MTTD/MTTR) e coleta de feedback do cliente.

## Documento Final

**A proposta consolidada e formatada encontra-se no arquivo [Proposta-sistema-voebem.pdf](Proposta-sistema-voebem.pdf) na raiz deste repositório.**

## Estrutura do Repositório

*   `/`: Contém o PDF final da proposta e este README.
*   `assets/`: Imagens e diagramas gerados (SVG, PNG, PDF).
*   `diagrams/`: Código fonte dos diagramas (PlantUML, Mermaid, etc.).
*   `docs/`: Arquivos de apoio, rascunhos e o modelo da proposta.
*   `latex-src/`: Código fonte LaTeX utilizado para gerar o documento PDF final.
*   `md-files/`: Arquivos Markdown usados como base para o conteúdo LaTeX.

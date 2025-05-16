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

## Como Gerar o Documento PDF

Para gerar o arquivo `Proposta-sistema-voebem.pdf` a partir dos fontes LaTeX:

1.  **Pré-requisitos:**
    *   Possuir uma distribuição LaTeX instalada (por exemplo, MiKTeX para Windows, TeX Live para Linux/macOS).
    *   O utilitário `latexmk` (geralmente incluído nas distribuições LaTeX).

2.  **Passos para Compilação:**
    *   Abra um terminal e navegue até o diretório `latex-src/`:
        ```shell
        cd latex-src
        ```
    *   Execute o comando `latexmk`:
        ```shell
        latexmk -pdf 00-proposta-sistema-voebem.tex
        ```
        Para uma compilação forçada, utilize:
        ```shell
        latexmk -f -pdf 00-proposta-sistema-voebem.tex
        ```
        Isso gerará o arquivo `00-proposta-sistema-voebem.pdf` dentro da pasta `latex-src/`.

3.  **Documento Final:**
    *   O principal artefato da proposta é o arquivo `Proposta-sistema-voebem.pdf` localizado na raiz do repositório.
    *   Após a compilação bem-sucedida, o arquivo `00-proposta-sistema-voebem.pdf` gerado em `latex-src/` deve ser copiado para a raiz do projeto e renomeado para `Proposta-sistema-voebem.pdf`. Este passo pode ser manual.

## Estrutura do Repositório

*   `/`: Contém o PDF final da proposta e este README.
*   `assets/`: Imagens e diagramas gerados (SVG, PNG, PDF).
*   `diagrams/`: Código fonte dos diagramas (PlantUML, Mermaid, etc.).
*   `docs/`: Arquivos de apoio, rascunhos e o modelo da proposta.
*   `latex-src/`: Código fonte LaTeX utilizado para gerar o documento PDF final.
*   `md-files/`: Arquivos Markdown usados como base para o conteúdo LaTeX.

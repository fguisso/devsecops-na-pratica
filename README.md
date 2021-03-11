# devsecops-na-pratica
Este repositorio é apenas um exemplo de como adicionar OWASP ZAP Actions em uma pipeline de DevOps.

##  DAST - Dynamic Application Security Testing ou Teste de segura de aplicativo dinâmico

Este teste só é realizado em aplicações dinâmicos ou melhor dizendo, em aplicações que estão funcinando.

O motivo disso é que neste contexto você pode explorar situações que talvez não possam ser obtidas antes de rodar a aplicação ou no Code Review.

## OWASP ZAP

A ferramenta que iremos utilizar neste exemplo é o OWASP ZAP, um DAST muito poderoso que tem inumeraas funções e pode nos ajudar no momento de testar nossa aplicação. Esta ferramenta fornece uma interface grafica, mas também uma API e ferramentas CLI, que serão as utilizadas no momento.

## Github Actions

As Actions são comandos em sequencia utilizados para montar uma pipeline no CI/CD do Github, muitos dessas Actions são open source, possibilitando que a comunidade se ajudee criando cada vez mais opções de sequencias para as pipelines.

Neste caso, usaremos uma Action pronta do OWASP ZAP, que já implementa as sequencias do CLI e espera apenas alguns parametros para configuração final.

No momento, existem apenas duas Actions prontas do OWASP ZAP, mas você pode criar sua propria configuração do zero se precisar, basta analisar o código das Actions já exitentes.

- [OWASP ZAP Action Baseline Scan](https://github.com/marketplace/actions/owasp-zap-baseline-scan), esta Action roda apenas um reconhecimento basico da aplicação sem aplicar nenhuma regra de ataque e possibilita a configuração de alguns alertas de segurança.
- [OWASP ZAP Action Full Scan](https://github.com/marketplace/actions/owasp-zap-full-scan), já aqui nossa Action roda varias funções de reconhecimento e de ataque da ferramenta, podendo levar muito mais tempo para finalizar a tarefa.

Vamos utilizar o `full scan` apenas para visualizar todos os possiveis resultados da ferramenta.

## Github Actions Workflow

Quando colocamos um arquivo de configuração YML dentro de um diretorio chamado `.github/workflows`, automaticamento o Github Actions vai interpretar estas configurações e executar de acordo. Você pode [clicar aqui](https://github.com/fguisso/devsecops-na-pratica/tree/main/.github/workflows) para verficar como ficou nossa configuração final. Lembrando que estamos utilizando a aplicação, já em produção, OWASP Juice Shop, que é outro projeto da OWASP para simular um eCommerce com vulnerabilidades, para ser o nosso `target`: http://demo.owasp-juice.shop/

Nossa Action agora espera que o fluxo da pipeline seja executada toda vez que ocorrer ou um `push` na master, ou um PR e ainda pode ser disparada direto pelo dashboard de Actions.

Assim que a ferramenta terminar de executar, ela ira abrir uma Issue com um resumo dos resultados e seguindo o link para a execução da Actions, podemos baixar o Artifact, que neste caso é o report da ferramenta OWASP ZAP daa maneira convencional.

Você pode verificar a Issue criada no primeiro Scan neste link: https://github.com/fguisso/devsecops-na-pratica/issues/1
Para analisar o job deste primeiro scan, acesse este link: https://github.com/fguisso/devsecops-na-pratica/actions/runs/641418788
E para baixar o Artifact deste job, só clicar e fazer o download do .zip que contem o resultado em formato Markdown, JSON ou HTML para melhor visualização: https://github.com/fguisso/devsecops-na-pratica/suites/2230937725/artifacts/46242565

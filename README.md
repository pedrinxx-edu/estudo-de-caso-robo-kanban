# Robô Kanban: estudo de caso

> O código é de uso interno de um escritório de advocacia e fica em repositório privado. Aqui está como o projeto funciona e o que ele resolveu, sem dados da empresa.

## O problema
Uma equipe de 5 pessoas com 11 quadros e mais de 800 cards. Muitos cards sem prazo, sem início, sem descrição ou parados sem explicação. Atualizar tudo à mão tomava tempo e acabava não sendo feito.

## A solução
Uma ferramenta local (Python + Flask), aberta como aplicativo no computador de cada pessoa:

- **Relato → mudanças**: a pessoa escreve o que fez (ou usa os próprios commits do Git). A IA lê o relato e os cards abertos e propõe ações: comentar, mover de coluna, ajustar datas, trocar responsáveis ou criar card. **Nada é aplicado sem a pessoa confirmar.**
- **Conferência**: encontra cards com problema e sugere datas por prioridade, pulando fins de semana, feriados e férias e respeitando um limite de vencimentos por dia.
- **Carga da equipe**: quantos cards cada pessoa tem, quantos atrasados e críticos, e sugestão de redistribuição.
- **Cobrança automática** de cards parados ou atrasados, no máximo uma vez por semana por card.
- **Histórico com desfazer**: toda alteração fica registrada e pode ser revertida, desde que o card não tenha mudado depois.
- **Painel e relatórios**: entregas por semana, evolução da qualidade do planejamento e relatório semanal/mensal.

## Decisões técnicas
- Login com **Playwright** (inclui 2FA). Depois, as chamadas vão direto na API do sistema com **requests**, reaproveitando a sessão: muito mais rápido que clicar na tela.
- **IA com regras rígidas**: só usa o que está no relato e nos cards, nunca inventa datas ou nomes e, na dúvida, devolve um "aviso" em vez de agir.
- **Segurança**: servidor só em 127.0.0.1, token por sessão, conferência de origem e permissões por papel (coordenação × equipe).
- **Pacote para Windows e Mac** com o navegador embutido, encerramento automático por inatividade e mensagens de erro em português simples.

## Tecnologias
Python · Flask · Playwright · requests · pandas · Claude Code (CLI) · HTML/JS · Chart.js

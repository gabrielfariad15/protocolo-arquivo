# Protocolo de Arquivo

Aplicação de solicitação e controle de empréstimo de documentos de arquivo, construída em Power Apps (canvas), Microsoft Dataverse e Power Automate.

**Situação: em construção.** Este repositório registra o projeto desde o primeiro dia. O que já está pronto e o que falta está na seção Andamento, mais abaixo.

## O problema

Num arquivo institucional, o pedido de documento costuma chegar por e-mail, telefone ou conversa de corredor. Alguém de outro setor precisa de um documento, o arquivista localiza a caixa no acervo, entrega e depois controla a devolução. Nada disso fica registrado de forma que se possa medir: não se sabe quanto tempo um pedido leva, qual setor mais demanda, quantos pedidos saem do prazo nem com que frequência um documento simplesmente não é encontrado.

Este projeto transforma esse processo em registro. Cada pedido tem situação, prazo e responsável, e o conjunto vira indicador.

O domínio vem da minha rotina de trabalho com gestão documental. Todos os dados usados aqui são fictícios; nenhum documento ou informação de acervo real faz parte deste repositório.

## Modelo de dados

Três tabelas no Dataverse.

**Solicitação** é a tabela central. Guarda quem pediu e de qual setor, o que foi pedido (descrição, tipo documental e período de referência), a urgência, o prazo de atendimento calculado na criação (2 dias úteis se normal, 1 se urgente), a situação, as datas de entrega e devolução, o atendente e a caixa do acervo que atendeu o pedido.

A situação percorre: Recebida, Em localização, Localizada, Entregue, Devolvida, ou termina em Não localizada.

**Acervo** registra onde cada caixa está: identificação, tipo documental, ano inicial e final, endereço físico em quatro campos (rua, estante, prateleira e posição) e se a caixa está disponível ou emprestada.

**Setor** guarda o nome do setor e o responsável. Existe para que os indicadores saiam agrupados corretamente, sem o mesmo setor escrito de três formas diferentes.

## Indicadores

1. Solicitações abertas por situação, que mostra onde está o gargalo.
2. Tempo médio de atendimento, em dias.
3. Solicitações por setor.
4. Percentual atendido dentro do prazo.
5. Taxa de não localização. Mede a organização do acervo, e não o desempenho do atendente: se uma parcela fixa dos pedidos termina sem o documento, o problema está na organização física.

## Andamento

- [ ] Ambiente de desenvolvimento e solução `ProtocoloArquivo` com publicador próprio
- [ ] Tabelas, relacionamentos e dados fictícios
- [ ] App canvas: nova solicitação, lista com busca e filtro, detalhe com mudança de situação
- [ ] Fluxos: aviso de nova solicitação e confirmação de entrega
- [ ] Tela de indicadores
- [ ] Solução exportada e desempacotada em `src/`, capturas de tela

## Estrutura do repositório

- `src/` recebe a solução desempacotada com a Power Platform CLI (`pac solution unpack`), em arquivos de texto versionáveis
- `solucao/` recebe os pacotes `.zip` exportados
- `capturas/` recebe as imagens das telas e dos fluxos
- `documentacao/` guarda o planejamento do projeto

## Fora do escopo desta versão

Painel em Power BI, app model-driven sobre as mesmas tabelas, leitura do código da caixa pela câmera, aprovação em duas etapas para documento sigiloso e relatório mensal em PDF.

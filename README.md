# Razão · Controladoria da safra

Painel de controladoria para usina sucroenergética: resultado, simulação de margem, custo de produção, GR/IR e fechamento contábil.

O diferencial é o botão **SAP** em cada número. Ele abre uma gaveta que mostra de onde o dado vem no S/4HANA: transação, filtros, colunas, tabela na SE16N, frequência de atualização e área responsável. Quando o dado vem de fora do SAP (boletim industrial, laboratório, cotações), a gaveta diz de quem pedir.

> Todos os números são fictícios, só para demonstração. Nenhum dado real de empresa foi usado.

## Telas

| Tela | O que responde |
|---|---|
| Visão geral | Como está o resultado da safra contra o orçado? |
| Simulador de margem | O que acontece com o EBITDA se preço, câmbio, moagem ou custo mudarem? |
| Custo de produção | Por que o custo por tonelada subiu: diluição, preço ou consumo? |
| GR/IR | O que está parado entre Compras e Contabilidade, por quê e com quem? |
| Fechamento contábil | Em que dia está o fechamento, o que atrasou e o que isso trava? |
| Dicionário SAP | De onde vem cada número do painel? |

### Visão geral
- KPIs com sparkline: receita líquida, EBITDA, custo por tonelada, custo por saca, moagem e saldo GR/IR
- Ponte do EBITDA (orçado → realizado), receita por produto e receita mensal orçado × realizado
- Alertas clicáveis e orçado × realizado por centro de custo
- Filtro de mês (acumulado da safra de abril até o mês escolhido)

### Simulador de margem
- Nove premissas: moagem, ATR, mix, açúcar NY nº 11, câmbio, etanol, custo agrícola, custo industrial e despesas fixas
- Cenários orçamento, otimista e pessimista, com transição animada
- Leitura automática do resultado e KPIs contra o orçamento
- Ponte do EBITDA orçamento → cenário (soma exata, efeito de cada premissa)
- Sensibilidade de ±10% em cada premissa
- Paridade açúcar × etanol por kg de ATR (fatores Consecana)

### Custo de produção
- Leitura automática: quanto do aumento é diluição pela moagem e quanto é preço
- Ponte do custo por tonelada: orçado → diluição → preço → consumo → outros → amortização → real
- Composição do custo por tonelada (CCT, tratos, plantio, indústria, amortização)
- Efeito preço × efeito consumo por insumo, contra o orçado flexível
- Pareto dos estouros com corte de 80%
- Tabela de desvio por insumo e curva ABC dos materiais, com filtro, busca e ordenação

### GR/IR
- Leitura automática: recebido sem nota, faturado sem entrada e itens parados
- Idade do saldo e evolução na safra
- Causa de cada item em aberto, com o responsável e a transação que resolve
- Plano de limpeza com caixas de marcar (fica salvo no navegador)
- Os 40 maiores itens em aberto, com filtros, busca, ordenação e exportação em CSV
- Saldo por fornecedor e adiantamentos a fornecedor

### Fechamento contábil
- Leitura automática do dia do fechamento, das tarefas atrasadas e do que elas travam
- Cronograma de D−1 a D+5 com 24 tarefas, coluna de hoje, filtro por área e caminho crítico
- Cada tarefa abre a gaveta com passos, transação SAP, dependências e o que ela libera
- Tempo de fechamento contra a meta de 5 dias úteis, com ajustes manuais depois do corte
- Andamento por área e conciliação das contas (saldo contábil × fonte)

### Dicionário SAP
- Todas as origens do painel numa tabela só: dado, tela, transações, tabela, frequência e responsável
- Nuvem de transações: clique em uma para ver onde ela aparece
- Busca, filtro por tela e exportação em CSV para entregar à TI

## Recursos gerais

- **Modo TV**: botão no topo. Abre em tela cheia, gira entre as cinco telas a cada 20 segundos, rola cada uma até o fim e anima o simulador entre os cenários. Sai com Esc ou com o botão "Sair do modo TV".
- **Tema claro e escuro**, no rodapé do menu (a escolha fica salva).
- **Celular**: o menu vira gaveta e as tabelas rolam na horizontal.
- **Coerência entre telas**: o saldo GR/IR, os itens parados, o custo por tonelada e os adiantamentos batem entre as telas.

## Como trocar pelos dados reais

Os dados ficam no início de cada bloco do `<script>`, em listas simples:

| Bloco | Variáveis |
|---|---|
| Visão geral | `D` (série mensal), `PONTE`, `PROD`, `CC` |
| Simulador | `PRE` (cenários) e `model()` (fatores fixos) |
| Custo de produção | `CGR`, `INS`, `ABC` |
| GR/IR | `AGE_GR`, `AGE_IR`, `CAUSAS`, `FORN`, `ADV` |
| Fechamento | `TK` (tarefas), `CONTAS`, `FT_D`, `FT_A` |
| Gaveta SAP | `SRC` (origem de cada dado) |

Basta substituir os valores pelos extraídos nas transações indicadas na gaveta de cada dado.

## Publicar no GitHub Pages

1. Crie um repositório e envie o `index.html` e este `README.md`.
2. Em **Settings → Pages**, escolha a branch `main` e a pasta raiz.
3. O painel fica em `https://<seu-usuario>.github.io/<repositorio>/`.

Usa Chart.js, fonte Inter e ícones Tabler via CDN. Não precisa instalar nada.

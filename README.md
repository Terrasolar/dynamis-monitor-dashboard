# Radar de orçamentos · Dynamis + Belenus

Página única, sem build, servida por GitHub Pages em
https://terrasolar.github.io/dynamis-monitor-dashboard/

Compara preço de kit solar entre topologias de inversor (microinversor vs.
string) e entre distribuidores (Dynamis vs. Belenus), por quantidade de módulos.

## De onde vêm os dados

Da tabela `cotacoes_distribuidores` no Supabase (`lkfcdfpoxeallhzmvler`), que as
Edge Functions `dynamis-monitor` e `belenus-monitor` reescrevem toda manhã — o
código delas está no projeto `Pesquisa de Preço`.

A tabela guarda **o estado atual**, uma linha por orçamento (upsert), não série
histórica. Por isso a coluna de tendência da listagem aparece como "sem
histórico": não há com que comparar. Para a tendência funcionar, a coleta teria
que passar a inserir uma linha por verificação em vez de sobrescrever.

O desconto sai da coluna `desconto` de cada linha (Dynamis 8%, ou 9% nos kits de
estrutura 2P; Belenus 0). A regra que adivinhava isso pelo nome do orçamento
ficou só como reserva, para linha sem desconto gravado.

## Login

A página exige login do Supabase. Ela mostra preço de custo de fornecedor, e
até 2026-11-23 lia a tabela com a chave anon, que vai no código da página e é
pública por definição: qualquer pessoa com a URL baixava a tabela inteira. Era o
achado SEG-1 da auditoria do CRM.

O token fica em `sessionStorage` e morre ao fechar a aba — de propósito, para não
deixar o acesso aberto para quem usar a mesma máquina depois. Token vencido
devolve 401 e a página volta ao login dizendo que a sessão expirou.

## Histórico desta página

O layout veio do artifact "Radar de orçamentos · Dynamis + Belenus" do claude.ai,
que era a versão em uso e estava bem à frente do que havia aqui. O artifact lia o
banco do próprio artifact (`claude.use("db")`), que só enche quando alguém copia
os dados à mão — e estava parado desde 2026-11-19. Artifacts não têm capability
de rede, então não havia como ele buscar o Supabase sozinho; a página passou a
viver aqui, onde pode.

# Simulador Fiscal de Triangulação

Validador de **Venda à Ordem** (Convênio SINIEF s/nº de 1970, art. 40) e de **entrega em local diverso**, com consulta cadastral automática de CNPJ.

Ferramenta de apoio operacional para o setor comercial/fiscal: informa o CNPJ do cliente comprador, o local de entrega física e a condição do produto (ICMS-ST) e recebe o **passo a passo de emissão das NF-e** (natureza, CFOP, destaque de ICMS, notas referenciadas, campos `idDest`/`indFinal`/`indIEDest`) mais os **alertas de conformidade** (DIFAL, ST, cadastro inapto, CNAE incompatível, etc.).

## Cenários cobertos

| Cenário | Enquadramento | Notas emitidas |
|---|---|---|
| Entrega no endereço do comprador | Venda direta | 1 NF-e de venda |
| Entrega em filial do comprador (mesma raiz de CNPJ) | Autonomia dos estabelecimentos (LC 87/96, art. 11) | 1 NF-e com grupo `<entrega>` ou faturamento direto à filial |
| Comprador contribuinte **revende** a terceiro/PF | **Venda à ordem** (art. 40, §3º) | 3 NF-e: venda B→C (x.120), remessa A→C (x.923, sem ICMS), remessa simbólica A→B (x.118/x.119, com ICMS) |
| Comprador contribuinte, **uso/consumo/obra** | Entrega em local diverso | 1 NF-e com grupo `<entrega>` |
| Comprador **não contribuinte** | Não cabe venda à ordem | 1 NF-e com grupo `<entrega>` + DIFAL (EC 87/2015) |

## Consulta cadastral

- [BrasilAPI](https://brasilapi.com.br) — razão social, UF/município, CNAE, situação cadastral, Simples Nacional.
- [CNPJ.ws](https://cnpj.ws) — inscrições estaduais (sugere automaticamente *Contribuinte* / *Não contribuinte*).

Ambas são públicas e gratuitas; o CNPJ.ws limita a 3 consultas por minuto no plano público.

## Configuração

Os dados do remetente ficam no início do bloco `<script>` de `index.html`, na constante `EMITENTE`. As alíquotas internas de referência por UF estão em `ALIQ_INTERNA` e devem ser revisadas periodicamente.

## Execução

É um site estático: basta abrir `index.html` no navegador ou servir a pasta com qualquer servidor HTTP. Hospedado no Vercel.

## Aviso

Ferramenta de apoio. Não substitui a análise do setor fiscal/contábil, especialmente para regimes especiais, benefícios fiscais e produtos com tratamento específico.

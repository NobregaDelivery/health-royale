# Health Royale

Arquive seus exames de sangue e de bioimpedância, veja o que melhorou e o que piorou entre um exame e outro, e compare com amigos sem que ninguém veja os valores de ninguém.

**Abrir o app:** https://nobregadelivery.github.io/health-royale/

## Como funciona

- **Adicionar exame:** envie o PDF do laboratório ou a foto do exame. O Claude lê o arquivo (inclusive os "resultados anteriores" impressos no laudo), mostra o que encontrou para você conferir, e só então arquiva.
- **Painel:** o que melhorou, o que piorou e o que está fora da referência, comparando o resultado mais recente de cada marcador com o anterior.
- **Tabela:** todos os resultados já arquivados, um marcador por linha e uma data por coluna. Clique numa linha para ver o gráfico com a faixa de referência.
- **Arena:** cada marcador vira uma nota de 0 a 100 (de 10 em 10) pela distância da faixa de referência. Você gera um código de cartão com essas notas e troca com amigos; a arena mostra a classificação e quem está melhor em cada marcador.

## Privacidade

- **Os exames ficam só no seu navegador** (localStorage). Nada é enviado para este repositório nem para outro servidor.
- **A leitura dos arquivos** usa a sua própria chave da API da Anthropic, guardada só no seu navegador e enviada só para `api.anthropic.com`. Crie uma em [console.anthropic.com](https://console.anthropic.com/settings/keys); cada leitura consome créditos da sua conta.
- **O código de cartão da arena** leva apenas as notas arredondadas por marcador, sem valores, datas ou arquivos. A nota ainda dá uma ideia aproximada de quão longe da referência a pessoa está.
- **Backups:** use "Exportar backup" para levar seus dados para outro aparelho. **Nunca suba o arquivo de backup para este repositório** — o `.gitignore` já bloqueia `health-royale-backup*.json`.

## Aviso

O Health Royale organiza e compara números; ele não faz diagnóstico. "Melhorou" e "piorou" seguem a faixa de referência do próprio laudo. Converse com seu médico antes de mudar qualquer tratamento.

## Estrutura

Um único arquivo, `index.html`, sem build. Usa [pdf.js](https://mozilla.github.io/pdf.js/) (via cdnjs) para extrair o texto dos PDFs e a API Messages da Anthropic para interpretar os resultados.

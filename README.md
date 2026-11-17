# Health Royale

Arquive seus exames de sangue e de bioimpedância, veja o que melhorou e o que piorou entre um exame e outro, e compare com amigos sem que ninguém veja os valores de ninguém.

**Abrir o app:** https://nobregadelivery.github.io/health-royale/

## Como funciona

- **Adicionar exame:** envie o PDF do laboratório ou a foto do exame. O Claude lê o arquivo (inclusive os "resultados anteriores" impressos no laudo), mostra o que encontrou para você conferir, e só então arquiva.
- **Painel:** o que melhorou, o que piorou e o que está fora da referência, comparando o resultado mais recente de cada marcador com o anterior.
- **Tabela:** todos os resultados já arquivados, um marcador por linha e uma data por coluna. Clique numa linha para ver o gráfico com a faixa de referência.
- **Gráficos:** um gráfico para cada marcador com dois ou mais registros, com a faixa de referência, e um comparador de até três marcadores na mesma escala (variação % desde o primeiro registro).
- **Arquivos:** todos os arquivos enviados, os exames que saíram de cada um e uma cópia do original guardada no navegador. O calendário mostra os meses com exame, sem exame e com dados só de histórico, para você saber se falta enviar algum laudo.
- **Arena:** cada marcador vira uma nota de 0 a 100 (de 10 em 10) pela distância da faixa de referência. Você gera um código de cartão com essas notas e troca com amigos; a arena mostra a classificação e quem está melhor em cada marcador.

## Contas e privacidade

- **Login com Google:** só entram os e-mails aprovados pelo administrador (até 4 pessoas). Quem não está na lista vê uma tela de acesso negado.
- **Cada pessoa tem o próprio perfil** no Firebase (Firestore, plano gratuito): exames, configurações e cópias dos arquivos. As regras de segurança (`firestore.rules`) garantem que ninguém lê os dados de outra pessoa, nem o administrador.
- **Arena:** quem quiser participar publica só as notas de 0 a 100 por marcador, nunca os valores. Para comparar com alguém de fora, ainda dá para trocar o código de cartão.
- **Leitura dos exames:** usa a chave da API da Anthropic cadastrada pelo administrador. Quem tem acesso consegue ver essa chave pelas ferramentas do navegador; por isso vale definir um limite de gastos no console da Anthropic.
- **Backups:** "Exportar backup" baixa seus exames em JSON. **Nunca suba o arquivo de backup para este repositório** — o `.gitignore` já bloqueia `health-royale-backup*.json`.
- A configuração do Firebase no `index.html` é pública por natureza; a proteção dos dados está nas regras do Firestore.

## Aviso

O Health Royale organiza e compara números; ele não faz diagnóstico. "Melhorou" e "piorou" seguem a faixa de referência do próprio laudo. Converse com seu médico antes de mudar qualquer tratamento.

## Estrutura

Um único arquivo, `index.html`, sem build. Usa [pdf.js](https://mozilla.github.io/pdf.js/) (via cdnjs) para extrair o texto dos PDFs, a API Messages da Anthropic para interpretar os resultados e o Firebase (Auth + Firestore) para login e perfis.

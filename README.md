# Pesquisa de divulgação IBGE

A paǵina tem como ideia consultar a API pública do calendário de divulgação do IBGE (https://servicodados.ibge.gov.br/api/v3/calendario/).
O usuário precisa escolher a quantidade, a data de inicio e a data de fim. Todos os campos são obrigatórios.

Como o resultado da pesquisa retorna bastante dados, optei por apresentar somente os dados principais, e deixei a opção do usuário baixar a tabela completa em xls. 
Numa aplicação conversaria com o PO para chegar quais dados seriam importantes apresentar e chegar numa melhor decisão de desing para o usuário.

De tecnologias, usei Vue, Vuetify e o Tabulator com a ideia de ficar mais apresentável no prazo da entrega. Essa também seria uma outra decisão a ser tomada, principalmente sobre o uso do vuetify ou css e seus pontos positivos e negativos.

Para rodar:

```
npm install
```
```
npm run dev
```

É possível também acessar o projeto aqui: https://morganaduarte.github.io/search-ibge/

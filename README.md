# Pesquisa de divulgação IBGE

A paǵina tem como ideia consultar a API pública do calendário de divulgação do IBGE (https://servicodados.ibge.gov.br/api/v3/calendario/).
O usuário precisa escolher a quantidade, a data de inicio e a data de fim. Todos os campos são obrigatórios.

Como o resultado da pesquisa retorna bastante dados, achei melhor apresentar somente alguns dados e dar a opção do usuário baixar a tabela completa, se ele desejar. Sobre quais dados mostrar e como mostrar seria uma decisão que tomaria em conjunto com o PO.

Além do Vue, usei o vuetify e o Tabulator com a ideia de ficar mais apresentável no prazo da entrega. Essa também seria uma outra decisão a ser tomada, principalmente sobre o uso do vuetify ou css e seus pontos positivos e negativos.

Para rodar:

```
npm install
```
```
npm run dev
```

É possível também acessar o projeto aqui: https://morganaduarte.github.io/search-ibge/

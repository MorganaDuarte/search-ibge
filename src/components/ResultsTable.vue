<template>
  <div ref="table"></div>
  <v-btn v-if="!!searchResult.items" variant="text" @click="downloadXls">Baixe sua tabela completa aqui!</v-btn>
</template>

<script>
import {TabulatorFull as Tabulator} from 'tabulator-tables';
import 'tabulator-tables/dist/css/tabulator.min.css';
import 'tabulator-tables/dist/css/tabulator_materialize.min.css';

export default {
  props: {
    searchResult: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      tabularIsReady: false
    }
  },
  watch: {
    searchResult: {
      handler() {
        this.tabularIsReady ? this.tabulator.setData(this.searchResult.items) : this.prepareTable();
      }
    }
  },
  methods: {
    prepareTable() {
      const columns = [
        { title: 'Id', field: 'id' },
        { title: 'Título', field: 'titulo', width: "10%", formatter: "textarea" },
        { title: 'Data divulgação', field: 'data_divulgacao', width: "15%", formatter: "textarea" },
        { title: 'Nome produto', field: 'nome_produto', width: "10%", formatter: "textarea" },
        { title: 'Descrição produto', field: 'descricao_produto', formatter: "html", cssClass: 'description-column' },
      ]
      this.tabulator = this.createTable(this.$refs.table, columns);
      this.tabulator.on('tableBuilt', () => this.tabularIsReady = true);
    },
    createTable(html, columns) {
      return new Tabulator(html, {
        layout: "fitDataTable",
        reactiveData: true,
        columns: columns,
        data: this.searchResult.items,
        placeholder: "Não há dados disponiveis",
        paginationSize: 3,
        pagination: true,
      });
    },
    downloadXls() {
      const columns = [
        { title: 'Id', field: 'id' },
        { title: 'Título', field: 'titulo' },
        { title: 'Descricao', field: 'descricao'},
        { title: 'Data divulgação', field: 'data_divulgacao' },
        { title: 'Id do produto', field: 'produto_id' },
        { title: 'Nome produto', field: 'nome_produto' },
        { title: 'Alias', field: 'alias_produto' },
        { title: 'Descrição produto', field: 'descricao_produto' },
        { title: 'Ano ref inicio', field: 'ano_referencia_inicio' },
        { title: 'Mês ref inicio', field: 'mes_referencia_inicio' },
        { title: 'Ano ref fim', field: 'ano_referencia_fim' },
        { title: 'Mês ref fim', field: 'mes_referencia_fim' },
        { title: 'Link', field: 'link' },
        { title: 'Tipo', field: 'tipo' },
        { title: 'Id do tipo', field: 'tipo_id' },
      ]
      const temp = document.createElement('div');
      const tabulatorToDownload = this.createTable(temp, columns)
      setTimeout(() => {
        tabulatorToDownload.download("xlsx", "calendario-de-divulgacao.xlsx", {sheetName: "Aba 1", booktype: "xls"})
      }, 100)
    },
  }
}
</script>

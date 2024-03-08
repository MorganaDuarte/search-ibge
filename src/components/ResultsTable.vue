<template>
  <div ref="table"></div>
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
      columns: [
        { title: 'Id', field: 'id' },
        { title: 'Título', field: 'titulo', width: "20%", formatter: "textarea" },
        { title: 'Data divulgação', field: 'data_divulgacao' },
        { title: 'Id do produto', field: 'produto_id' },
        { title: 'Nome produto', field: 'nome_produto', width: "20%", formatter: "textarea" },
        { title: 'Alias', field: 'alias_produto', width: "15%", formatter: "textarea" },
        { title: 'Descrição produto', field: 'descricao_produto', width: "40%", formatter: "html" },
        { title: 'Ano ref inicio', field: 'ano_referencia_inicio' },
        { title: 'Mês ref inicio', field: 'mes_referencia_inicio' },
        { title: 'Ano ref fim', field: 'ano_referencia_fim' },
        { title: 'Mês ref fim', field: 'mes_referencia_fim' },
        { title: 'Link', field: 'link', width: "15%", formatter:"link", formatterParams: {target:"_blank"} },
        { title: 'Tipo', field: 'tipo', width: "15%", formatter: "textarea" },
        { title: 'Id do tipo', field: 'tipo_id' },
      ],
      totalPages: 0,
      items: [],
      tabularIsReady: false
    }
  },
  watch: {
    searchResult: {
      handler() {
        this.tabularIsReady ? this.tabulator.setData(this.searchResult.items) : this.createTable();
      }
    }
  },
  methods: {
    createTable() {
      this.tabulator = new Tabulator(this.$refs.table, {
        layout: "fitDataStretch",
        reactiveData: true,
        columns: this.columns,
        data: this.searchResult.items,
        placeholder: "Não há dados disponiveis",
        paginationSize: 3,
        pagination: true,
      });

      this.tabulator.on('tableBuilt', () => this.tabularIsReady = true);
    },
  }
}
</script>

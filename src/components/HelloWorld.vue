<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <v-sheet class="mx-auto" width="300">
        <v-form @submit.prevent="result">
          <v-text-field v-model="amount" label="Quantidade"></v-text-field>
          <v-text-field v-model="since" label="Desde de"></v-text-field>
          <v-text-field v-model="until" label="Até"></v-text-field>
          <v-btn class="mt-2" type="submit" block>Pesquisar</v-btn>
        </v-form>
      </v-sheet>
      <v-list lines="one">
        <v-list-item v-for="d in disclosureCalendar" :key="d.count">
          <v-list-item-title>{{ d.items }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-responsive>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      amount: 5,
      since: "2020/01/01",
      until: "2024/03/08",
      disclosureCalendar: []
    }
  },
  computed: {
    result() {
      return this.disclosureCalendar = [{
        "count": 3,
        "page": 1,
        "totalPages": 1,
        "nextPage": 0,
        "previousPage": 0,
        "showingFrom": 1,
        "showingTo": 3,
        "items": [
          {
            "id": 868,
            "titulo": "Prognóstico da Safra (3º Prognóstico)",
            "descricao": "",
            "data_divulgacao": "08/01/2020 11:00:00",
            "tipo_id": 1,
            "tipo": "Divulgação de Indicadores",
            "produto_id": 19068,
            "nome_produto": "Prognóstico da Safra",
            "alias_produto": "prognostico-da-safra",
            "descricao_produto": "",
            "ano_referencia_inicio": 2020,
            "mes_referencia_inicio": 0,
            "ano_referencia_fim": 0,
            "mes_referencia_fim": 0,
            "link": ""
          },
        ]
      }]
    }
  },
  watch: {
    amount(value) {
      console.log(value,'value')
    }
  }
}

</script>

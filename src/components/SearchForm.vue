<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <div class="pb-4">
        <h1>Calendário de Divulgação de Pesquisas do IBGE</h1>
      </div>
      <v-sheet class="mx-auto" width="300">
        <v-form class="pb-6" @submit.prevent="research">
          <v-text-field v-model="amount" label="Quantidade" :rules=[validAmountRules]></v-text-field>
          <v-text-field v-model="since" label="Desde de"></v-text-field>
          <v-text-field v-model="until" label="Até" :rules="[validUntilRules]"></v-text-field>
          <v-btn class="mt-2" :disabled="disabledButton" type="submit" block>Pesquisar</v-btn>
        </v-form>
      </v-sheet>
      <ResultsTable :search-result="searchResult" />
    </v-responsive>
  </v-container>
</template>

<script>
import ResultsTable from "@/components/ResultsTable.vue";

export default {
  components: { ResultsTable },
  data() {
    return {
      amount: 5,
      since: "2020/01/01",
      until: "2024/03/08",
      searchResult: [],
    }
  },
  computed: {
    validAmountRules() {
      if(this.amount >= 1 && this.amount <= 25) return true;

      return "A quantidade deve ser entre 1 e 25";
    },
    validUntilRules() {
      if(this.until > this.since) return true;

      return "A data de 'até' deve ser maior que a data 'de'"
    },
    disabledButton() {
      return this.until < this.since || (this.amount < 1 || this.amount > 25) || !this.since.length;
    }
  },
  methods: {
    async research() {
      const url = `https://servicodados.ibge.gov.br/api/v3/calendario/?qtd=${this.amount}&de=${this.since}&ate=${this.until}`
      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        this.searchResult = await response.json();
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    }
  }
}

</script>

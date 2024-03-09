<template>
  <div class="pb-4">
    <h1>Calendário de Divulgação de Pesquisas do IBGE</h1>
  </div>
  <v-sheet class="mx-auto" width="300">
    <v-form class="pb-6" @submit.prevent="research">
      <v-text-field v-model="amount" label="Quantidade" :rules=[validAmountRules]></v-text-field>
      <v-text-field v-model="startDate" label="Desde de" type="date" :rules=[validStartDateRules]></v-text-field>
      <v-text-field type="date" v-model="endDate" label="Até" :rules="[validEndDateRules]"></v-text-field>
      <v-btn class="mt-2" :disabled="disabledButton" type="submit" block>Pesquisar</v-btn>
    </v-form>
  </v-sheet>
  <ResultsTable :search-result="searchResult" />
</template>

<script>
import ResultsTable from "@/components/ResultsTable.vue";

export default {
  components: { ResultsTable },
  data() {
    return {
      amount: 5,
      startDate: "2020-01-01",
      endDate: "2024-03-08",
      searchResult: [],
    }
  },
  computed: {
    validAmountRules() {
      if(this.amount >= 1 && this.amount <= 25) return true;

      return "A quantidade deve ser entre 1 e 25";
    },
    validStartDateRules() {
      if(!!this.startDate.length) return true;

      return "O campo não pode estar vazio"
    },
    validEndDateRules() {
      if(this.endDate > this.startDate) return true;

      return "A data de 'até' deve ser maior que a data 'de'"
    },
    disabledButton() {
      return this.endDate < this.startDate || (this.amount < 1 || this.amount > 25) || !this.startDate.length;
    }
  },
  methods: {
    async research() {
      const url = `https://servicodados.ibge.gov.br/api/v3/calendario/?qtd=${this.amount}&de=${this.startDate}&ate=${this.endDate}`
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

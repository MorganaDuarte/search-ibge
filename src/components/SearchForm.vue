<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <div class="pb-4">
        <h1>Calendário de Divulgação de Pesquisas do IBGE</h1>
      </div>
      <v-sheet class="mx-auto" width="300">
        <v-form @submit.prevent>
          <v-text-field v-model="amount" label="Quantidade" :rules=[validAmoutRules]></v-text-field>
          <v-text-field v-model="since" label="Desde de" :rules=[validSinceRules]></v-text-field>
          <v-text-field v-model="until" label="Até" :rules="[validUntilRules]"></v-text-field>
          <v-btn class="mt-2" :disabled="disabledButton" type="submit" block>Pesquisar</v-btn>
        </v-form>
      </v-sheet>
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
    }
  },
  computed: {
    validAmoutRules() {
      if(this.amount >= 1 && this.amount <= 25) return true;

      return "A quantidade deve ser entre 1 e 25";
    },
    validSinceRules() {
      if(this.since >= "2020/01/01") return true;

      return "Data limite de 2020/01/01";
    },
    validUntilRules() {
      if(this.until > this.since) return true;

      return "A data de 'até' deve ser maior que a data 'de'"
    },
    disabledButton() {
      return this.until < this.since || (this.amount < 1 || this.amount > 25) || this.since < "2020/01/01";
    }
  }
}

</script>

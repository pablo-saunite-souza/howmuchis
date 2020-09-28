<template>
  <div id="conversor" class="card shadow p-1 m-3 bg-white rounded">
    <div class="card-body">
      <h5 class="card-title">Conversor</h5>
      <form class="d-flex row align-items-center justify-content-center" autocomplete="off"
      v-on:submit.prevent="">
        <div class="form-group m-2">
          <select id="selectCurrency0" class="form-control m-1">
            <option v-for="coin in coins" v-bind:name="coin+'0'" v-bind:key="coin+'0'" >{{coin}}</option>
          </select>
          <input type="number" class="form-control m-1" id="inputCurrency0" v-model="amaut">
        </div>
        <div class="form-group m-2">
          <select id="selectCurrency1" class="form-control m-1">
            <option v-for="coin in coins" v-bind:name="coin+'1'" v-bind:key="coin+'1'" >{{coin}}</option>
          </select>
          <input disabled class="form-control m-1" id="inputCurrency1" v-bind:value="price">
        </div>
        <button class="btn btn-primary btn-block" @click="convert()" type="submit">Convert</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'conversor',
  props: ["coins", "price"],
  data (){
    return {
      amaut: 1
    };
  },
  methods: {
    convert(){
      const options = document.querySelectorAll("option");
      let coinA = "";
      let coinB = "";
      options.forEach( option => {
        if (option.selected){
          if (!coinA){
            coinA = option.label;
          }
          else {
            coinB = option.label;
          }
        }
      });
      this.$emit("convert", {coinA, coinB, amaut: this.amaut});
    }
  }
}
</script>

<style scoped>

#conversor {
  max-width: 500px;
}

.form-control {
  max-width: 200px;
}

</style>

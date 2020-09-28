<template>
  <div id="conversor" class="card shadow p-1 m-3 bg-white rounded">
    <div class="card-body">
      <h5 class="card-title">Conversor</h5>
      <form class="d-flex row align-items-center justify-content-center" autocomplete="off"
      v-on:submit.prevent="">
        <div class="form-group m-2">
          <select id="selectCurrency0" class="form-control m-1">
            <option selected >BRL</option>
          </select>
          <input type="number" class="form-control m-1" id="inputCurrency0" >
        </div>
        <div class="form-group m-2">
          <select id="selectCurrency1" class="form-control m-1">
            <option selected >USD</option>
          </select>
          <input disabled class="form-control m-1" id="inputCurrency1" >
        </div>
        <button class="btn btn-primary btn-block" type="submit">Convert</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'conversor'
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

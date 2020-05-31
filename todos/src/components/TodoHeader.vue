<template>
  <header>

    <h1>ToDo List!</h1>
    <button v-on:click="clickBtn" v-if="!showMessage">About!</button>
    <p ref="pEl"></p>
  </header>
</template>

<script>
export default {
  data() {
    return {
      showMessage : false
    }
  },
  methods: {
    clickBtn: function () {
      this.$refs.pEl.innerText = '처음 만들어 보는 Vue App';
      this.showMessage = !this.showMessage;
    }
  }

}
</script>

<style scoped>
  h1 {
    color: #2F3852;
    font-weight: 900;
    margin: 2.5rem 0 1.5rem;
  }
</style>

<template>
  <div>
    <input type="email" name="email">
    <input type="password" name="password">
    <input type="button" name="BTN_LOGIN" value="LOGIN" @click="goBody()">
  </div>
</template>

<script>
export default {
  methods: {
    goBody() {
      console.log(self)
      this.$router.push('/home')
    }
  }

}
</script>

<style scoped>
  input {
    width : 12em;
    height : 2em;
  }
</style>

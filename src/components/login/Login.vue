<template lang="html">
  <div>
    <LoginHeader></LoginHeader>
    <LoginForm></LoginForm>
    <LoginSNS></LoginSNS>
  </div>
</template>

<script>
import LoginForm from './LoginForm.vue'
import LoginHeader from './LoginHeader.vue'
import LoginSNS from './LoginSNS.vue'

export default {
  components: {
    LoginHeader,
    LoginForm,
    LoginSNS
  }
}
</script>

<style>
</style>

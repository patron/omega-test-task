<template>
  <div>
    <img alt="Omega logo" src="@/assets/logo.svg" class="logo" />
    <LoginPage />
  </div>
</template>

<script>
import LoginPage from "./components/LoginPage.vue";

export default {
  name: "App",
  components: {
    LoginPage
  }
};
</script>

<style>
.logo {
  position: absolute;
  top: 40px;
  left: 40px;
}
</style>

<template>
  <div class="login-container">
    <form class="form-container" v-on:submit.prevent="login">
      <div class="logo">
        <img src="../assets/logo.png" alt="" />
      </div>
      <h1 class="h3 mb-3 fw-normal">Sign in</h1>
      <div class="form-floating">
        <input
          type="text"
          class="form-control"
          id="floatingInput"
          placeholder="Username"
          v-model="usuario"
        />
        <label for="floatingInput">Username</label>
      </div>
      <div class="form-floating mb-4 mt-1">
        <input
          type="password"
          class="form-control"
          id="floatingPassword"
          placeholder="Password"
          v-model="password"
        />
        <label for="floatingPassword">Password</label>
      </div>
      <button class="btn btn-primary w-100 py-2" type="submit">Sign in</button>
      <div v-if="error" class="alert alert-danger mt-2 mb-2" role="alert">
        <i class="bi bi-exclamation-triangle-fill"></i>
        {{ errorMsg }}
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: "",
      password: "",
      error: false,
      errorMsg: "",
    };
  },
  methods: {
    login() {
      if (this.usuario === "rubiolomatias" && this.password === "12345") {
        this.error = false;
        this.errorMsg = "";
        this.$store
          .dispatch("login", {
            usuario: this.usuario,
          })
          .then(() => {
            this.$router.push({ name: "home" });
          })
          .catch((error) => {
            this.error = true;
            this.errorMsg = "Login failed: " + error.message;
          });
      } else {
        this.error = true;
        this.errorMsg = "Los datos ingresados son incorrectos";
      }
    },
  },
};
</script>

<style scoped>
.login-container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.form-container {
  width: 360px;
  padding: 20px;
  border-radius: 5%;
  box-shadow: 1px 1px 3px #ccc;
}
.logo {
  display: flex;
  justify-content: center;
}
.logo img {
  width: 200px;
}
</style>

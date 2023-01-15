<template>
  <div class="container">
    <form>
      <img src="@/assets/vrm_logo.png" alt="VRM logo">
      <label>Username:</label>
      <input type="text" v-model="username" placeholder="username" />
      <label>Password:</label>
      <input type="password" v-model="password" placeholder="**********" />
      <button @click.prevent="login">Login</button>
    </form>
  </div>
</template>

<script>

export default {
  name: 'LoginView',
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    login() {
      if (this.username === 'Bence' && this.password === 'supersecret') {
        localStorage.setItem('isLoggedIn', true);
        localStorage.setItem('loginDate', Date.now());
        this.$router.push({ path: '/' });
      } else {
        alert('Incorrect username or password!');
      }
    },
  },
}
</script>
<style scoped lang="scss">

// Variables
$primary-color: #000000;
$secondary-color: #ffffff;

// Classes
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  padding: 0 10px;
}

form {
  background-color: $primary-color;
  padding: 30px;
  border-radius: 10px;
  flex-direction: column;

  img {
    width: 150px;
  }

  label {
    color: $secondary-color;
    display: block;
    text-align: left;
    margin-bottom: 5px;
    font-size: 14px;
  }

  input {
    display: inline-block;
    width: 100%;
    margin-bottom: 10px;
    padding: 12px;
    border: solid 1px $primary-color;
    border-radius: 4px;
    box-sizing: border-box;
    outline-style: none;
    background-color: $secondary-color;
  }

  button {
    background-color: $secondary-color;
    color: $primary-color;
    background: $secondary-color;
    width: 100%;
    padding: 14px 20px;
    border: none;
    border-radius: 4px;
    font-weight: bold;
    margin-top: 20px;
    cursor: pointer;

    &:hover {
      background-color: darken($secondary-color, 10%);
    }
  }
}

</style>

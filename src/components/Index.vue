<template>
  <div class="index container">
    <div v-if="errorCode == 'auth/wrong-password | auth/invalid-email'" class="error-message">
      <h6>Email ou senha inválido</h6>
    </div>
    <h4>Bem vindo, para mais informações faça o login!</h4>
    <div class="card">
      <form class="card-content" @submit.prevent="login">
        <div class="card-title">
          <i class="medium material-icons teal-text">account_circle</i>
          <h3 class="teal-text">Login</h3>
        </div>
        <ul>
          <li>
            <label for="email">Email</label>
            <input type="email" name="email" v-model="email" required>
          </li>
          <li>
            <label for="password">Password</label>
            <input type="password" name="password" v-model="password" required>
          </li>
        </ul>
        <div>
          <button class="btn-large">Login</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import auth from '@/firebase/init'
export default {
  name: 'Index',
  data () {
    return {
      email:null,
      password: null,
      errorCode: null
    }
  },
  methods: {
    login() {
      auth.signInWithEmailAndPassword(this.email, this.password)
      .then(response => {
          this.$router.push({ name: 'Success' })
        })
      .catch(err => {
        this.errorCode = err.code
      })
    }
  }
}
</script>

<style>
  .index {
    margin: 60px auto;
  }

  .index h4 {
    text-align: center;
  }

  .index .card .card-content .card-title {
    display: flex;
    align-items: center;
  }

  .index .card .card-content .card-title h3 {
    margin: 0px 15px
  }

  .index .card .card-content ul+div {
    display: flex;
    justify-content: flex-end;
  }

  .error-message {
    color: red;
    text-align: center;
  }
</style>

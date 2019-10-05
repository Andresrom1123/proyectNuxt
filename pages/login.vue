<template>
  <div class="container my-5">
    <router-link to="/dashboard">Dashboard</router-link>
    <b-form @submit.prevent="onSubmit">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        >
        </b-form-input>
      </b-form-group>
      <b-form-group id="input-group-1" label="Password:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.password"
          type="password"
          required
        >
        </b-form-input>
      </b-form-group>
      <b-button class="btn-block" type="submit" variant="primary">
        Iniciar sesión
      </b-button>
    </b-form>
  </div>
</template>
<script>
import { mapMutations } from 'vuex'
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      }
    }
  },
  methods: {
    ...mapMutations(['login']),
    onSubmit() {
      this.login(this.form)
      alert('Mandaste la informacion correctamente')
      this.$router.push('/dashboard')
    }
  }
}
</script>

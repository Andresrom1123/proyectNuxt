<template>
  <div class="container my-5">
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
import axios from 'axios'
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
      const endpoint = 'https://newsletters.academlo.com/api/v1/auth/login'
      axios
        .post(endpoint, this.form)
        .then((response) => {
          // Dirigimos la respuesta de la api a la constante user
          const user = response.data
          // Mandamos a llamar el método que mapea la mutación login
          this.login(user)
          // Redireccionamos al dashboard
          this.$router.push('/dashboard')
        })
        .catch((error) => {
          // Si el usuario no existe en la base de datos
          if (error.response.status === 401) {
            alert('no existe el usario en la base de datos')
          } else if (error.response.status === 422) {
            // Si esta enviando mal la informacion
            alert('no estoy enviando bien la informacion')
          } else {
            alert('Tuvimos un error desconcido')
          }
        })
    }
  }
}
</script>

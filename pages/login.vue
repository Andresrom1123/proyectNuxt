<template>
  <div class="shadow my-4 login bg mx-auto p-3 rounded">
    <h3 class="text-center text-white">Log Out</h3>
    <ValidationObserver ref="observer" v-slot="{ passes }">
      <b-form @submit.prevent="passes(onSubmit)">
        <ValidationProvider
          rules="required|email"
          name="email"
          v-slot="{ errors }"
        >
          <b-form-group
            id="input-group-1"
            label="Email address:"
            label-for="input-1"
            class="text-muted"
          >
            <div class="position-relative">
              <b-form-input
                id="input-1"
                v-model="form.email"
                type="email"
                placeholder="Enter email"
                class="col-11 ml-4"
              >
              </b-form-input>
              <i class="ico position-absolute text-white fas fa-envelope"></i>
            </div>
            <small class="form-text text-danger">
              {{ errors[0] }}
            </small>
          </b-form-group>
        </ValidationProvider>
        <ValidationProvider
          rules="required"
          name="password"
          v-slot="{ errors }"
        >
          <b-form-group
            id="input-group-2"
            label="Password:"
            label-for="input-2"
            class="text-muted"
          >
            <div class="position-relative">
              <b-form-input
                id="input-2"
                v-model="form.password"
                type="password"
                class="col-11 ml-4"
              >
              </b-form-input>
              <i class="ico position-absolute text-white fas fa-key"></i>
            </div>
            <small class="form-text text-danger">
              {{ errors[0] }}
            </small>
          </b-form-group>
        </ValidationProvider>
        <b-button class="btn-block text-muted" type="submit" variant="light">
          Log in
        </b-button>
      </b-form>
    </ValidationObserver>
  </div>
</template>
<script>
import axios from 'axios'
import { mapMutations } from 'vuex'
export default {
  layout: 'login',
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      error401: ''
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
<style>
.login {
  width: 40%;
}
.bg {
  background-color: rgba(255, 193, 7, 0.68);
}
.form {
  width: 100%;
}
.ico {
  top: 0.5rem;
}
</style>

<template>
  <div class="container mx-auto mt-3">
    <h4 class="text-muted">
      Add a new <span class="text-warning">newsletter</span>
    </h4>
    <ValidationObserver ref="observer" v-slot="{ passes }">
      <b-form @submit.prevent="passes(onSubmit)">
        <ValidationProvider rules="required" name="tilte" v-slot="{ errors }">
          <b-form-group
            class="text-muted"
            id="input-group-1"
            label="Title:"
            label-for="input-1"
          >
            <b-form-input
              style="width:50%;"
              id="input-1"
              v-model="form.title"
              type="text"
              placeholder=""
            ></b-form-input>
            <small class="text-danger">
              {{ errors[0] }}
            </small>
          </b-form-group>
        </ValidationProvider>
        <ValidationProvider
          rules="required"
          name="textarea"
          v-slot="{ errors }"
        >
          <b-form-textarea
            style="width:50%;"
            id="textarea"
            v-model="form.description"
            placeholder="Description"
            rows="3"
            max-rows="6"
          ></b-form-textarea>
          <small class="text-danger">
            {{ errors[0] }}
          </small>
        </ValidationProvider>
        <ValidationProvider rules="required" name="number" v-slot="{ errors }">
          <b-form-group
            class="mt-2 text-muted"
            id="input-group-1"
            label="Target:"
            label-for="input-2"
          >
            <b-form-input
              style="width:10%;"
              id="input-2"
              v-model="form.target"
              type="number"
              placeholder=""
            ></b-form-input>
            <small class="text-danger">
              {{ errors[0] }}
            </small>
          </b-form-group>
        </ValidationProvider>
        <b-button
          class="btn-block"
          style="width:50%;"
          type="submit"
          variant="success"
        >
          Send
        </b-button>
      </b-form>
    </ValidationObserver>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  layout: 'dashboard',
  middleware: 'authenticated',
  data() {
    return {
      form: {
        title: '',
        description: '',
        target: ''
      }
    }
  },
  methods: {
    onSubmit() {
      const url = 'https://newsletters.academlo.com/api/v1/newsletters'
      axios
        .post(url, this.form)
        .then((response) => {
          // console.log(response.data)
          alert('Se creo un nuevo newsletter')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    }
  }
}
</script>

<template>
  <div>
    <b-modal id="bv-modal-example" hide-footer>
      <template v-slot:modal-title class="">
        <h2 class="m-auto">
          {{ titleName }}
        </h2>
      </template>
      <div class="d-block text-center">
        <div class="">
          <div
            class="border rounded-circle  m-auto"
            style="width:80px; height:80px;"
          >
            <img class="overflow-hidden" src="" alt="" width="100%" />
          </div>
          <div>
            <p>
              {{}}
            </p>
          </div>
          <div class="position-relative">
            <input
              placeholder="Your Email"
              v-model="form.email"
              class="btn-block pl-5 py-2 border rounded"
              type="email"
            />
            <i
              class="position-absolute fas fa-envelope text-warning"
              style="top: 0.8rem; left: 1.5rem; bottom:0;"
            >
            </i>
          </div>
        </div>
      </div>
      <b-button
        class="mt-3 btn-warning"
        block
        @click.prevent="suscribe"
        @click="$bvModal.hide('bv-modal-example')"
      >
        Suscribe
      </b-button>
    </b-modal>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  props: ['image', 'description', 'titleName'],
  data() {
    return {
      form: {
        email: '',
        newsletter_id: 2
      }
    }
  },
  methods: {
    suscribe() {
      const url = 'https://newsletters.academlo.com/api/v1/users'
      axios
        .post(url, this.form)
        .then((response) => {
          console.log(response.data)
          alert('Se registro exitosamente')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    }
  }
}
</script>

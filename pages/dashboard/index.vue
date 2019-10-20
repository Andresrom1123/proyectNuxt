<template>
  <div class="container-fluid my-4">
    <div class="text-right mb-3">
      <nuxt-link to="dashboard/create">
        <button class="btn btn-success text-decoration-none">
          <i class="text-white fas fa-plus"></i>
        </button>
      </nuxt-link>
    </div>
    <b-table bordered striped :items="newsletters" :fields="fields">
      <template v-slot:cell(Options)="data">
        <div class="text-center">
          <b-button
            class="p-0"
            id="show-btn"
            variant="link"
            @click="$bvModal.show('modal-delete' + data.item.id)"
          >
            <span>
              <i class="text-danger fas fa-trash-alt"></i>
            </span>
          </b-button>
          <b-button
            class="p-0"
            variant="link"
            @click="$bvModal.show('modal-edit' + data.item.id)"
          >
            <span>
              <i class="text-info fas fa-edit"></i>
            </span>
          </b-button>
        </div>
      </template>
    </b-table>
    <div>
      <b-modal
        ref="my-modal"
        :id="'modal-delete' + newsletter.id"
        hide-footer
        v-for="newsletter in newsletters"
        :key="newsletter.id"
      >
        <template v-slot:modal-title>
          <p>
            <span class="text-danger">Delete</span>
            {{ newsletter.title }}
          </p>
        </template>
        <div class="d-block text-center">
          <h3>Confirm delete this newsletter</h3>
        </div>
        <div class="d-flex justify-content-center">
          <b-button
            class="mt-2 mr-2"
            variant="outline-danger"
            @click.prevent="delet(newsletter.id)"
            @click="$bvModal.hide('modal-delete' + newsletter.id)"
          >
            Yes
          </b-button>
          <b-button
            class="mt-2"
            variant="outline-success"
            @click="$bvModal.hide('modal-delete' + newsletter.id)"
          >
            No
          </b-button>
        </div>
      </b-modal>
    </div>
    <div>
      <b-modal
        :id="'modal-edit' + newsletter.id"
        v-for="newsletter in newsletters"
        :key="newsletter.id"
      >
        <template v-slot:modal-title>
          <p>
            <span class="text-info">Edit</span>
            {{ newsletter.title }}
          </p>
        </template>
        <form ref="form">
          <b-form-group
            label="Title"
            label-for="title-input"
            invalid-feedback="Name is required"
          >
            <b-form-input
              style="width:80%;"
              id="title-input"
              :value="newsletter.title"
              required
            ></b-form-input>
          </b-form-group>
          <b-form-textarea
            style="width:80%;"
            id="textarea"
            placeholder="Description"
            rows="3"
            max-rows="6"
            :value="newsletter.description"
          ></b-form-textarea>
          <b-form-group
            class="mt-2 text-muted"
            id="input-group-1"
            label="Target:"
            label-for="input-2"
          >
            <b-form-input
              style="width:20%;"
              id="input-2"
              type="number"
              placeholder=""
              :value="newsletter.target"
            ></b-form-input>
          </b-form-group>
        </form>
      </b-modal>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  layout: 'dashboard',
  middleware: 'authenticated',
  data() {
    return {
      // Note `isActive` is left out and will not appear in the rendered table
      urlApi: 'https://newsletters.academlo.com/api/v1',
      fields: [
        'title',
        'description',
        {
          key: 'subscribed',
          sortable: true
        },
        {
          key: 'target',
          sortable: true
        },
        'Options'
      ],
      newsletters: []
    }
  },
  created() {
    this.getTags()
  },
  methods: {
    getTags() {
      const url = this.urlApi + '/newsletters'
      axios
        .get(url)
        .then((response) => {
          this.newsletters = response.data
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    },
    delet(id) {
      const endpoint =
        'https://newsletters.academlo.com/api/v1/newsletters/' + id
      axios
        .delete(endpoint)
        .then(() => {
          alert('Se elemino')
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
      // const del = this.newsletters[index]
      // console.log(del)
    }
  }
}
</script>

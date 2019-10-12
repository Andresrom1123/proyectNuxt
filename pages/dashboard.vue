<template>
  <div class="container-fluid my-4">
    <b-table
      bordered
      striped
      hover
      :items="newsletters"
      :fields="fields"
    ></b-table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      // Note `isActive` is left out and will not appear in the rendered table
      urlApi: 'https://newsletters.academlo.com/api/v1',
      fields: ['title', 'description', 'target', 'subscribed', 'image'],
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
    }
  }
}
</script>

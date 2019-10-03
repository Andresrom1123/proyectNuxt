<template>
  <header class="container-fluid pl-0 pr-0">
    <div class="d-flex m-3">
      <div class="col-6 d-flex justify-content-start">
        <h1 class=" mb-0">
          <nuxt-link class="text-warning text-decoration-none" to="/">
            [ Inside ]
          </nuxt-link>
        </h1>
      </div>
      <div class="col-6 d-flex justify-content-end">
        <p class="text-warning pt-2 px-3"><i class="fas fa-search"></i></p>
        <p class="text-warning pt-2 px-3"><i class="fas fa-user"></i></p>
        <p class="text-warning p-1 border border-warning rounded">
          SPONSORSHIP
        </p>
      </div>
    </div>
    <div>
      <ul class="nav nav-tabs">
        <li v-for="tag in tags" :key="tag.id" class="nav-item">
          <nuxt-link class="nav-link text-muted" :to="'../tags/' + tag.slug">
            {{ tag.name }}
          </nuxt-link>
        </li>
      </ul>
    </div>
  </header>
</template>
<script>
import axios from 'axios'
export default {
  data() {
    return {
      tags: [],
      urlApi: 'https://newsletters.academlo.com/api/v1'
    }
  },
  created() {
    console.log(process.env.apiUrl)
    this.getTags()
  },
  methods: {
    getTags() {
      const url = this.urlApi + '/tags'
      axios
        .get(url)
        .then((response) => {
          this.tags = response.data
          // console.log(this.tags)
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    }
  }
}
</script>

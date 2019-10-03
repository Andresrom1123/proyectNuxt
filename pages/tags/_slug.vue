<template>
  <div>
    <div class="m-auto text-center">
      <h2 class="pt-4">
        Live newsletters
      </h2>
      <p class="text-muted">
        Packed with the trend, news &#38; links you need to be smart, ifrmoed,
        and ahead of the curve
      </p>
    </div>
    <div class="container-fluid my-5">
      <div class="row mx-0">
        <div
          v-for="newsletter in newsletters"
          :key="newsletter.id"
          class="col-lg-3 col-sm-6"
        >
          <inside
            :image="newsletter"
            :description="newsletter"
            :titleTag="newsletter"
          />
        </div>
      </div>
    </div>
    <modal />
  </div>
</template>
<script>
import axios from 'axios'
import Inside from '@/components/Inside.vue'
import Modal from '@/components/Modal.vue'
export default {
  components: {
    Inside,
    Modal
  },
  data() {
    return {
      newsletters: [],
      urlApi: 'https://newsletters.academlo.com/api/v1'
    }
  },
  mounted() {
    this.getTags()
  },
  methods: {
    getTags() {
      const url =
        this.urlApi +
        '/tags/' +
        this.$root.$route.params.slug +
        '?include=newsletters'
      axios
        .get(url)
        .then((response) => {
          this.newsletters = response.data.newsletters
          // console.log(this.newsletters)
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    }
  }
}
</script>

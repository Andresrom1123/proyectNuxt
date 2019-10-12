<template>
  <main class="container-fluid">
    <div>
      <div class="m-auto text-center">
        <h2 class="pt-4">
          Real news, curated by real humans
        </h2>
        <p class="text-muted">
          Packed with the trend, news &#38; links you need to be smart, ifrmoed,
          and ahead of the curve
        </p>
      </div>
      <div class=" my-5">
        <div class="row mx-0">
          <div
            v-for="newsletter in approved"
            :key="newsletter.id"
            class="col-lg-3 col-sm-6"
          >
            <inside :newsletter="newsletter" />
            <modal :newsletter="newsletter" />
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="m-auto text-center">
        <h2 class="pt-4">
          Up-and-coming
        </h2>
        <p class="text-muted">
          If these newsletters reach their goals (or get a
          <span class="text-primary">sponshorship</span>), we'll bring on expert
          writers and launch them. Vote for all your favorites:
        </p>
      </div>
      <div class=" my-5">
        <div class="row mx-0">
          <div
            v-for="newsletter in noApproved"
            :key="newsletter.id"
            class="col-lg-3 col-sm-6"
          >
            <no-inside :newsletter="newsletter" />
            <modal :newsletter="newsletter" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<script>
import axios from 'axios'
import Inside from '@/components/Inside.vue'
import NoInside from '@/components/NoInside.vue'
import Modal from '@/components/Modal.vue'
export default {
  components: {
    Inside,
    NoInside,
    Modal
  },
  data() {
    return {
      approved: [],
      noApproved: [],
      urlApi: 'https://newsletters.academlo.com/api/v1'
    }
  },
  created() {
    // Aqui mandamos a crear el método, traemos los newsletters de la api
    this.getTags()
    // console.log(this.$store.state.counter)
  },
  methods: {
    getTags() {
      // En esta constante almacenamos la url de la api
      const url = this.urlApi + '/newsletters'
      // Usamos axios para traer la api, en este caso, con el metodo get
      axios
        .get(url)
        .then((response) => {
          // Llamamos el metodo para aprovar las newsletter que cumpler con el target
          this.filterApproved(response.data)
          // Llamamos el metodo para aprovar las newsletter que no cumplen con el target
          this.filterNoApproved(response.data)
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    },
    // Aqui estamos haciendo un función, que consiste en filtrar los newsletter que cumplen
    filterApproved(newsletters) {
      this.approved = newsletters.filter(function(newsletter) {
        return newsletter.subscribed >= newsletter.target
      })
    },
    // Aqui estamos haciendo un función, que consiste en filtrar los newsletter que no cumplen
    filterNoApproved(newsletters) {
      this.noApproved = newsletters.filter(function(newsletter) {
        return newsletter.subscribed < newsletter.target
      })
    }
  }
}
</script>

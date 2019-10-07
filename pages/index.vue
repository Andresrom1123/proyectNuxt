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
      modalNewsletter: [],
      urlApi: 'https://newsletters.academlo.com/api/v1'
    }
  },
  created() {
    this.getTags()
    // console.log(this.$store.state.counter)
  },
  methods: {
    getTags() {
      const url = this.urlApi + '/newsletters'
      axios
        .get(url)
        .then((response) => {
          this.filterApproved(response.data)
          this.filterNoApproved(response.data)
          this.modalNewsletter = response.data[0]
          console.log(this.modalNewsletter)
        })
        .catch(() => {
          alert('Tuvimos un error')
        })
    },
    filterApproved(newsletters) {
      this.approved = newsletters.filter(function(newsletter) {
        return newsletter.subscribed >= newsletter.target
      })
    },
    filterNoApproved(newsletters) {
      this.noApproved = newsletters.filter(function(newsletter) {
        return newsletter.subscribed <= newsletter.target
      })
    }
  }
}
</script>

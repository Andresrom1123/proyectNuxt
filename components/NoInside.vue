<template>
  <div>
    <div class="shadow px-2 py-4 mb-5">
      <div class="">
        <div class="d-flex">
          <div
            class="overflow-hidden shadow rounded-circle mx-2 my-3"
            style="width:100%; height:100%;"
          >
            <img class="" :src="newsletter.image" alt="" width="100%" />
          </div>
          <div class="col-8">
            <h4 class="pt-2">
              {{ newsletter.title }}
            </h4>
            <p class="text-muted">
              {{ newsletter.description }}
            </p>
          </div>
        </div>
      </div>
      <div class="position-relative">
        <input
          id="show-btn"
          value="Vote"
          class="btn btn-block btn-light text-muted text-left pl-5 py-2 border rounded"
          type="button"
          @click="$bvModal.show('modal' + newsletter.id)"
        />
        <i
          class="position-absolute fas fa-envelope text-warning"
          style="top: 0.8rem; left: 1.5rem; bottom:0;"
        >
        </i>
        <i
          class="position-absolute text-black-50 fas fa-chevron-right"
          style="top: 0.8rem; right: 1.5rem; bottom:0;"
        >
        </i>
      </div>
      <div class="my-2">
        <b-progress
          :value="newsletter.subscribed"
          :max="newsletter.target"
          variant="warning"
          class="mb-3"
          animated
        ></b-progress>
      </div>
      <div class="d-flex justify-content-between">
        <p class="mb-0 ml-3">
          {{ newsletter.subscribed }}
        </p>
        <p class="mb-0 mr-3">
          {{ newsletter.target }}
        </p>
      </div>
      <div class="d-flex justify-content-between">
        <p class="text-muted mb-0">SUBSCRIBED</p>
        <p class="text-muted mb-0">TARGET</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['newsletter']
}
</script>

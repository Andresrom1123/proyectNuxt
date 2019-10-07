<template>
  <div>
    <div class="shadow px-2 py-4">
      <div class="">
        <div class="d-flex">
          <div
            class="overflow-hidden shadow rounded-circle mx-2 my-3"
            style="width:100%; height:100%;"
          >
            <img class="" :src="newsletter.image" alt="" width="100%" />
          </div>
          <div class="">
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
          @click="$bvModal.show(newsletter.id)"
          value="Vote"
          class="btn btn-block btn-light text-muted text-left pl-5 py-2 border rounded"
          type="button"
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
    </div>
  </div>
</template>
<script>
export default {
  props: ['newsletter']
}
</script>

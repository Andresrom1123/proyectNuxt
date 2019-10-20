<template>
  <div>
    <div class="shadow px-2 py-4 mb-5">
      <div class="">
        <div class="d-flex justify-content-center">
          <div
            class="overflow-hidden shadow rounded-circle "
            style="width:100%; height:100%; margin-left:5rem;"
          >
            <img class="" :src="newsletter.image" alt="" width="100%" />
          </div>
          <div class="ml-4">
            <p
              class="text-warning  rounded p-1 f-1"
              style="background:#ffa50026;"
            >
              DAILY
            </p>
          </div>
        </div>
        <div class="m-auto text-center">
          <h4 class="pt-2">
            {{ newsletter.title }}
          </h4>
          <p class="text-muted">
            {{ newsletter.description }}
          </p>
        </div>
      </div>

      <div class="position-relative">
        <input
          id="show-btn"
          value="Suscribe"
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
    </div>
  </div>
</template>
<script>
export default {
  props: ['newsletter']
}
</script>

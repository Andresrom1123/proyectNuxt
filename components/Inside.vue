<template>
  <div>
    <div class="shadow px-2 py-4">
      <div class="">
        <div class="d-flex justify-content-center">
          <div
            class="overflow-hidden shadow rounded-circle "
            style="margin-left:5rem;"
          >
            <img class="" :src="image.image" alt="" width="100%" />
          </div>
          <div class="ml-4">
            <p class="text-warning  rounded bg-orange-op p-1 f-1">
              TWICE
              <br />
              WEEKLY
            </p>
          </div>
        </div>
        <div class="m-auto text-center">
          <h4 class="pt-2">
            {{ titleTag.title }}
          </h4>
          <p class="text-muted">
            {{ description.description }}
          </p>
        </div>
      </div>

      <div class="position-relative">
        <input
          id="show-btn"
          @click="$bvModal.show('bv-modal-example')"
          value="Suscribe"
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
  props: ['image', 'titleTag', 'description']
}
</script>

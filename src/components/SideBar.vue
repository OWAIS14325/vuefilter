<template>
  <div class="accordion" id="accordionExample">
    <div class="accordion-item" v-for="(filter, index) in filters" :key="index">
      <h2 class="accordion-header" :id="`heading-${index}`">
        <button
          class="accordion-button"
          type="button"
          data-bs-toggle="collapse"
          :data-bs-target="`#collapse-${index}`"
          aria-expanded="true"
          :aria-controls="`collapse-${index}`"
        >
          {{ filter.filter_lable }}
        </button>
      </h2>
      <div
        :id="`collapse-${index}`"
        class="accordion-collapse collapse show"
        :aria-labelledby="`heading-${index}`"
        data-bs-parent="#accordionExample"
      >
        <div class="accordion-body">
          <div class="form-check" v-for="option in filter.options" :key="option.value">
            <input
              class="form-check-input"
              type="checkbox"
              :value="option"
              :id="option.value"
              v-model="filterArray"
            />
            <label class="form-check-label" :for="option.value">
             {{ option.value }}
            </label>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "SideBar",
  props: {
    filters: [],
  },
  emits : ["updateFilters"],
  data(){
    return {
      filterArray : []
    }
  },
  watch : {
    filterArray(val){
      this.$emit("updateFilters", val)
    }
  }
};
</script>


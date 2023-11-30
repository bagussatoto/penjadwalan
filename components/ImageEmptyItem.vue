<template>
  <!-- image empty start -->
  <div class="flex" v-if="condition == 0">
    <img
      src="~/assets/todo-empty-state.png"
      alt="image-todo-empty"
      class="w-1/2 xl:w-1/3 m-auto mt-5"
      data-cy="todo-empty-state"
    />
  </div>
  <!-- image empty end -->
</template>

<script>
export default {
  props: ["condition"],
};
</script>

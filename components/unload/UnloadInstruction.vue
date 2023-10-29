<template>
    <div class="block unloadInstruction">
        <h2 class="text-bold">{{ title }}</h2>
        <p class="text-bold">{{ subtitle }}</p>
        <slot/>
    </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "Заголовок по умолчанию"
    },
    subtitle: {
      type: String,
      default: "Подзаголовок по умолчанию"
    }
  }
};
</script>

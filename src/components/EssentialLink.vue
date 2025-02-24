<template>
  <q-item
    clickable
    tag="a"
    target="_blank"
    :href="props.link"
    class="flex justify-center items-center"
  >
    <q-icon :name="props.icon" size="24px" />
  </q-item>
</template>

<script setup>
const props = defineProps({
  link: {
    type: String,
    default: '#',
  },

  icon: {
    type: String,
    default: '',
  },
})
</script>

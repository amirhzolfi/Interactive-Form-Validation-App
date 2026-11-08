<template>
    <div @click="$emit('update:modelValue' , !this.modelValue)" >{{ modelValue? 'yes' : 'no' }}</div>
</template>

<script>
export default {
  name: 'isAccept',
  props: {
    modelValue: Boolean
  }
}
</script>

<style scoped>
</style>

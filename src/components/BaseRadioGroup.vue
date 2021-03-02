<template>
  <component
    v-for="option in options"
    :key="option.value"
    :is="vertical ? 'div' : 'span'"
    :class="{ horizontal: !vertical }"
  >
    <BaseRadio
      :label="option.label"
      :value="option.value"
      :name="name"
      :modelValue="modelValue"
      @update:modelValue="$emit('update:modelValue', $event)"
    />
  </component>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: [String, Number],
      required: true
    },
    name: {
      type: String,
      required: true
    },
    options: {
      type: Array,
      required: true
    },
    vertical: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.horizontal {
  margin-right: 20px;
}
</style>

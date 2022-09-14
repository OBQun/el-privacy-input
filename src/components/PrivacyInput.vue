<template>
  <el-input
    :value="show ? value : privacyValue"
    @input="$emit('update:value', $event)"
    class="input"
    @focus="show = true"
    @blur="handleBlur"
    v-bind="$attrs"
    v-on="$listeners"
  >
    <div @click="!debounce && (show = !show)" slot="suffix">
      <span v-if="show">👀</span>
      <span v-else>🙈</span>
    </div>
  </el-input>
</template>
<script>
export default {
  name: "privacy-input",
  model: {
    prop: "value",
    event: "update:value",
  },
  props: {
    value: String,
    slice: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      show: true,
      debounce: false,
    };
  },
  methods: {
    handleBlur() {
      this.debounce = true;
      setTimeout(() => {
        this.debounce = false;
      }, 300);
      this.show = false;
    },
  },
  computed: {
    privacyValue() {
      if (!this.slice.length) return this.value;
      return (
        this.value.substring(0, this.slice[0]) +
        this.value
          .substring(this.slice[0], this.slice[1])
          .split("")
          .map(() => "*")
          .join("") +
        (this.slice[1] ? this.value.substring(this.slice[1]) : "")
      );
    },
  },
};
</script>
<style scoped>
</style>
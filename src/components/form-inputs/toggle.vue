<template>
  <div class="v-toggle" @click="$emit('input', !value)">
    <input
      type="checkbox"
      :id="id"
      :disabled="disabled"
      :checked="value"
      @change="$emit('input', !value)" />
    <div class="switch-track" :class="{ active: value }" />
    <div class="switch-thumb" :class="{ active: value }" />
  </div>
</template>

<script>
export default {
  name: "v-toggle",
  props: {
    value: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    id: {
      type: String,
      default: null
    }
  }
};
</script>

<style lang="scss" scoped>
.v-toggle {
  padding: 3px;
  position: relative;
  cursor: pointer;
  width: max-content;
}

input {
  position: absolute;
  opacity: 0;
  left: -99999px;
}

.switch-track {
  &::after {
    content: "";
    display: block;
    height: 14px;
    width: 36px;
    background-color: var(--light-gray);
    border-radius: 100px;
    cursor: pointer;
    transition: var(--fast) var(--transition);
  }

  &.active::after {
    background-color: var(--accent);
    opacity: 0.5;
  }
}

.user-is-tabbing input:focus ~ .switch-track {
  box-shadow: 0 0 0 6px var(--white), 0 0 0 8px var(--accent);
}

.switch-thumb {
  position: absolute;
  top: 0;
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 100px;
  background-color: var(--white);
  box-shadow: 0 3px 1px -2px rgba(0, 0, 0, 0.2), 0 2px 2px 0 rgba(0, 0, 0, 0.14),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
  transition: var(--fast) var(--transition);

  &.active {
    background-color: var(--accent);
    transform: translateX(16px);
  }
}

input:disabled ~ .switch {
  background-color: var(--lightest-gray);

  &::after {
    background-color: var(--lighter-gray);
  }
}
</style>

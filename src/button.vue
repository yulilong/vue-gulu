<template>
    <button class="g-button" :class="{['icon-' + iconPosition]: true}"
      @click="$emit('click')">
      <g-icon class="icon" v-if="icon && !loading" :name="icon"></g-icon>
      <g-icon v-if="loading" class="loading icon" name="loading"></g-icon>
      <div class="content">
        <slot></slot>
      </div>
    </button>
</template>

<script>
export default {
  // props: ['icon', 'iconPosition']
  props: {
    icon: {},
    loading: {
      type: Boolean,
      default: false,
    },
    iconPosition: {
      type: String,         // 属性类型
      default: 'left',      // 属性默认值
      validator (value) {   // 属性检查性
        return value === 'left' || value === 'right'
        // if ( value !== 'left' && value !== 'right') {
        //   return false;
        // } else {
        //   return true;
        // }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.g-button {
  @keyframes spin {
    0% { transform: rotate(0deg)}
    100% { transform: rotate(360deg)}
  }
  height: var(--button-height); padding: 0 .5em; font: inherit;
  border-radius: var(--border-radius); border: 1px solid var(--border-color);
  background: var(--button-bg);
  display: inline-flex; justify-content: center; align-items: center;
  vertical-align: top;
  &:hover { border-color: var(--border-color-hover); }
  &:active { background: var(--button-active-bg); }
  &:focus { outline: none; }
  > .content { order: 2; }
  > .icon { order: 1; margin-right: .3em;}

  &.icon-right {
    > .content { order: 1;}
    > .icon { order: 2; margin-right: 0; margin-left: .3em;}
  }

  .loading {
    animation: spin 2s infinite linear;
  }
}
</style>

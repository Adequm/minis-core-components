<template>
  <div class="modal" v-if="value">
    <div 
      class="modal__background" 
      :style="{ borderRadius: isRoundedBorder ? '10px' : 0 }"
      @click="$emit('input', null)"
    />
    <div class="modal__content">
      <slot/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AppModal',

  props: {
    value: String,
    isRoundedBorder: Boolean,
  },
}
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 100;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 50px;
  box-sizing: border-box;
  &__background {
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 100;
    height: 100%;
    opacity: .5;
    background: var(--special-color);
    cursor: pointer;
    transition: opacity .2s;
    z-index: 1;
    &:hover {
      opacity: .45;
    }
  }
  &__content {
    max-width: 60vw;
    border-radius: 10px;
    padding: 10px;
    background: var(--main-bg-color);
    color: var(--text-color);
    z-index: 2;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
<template>
  <div class="minis__content">
    <iframe 
      :style="{ pointerEvents: isResize ? 'none' : 'all' }"
      :src="link"
      @load="$emit('load', $event)"
    />
  </div>
</template>

<script>
export default {
  name: 'LayoutFrame',

  props: {
    isResize: Boolean,
    link: String,
  },
};
</script>

<style lang="scss" scoped>
.minis__content {
  height: inherit;
  width: inherit;
  background-color: var(--main-bg-color);
  color: var(--text-color);
  font-size: 18px;
  position: relative;
  top: 0;
  z-index: 1;

  > iframe {
    height: inherit;
    width: inherit;
    position: absolute;
    top: 0;
    left: 0;
    border-radius: 10px;
    overflow: hidden;
    border: none;
    outline: none;
    z-index: 1;
  }
}

@media screen and (min-width: 768px) {
  .container:not(.fullscreen) .minis__content {
    border-radius: 10px;
    clip-path: polygon(
      0 5px, 5px 0, calc(100% - 5px) 0, 101% 5px, 
      101% calc(100% - 5px), calc(100% - 5px) 101%, 5px 101%, 0 calc(100% - 5px)
    );
  }
}
</style>
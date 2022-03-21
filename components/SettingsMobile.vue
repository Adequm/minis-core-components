<template>
  <div 
    class="settings" 
    :class="{ isClosedSettings: value }"
    :style="{ marginLeft: `${ title ? 50 : 0 }px` }"
  >
    <div v-if="title" class="title">
      <span
        v-for="(letter, index) of title"
        :key="index"
        v-text="letter"
      />
    </div>

    <div v-if="showArrows" class="arrows">
      <Icon 
        type="angle-double-small-left" 
        :size="60"
        class="arrow-left"
        @click.prevent="$emit('clickToArrow', 'left')"
      />
      <Icon 
        type="angle-double-small-right" 
        :size="60"
        class="arrow-right"
        @click.prevent="$emit('clickToArrow', 'right')"
      />
    </div>

    <Icon 
      :type="themeIcon" 
      :size="30"
      @click.prevent="$emit('switchTheme', 'main')"
    />
    <Icon 
      type="palette" 
      :size="30"
      @click.prevent="$emit('switchTheme', 'special')"
    />
    <Icon 
      type="globe" 
      :size="30"
      @click.prevent="$emit('switchLang')"
    />
    <Icon 
      v-if="isWidthMore768" 
      type="compress-alt" 
      :size="30"
      @click.prevent="$emit('switchFullscreen')"
    />
    <a href="https://adequm.github.io/minis" target="_blank" class="minis">
      <Icon type="home" :size="30"/>
    </a>
  </div>
</template>

<script>
import Icon from './Icon.vue'

export default {
  name: 'SettingsMobile',

  components: { 
    Icon,
  },

  props: {
    themeIcon: String,
    value: Boolean,
    isWidthMore768: Boolean,
    showArrows: Boolean,
    title: String,
  },
};
</script>

<style lang="scss" scoped>
.settings {
  display: grid;
  color: var(--special-color);
  z-index: 1;
  max-width: 60vw;
  align-items: center;
  justify-content: space-evenly;
  position: absolute;
  background: var(--main-bg-color);
  padding: 10px;
  border-radius: 10px;
  margin-bottom: 50px;

  & > .icon {
    cursor: pointer;
    margin: 15px;
    &:hover {
      color: var(--text-color);
    }
  }

  .arrows {
    .arrow-left { right: calc(100% + 80px); }
    .arrow-right { left: calc(100% + 40px); }
    .arrow-left, .arrow-right {
      position: absolute;
      top: 0;
      bottom: -90px;
      margin: auto;
      height: 60px;
      cursor: pointer;
    }
    .icon:hover {
      color: var(--main-bg-color);
    }
  }
  .title {
    position: absolute;
    justify-self: center;
    top: 10px;
    bottom: -80px;
    font-weight: bold;
    color: var(--main-bg-color);
    pointer-events: none;
    writing-mode: vertical-lr;
    right: calc(100% + 10px);
    transform: rotate(180deg);
    font-size: 30px;
    flex-wrap: nowrap;
    justify-content: space-between;
    display: flex;
    text-align: center;
  } 
  .minis {
    background: var(--main-bg-color);
    opacity: 1 !important;
    padding: 15px;
    justify-self: center;
    top: calc(100% + 10px);
    margin: 0 !important;
    height: 80px !important;
    border-radius: 10px;
    &:hover {
      color: var(--text-color);
    }
  }
}
</style>
<template>
  <div class="settings__wrapper" :class="{ isClosedSettings: value }">
    <Icon 
      type="settings" 
      class="settings__switcher"
      @click.prevent="$emit('input', !value)"
      :size="22"
    />

    <div 
      v-if="showHorizontalTop"
      class="settings__wrapper-horizontal" 
      :style="{ width: `${ appWidth }px` }"
    >
      <div class="settings__container dashed">
        <Icon 
          type="plus" 
          side="bottom"
          :text="getHint('plus')"
          :size="22"
          @click.prevent="!value && $emit('plus')"
        />
      </div>
    </div>

    <div 
      v-if="showHorizontalBottom"
      class="settings__wrapper-horizontal settings__wrapper-horizontal_bottom" 
      :style="{ 
        width: `${ appWidth }px`, 
        transform: `translateY(${ appHeight }px)`
      }"
    >
      <div class="settings__container dashed">
        <Icon 
          type="trash" 
          side="top"
          :text="getHint('trash')"
          :size="22"
          @click.prevent="!value && $emit('trash')"
        />
      </div>
    </div>

    <div class="settings__wrapper-vertical">
      <div class="settings__container">
        <Icon 
          :type="themeIcon" 
          :text="getHint('theme')"
          :size="22"
          @click.prevent="!value && $emit('switchTheme', 'main')"
        />
        <Icon 
          type="palette" 
          :text="getHint('color')"
          :size="22"
          @click.prevent="!value && $emit('switchTheme', 'special')"
        />
        <Icon 
          type="globe" 
          :text="getHint('lang')"
          :size="22"
          @click.prevent="!value && $emit('switchLang')"
        />
        <Icon 
          type="expand-arrows-alt" 
          :text="getHint('fullscreen')"
          :size="22"
          @click.prevent="!value && $emit('switchFullscreen')"
        />
      </div>

      <div class="settings__container" :class="{ dashed: !showHints }">
        <Icon 
          type="interrogation" 
          :text="getHint('hints', true)"
          :size="22"
          @click.prevent="!value && $emit('switchHints')"
        />
      </div>

      <div v-if="showVertical" class="settings__container dashed">
        <Icon 
          type="caret-up" 
          :class="{ active: rating == 'up' }" 
          :text="getHint('up')"
          :size="22"
          @click.prevent="!value && $emit('like')"
        />
        <Icon 
          type="headset" 
          :text="getHint('headset')"
          :size="22"
          @click.prevent="!value && $emit('headset')"
        />
        <Icon 
          type="caret-down" 
          :class="{ active: rating == 'down' }" 
          :text="getHint('down')"
          :size="22"
          @click.prevent="!value && $emit('dislike')"
        />
      </div>
    </div>

  </div>
</template>

<script>
import _ from 'lodash';
import Icon from './Icon.vue';

export default {
  name: 'SettingsDesktop',

  components: { 
    Icon,
  },

  props: {
    themeIcon: String,
    appWidth: Number,
    appHeight: Number,
    value: Boolean,
    rating: String,
    showHints: Boolean,
    showVertical: Boolean,
    showHorizontalTop: Boolean,
    showHorizontalBottom: Boolean,
    translate: Function,
    translateDef: Function,
  },

  data: () => ({
    lodash: _,
  }),

  methods: {
    getHint(path, showImportant) {
      if((!this.showHints && !showImportant) || this.value) return;
      const errorMessage = _.invoke(this, 'translate', 'error');
      const hint = _.invoke(this, 'translateDef', `settings[${path}]`);
      return hint !== errorMessage ? hint : null;
    },
  },
};
</script>

<style lang="scss" scoped>
.settings__wrapper {
  position: absolute;
  width: 50px;
  height: 50px;
  margin-left: calc(100% - 15px);
  margin-top: -35px;
  color: var(--special-color);

  .icon {
    cursor: pointer;
  }

  .settings__switcher {
    width: inherit;
    height: inherit;
    display: flex;
    align-items: center;
    justify-items: center;
    &:hover {
      animation: rotate 2s infinite linear;
    }
  }

  &-vertical, &-horizontal {
    position: absolute;
    transition: right .2s, top .2s;
    display: flex;
    gap: 10px;
    .settings__container {
      background: var(--main-bg-color);
      border-radius: 10px;
      display: grid;
      grid-auto-rows: 50px;
      grid-auto-columns: 50px;
      &.rounded {
        border-radius: 25px;
      }
      &.dashed {
        background: transparent;
        margin: 2px;
        outline: 2px dashed var(--main-bg-color);
        .icon:not(.active) {
          color: var(--main-bg-color);
        }
      }
    }
    .icon:hover {
      color: var(--text-color) !important;
    }
  }

  &-vertical {
    top: 35px;
    right: -35px;
    flex-direction: column;
    .settings__container.dashed:not(.rounded) {
      grid-auto-columns: 46px;
      grid-auto-rows: 46px;
    }
  }

  &-horizontal {
    top: -35px;
    right: 35px;
    &_bottom {
      top: 55px;
    }
    flex-direction: row-reverse;
    justify-content: center;
    .settings__container {
      grid-auto-flow: column;
      direction: rtl;
      &.dashed:not(.rounded) {
        grid-auto-rows: 46px;
      }
    }
  }

  &.isClosedSettings {
    .settings__wrapper-vertical { 
      right: 40px;
      top: 36px;
    }
    .settings__wrapper-horizontal { 
      top: 40px;
      &_bottom {
        top: -60px;
      }
    }
  }
}
</style>
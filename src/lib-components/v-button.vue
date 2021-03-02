<template>
  <component
    class="v-button"
    :class="{
      'v-button__secondary': color === 'secondary',
      'v-button__primary': color === 'primary',
      'v-button__outline': outline,
      'v-button--button': isButton
    }"
    :is="componentType"
    v-bind="$attrs"
    @click="handleClick"
  >
    <p>
      <span class="bg"/>
      <span class="base"/>
      <span class="text">
        {{ label }}
      </span>
    </p>
  </component>
</template>

<script lang="ts">
import Vue from 'vue'

enum componentTypes {
  a = 'a',
  button = 'button',
  'router-link' = 'router-link',
  'nuxt-link' = 'nuxt-link',
}

export default /*#__PURE__*/Vue.extend({
  props: {
    label: {
      type: String,
      default: 'Play Valorant'
    },

    type: {
      type: String,
      default: componentTypes.button
    },

    outline: {
      type: Boolean,
      default: false
    },

    color: {
      type: String,
      default: 'secondary'
    }
  },

  computed: {
    componentType () {
      return componentTypes[this.type as keyof typeof componentTypes] || componentTypes.button
    },

    isButton () {
      return this.type === componentTypes.button
    }
  },
  
  methods: {
    handleClick(e: Event) {
      this.$emit("click", e)
    }
  }
})
</script>

<style lang="scss" scoped>
$base: #0f1923;
$white: #ece8e1;
$pink: #ff4655;
$height: 54px;
$transition: 0.3s ease-out all;
$padding: 8px;
$button-padding: 16px;

.v-button {
  cursor: pointer;
  display: flex;
  width: 100%;
  max-width: 240px;
  height: $height;
  padding: $padding;
  font-size: 0.8rem;
  font-weight: 900;
  color: $pink;
  text-align: center;
  text-transform: uppercase;
  text-decoration: none;
  box-shadow: 0 0 0 1px inset rgba($white, 0.3);
  position: relative;
  margin: 10px 0;
  background-color: transparent;
  border: none;

  &--button {
    max-width: 240px + $button-padding;
    height: $height + $button-padding
  }

  &__primary {
    p {
      & span.base {
        border: 1px solid $pink;
      }
    }
  }

  &__secondary {
    p {
      background: $white;
      color: $base;

      & span.base {
        border: 1px solid $white;
      }
    }

    &:hover {
      p {
        color: $white;
      }
    }
  }

  &__outline {
    p {
      background: $base;

      .text {
        color: $white;

      }
    }
  }

  &__primary {
    p {
      background-color: $pink;

      .text {
        color: $white !important;
      }

      .bg {
        background: $white !important;
      }
    }

    &:hover {
      p .text {
        color: $pink !important;

        &:after {
          background: $pink;
        }
      }
    }

    &.v-button__outline {
      p {
        background-color: transparent;

        .text {
          color: $pink !important;
        }

        .bg {
          background: $pink !important;
        }
      }  

      &:hover {
        p .text {
          color: $white !important;
        }

        &:after {
          background: $white !important;
        }
      }
    }
  }

  &:after,
  &:before {
    content: "";
    width: 1px;
    position: absolute;
    height: $padding;
    background: $base;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
  }

  &:before {
    right: 0;
    left: initial;
  }

  & p {
    margin: 0;
    height: $height;
    line-height: $height;
    box-sizing: border-box;
    z-index: 1;
    left: 0;
    width: 100%;
    position: relative;
    overflow: hidden;

    & span.base {
      box-sizing: border-box;
      position: absolute;
      z-index: 2;
      width: 100%;
      height: 100%;
      left: 0;

      &:before {
        content: "";
        width: 4px;
        height: 4px;
        left: -1px;
        top: -1px;
        background: $base;
        position: absolute;
        transition: $transition;
      }
    }

    & span.bg {
      left: -5%;
      position: absolute;
      background: $pink;
      width: 0;
      height: 100%;
      z-index: 3;
      transition: $transition;
      transform: skewX(-10deg);
    }

    & span.text {
      z-index: 4;
      width: 100%;
      height: 100%;
      position: absolute;
      left: 0;
      top: 0;
      &:after {
        content: "";
        width: 4px;
        height: 4px;
        right: 0;
        bottom: 0;
        background: $base;
        position: absolute;
        transition: $transition;
        z-index: 5;
      }
    }
  }

  &:hover {
    color: $white;

    & span.bg {
      width: 110%;
    }

    & span.text:after {
      background: $white;
    }
  }
}
</style>

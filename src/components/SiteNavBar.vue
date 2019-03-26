<template>
  <div class="site-nav-bar text-white">
    <NuxtLink
      class="site-nav-bar__logo"
      :to="{ name: 'index' }"
    >liker.land</NuxtLink>

    <button
      class="site-nav-bar__menu-button"
      @click="toggleSlidingMenu(!getIsSlidingMenuOpen)"
    >
      <span />
      <span />
      <span />
    </button>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';

export default {
  name: 'SiteNavBar',
  computed: {
    ...mapGetters(['getIsSlidingMenuOpen']),
  },
  methods: {
    ...mapActions(['toggleSlidingMenu']),
  },
};
</script>

<style lang="scss">
.site-nav-bar {
  @apply flex;
  @apply items-center;
  @apply justify-between;

  @apply p-16;

  @media screen and (min-width: config('screens.desktop.min')) {
    @apply px-64;
    @apply py-32;

    &:not(:last-child) {
      @apply pb-4;
    }
  }

  &__logo,
  &__menu-button {
    transition-property: transform, opacity;
    transition-duration: 0.2s;
    transition-timing-function: ease;

    &:hover {
      opacity: 0.6;
    }
    &:active {
      transform: scale(0.9);

      opacity: 0.3;
    }
  }

  &__logo {
    @apply text-inherit-color;
    @apply font-600;
  }

  &__menu-button {
    @apply block;
    @apply relative;

    @apply text-inherit-color;

    @apply flex;
    @apply items-center;
    @apply justify-center;

    @apply w-32;
    @apply h-32;

    > span {
      width: calc(100% - 0.5em);

      background: currentColor;

      transition-duration: 0.25s;
      transition-timing-function: ease-in-out;

      @apply absolute;

      @apply h-2;

      &:nth-child(1),
      &:nth-child(3) {
        transition-property: transform;
        will-change: transform;
      }

      &:nth-child(1) {
        transform: translateY(0.5em);
      }

      &:nth-child(2) {
        transition-property: opacity;
      }

      &:nth-child(3) {
        transform: translateY(-0.5em);
      }

      // Turn the hamburger into cross
      html[sliding-menu='opened'] & {
        &:nth-child(1) {
          transform: rotateZ(45deg);
        }

        &:nth-child(2) {
          opacity: 0;
        }

        &:nth-child(3) {
          transform: rotateZ(-45deg);
        }
      }
    }
  }
}
</style>
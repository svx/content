<template>
  <div
    v-if="toc.length"
    class="w-full lg:w-1/4 py-4 lg:py-8"
    :class="{
      'lg:pl-8 lg:pr-0': settings.layout !== 'single',
      'lg:px-8': settings.layout === 'single'
    }"
  >
    <div class="lg:sticky lg:top-0 lg:pt-24 lg:-mt-24">
      <h3
        class="mb-3 lg:mb-2 text-gray-500 uppercase tracking-wider font-bold text-sm lg:text-xs"
      >{{ $t('toc.title') }}</h3>
      <nav>
        <scrollactive highlight-first-item active-class="text-primary-500" :offset="0" tag="ul">
          <li
            v-for="link of toc"
            :key="link.id"
            class="text-gray-700 dark:text-gray-300"
            :class="{
              'border-t border-dashed dark:border-gray-800 first:border-t-0': link.depth === 2
            }"
          >
            <a
              :href="`#${link.id}`"
              class="block text-sm scrollactive-item transition-transform ease-in-out duration-300 transform hover:translate-x-1"
              :class="{
                'py-2': link.depth === 2,
                'ml-2 pb-2': link.depth === 3
              }"
            >{{ link.text }}</a>
          </li>
        </scrollactive>
      </nav>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  props: {
    toc: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    ...mapGetters([
      'settings'
    ])
  }
}
</script>

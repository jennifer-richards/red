<template>
  <form method="get" :action="SEARCH_PATH" class="w-full flex pt-4 pb-6">
    <input
      id="search"
      v-model="searchStore.q"
      type="search"
      name="q"
      class="flex-1 bg-white text-black dark:bg-black dark:text-white dark:border-white dark:border pl-4 py-3"
      :placeholder="
        responsiveModeStore.responsiveMode === 'Desktop' ?
          `Find an RFC (e.g. ‘${formatTitlePlaintext('RFC7120')}’)`
        : 'Find an RFC'
      "
      :aria-label="`Find an RFC (e.g. ‘${formatTitlePlaintext('RFC7120')}’)`"
    />
    <button
      type="submit"
      name="search"
      class="bg-blue-200 px-2 flex items-center"
    >
      <Icon name="fluent:search-12-filled" size="2em" />
    </button>
  </form>
</template>

<script setup lang="ts">
import { useSearchStore } from '~/stores/search'
import { formatTitlePlaintext } from '~/utilities/rfc'
import { SEARCH_PATH } from '~/utilities/url'

const searchStore = useSearchStore()
const responsiveModeStore = useResponsiveModeStore()
</script>

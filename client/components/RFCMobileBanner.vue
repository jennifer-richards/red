<template>
  <div
    :class="[
      'flex flex-row w-full justify-between items-center py-1 bg-[#002D3CE5] text-white dark:bg-black dark:border',
      props.isFixed && 'fixed bottom-0 left-0 right-0 lg:hidden print:hidden'
    ]"
  >
    <div
      :class="[
        'xs:leading-5 sm:leading-6',
        props.isFixed && 'container mx-auto p-2',
        !props.isFixed && 'p-2'
      ]"
    >
      <div class="font-bold">{{ idParts.type }} {{ idParts.number }}</div>
      <div v-if="idParts.type === RFC_TYPE_RFC">Internet Standard</div>
      <div class="text-red-400">
        Obsoleted by
        <ul>
          <li
            v-for="(obsoletedByItem, obsoletedByItemIndex) in props.rfc
              .obsoleted_by"
            :key="obsoletedByItemIndex"
          >
            <A :href="infoRfcPathBuilder(`RFC${obsoletedByItem.id}`)">
              <component :is="formatTitle(`RFC${obsoletedByItem.id}`)" />
              {{ obsoletedByItem.title }}
            </A>
          </li>
        </ul>
      </div>
    </div>
    <slot />
  </div>
</template>

<script setup lang="ts">
import type { Rfc } from '~/generated/red-client'
import { formatTitle, RFC_TYPE_RFC, parseRFCId } from '~/utilities/rfc'
import { infoRfcPathBuilder } from '~/utilities/url'

type Props = {
  rfc: Rfc
  isFixed: boolean
}

const props = defineProps<Props>()

const idParts = parseRFCId(`RFC${props.rfc.number}`)
</script>

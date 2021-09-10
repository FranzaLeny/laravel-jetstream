<template>
  <div v-if="data.links.length > 3">
    <div class="flex flex-wrap -mb-1">
      <div
        v-if="data.current_page === 1"
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 text-gray-400 border rounded"
        v-html="1"
      />
      <Link
        v-if="data.current_page !== 1"
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border-blue-200 border rounded-full hover:bg-white focus:border-indigo-500 focus:text-indigo-500"
        :href="data.first_page_url"
        preserve-state
      >1</Link>
      <div
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border-blue-200"
        v-if="data.current_page-1 > 3"
      >...</div>
      <template
        v-for="(link, key) in data.links"
        :key="key"
      >
        <template v-if="key > data.current_page-3">
          <template v-if="key>1">
            <template v-if="key < data.current_page+3">
              <Link
                v-if="key < data.last_page"
                class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border-blue-200 border rounded-full hover:bg-white focus:border-indigo-500 focus:text-indigo-500"
                :class="{ 'ring ring-blue-100 bg-blue-200': link.active }"
                :href="link.url"
                v-html="link.label"
                preserve-state
              />
            </template>
          </template>
        </template>
      </template>
      <div
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border-blue-200"
        v-if="data.last_page-data.current_page > 3"
      >...</div>
      <div
        v-if="data.current_page === data.last_page"
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 text-gray-400 border rounded"
        v-html="data.last_page"
      />
      <Link
        v-if="data.current_page !== data.last_page"
        class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border-blue-200 border rounded-full hover:bg-white focus:border-indigo-500 focus:text-indigo-500"
        :href="data.last_page_url"
        preserve-state
        v-html="data.last_page"
      />
    </div>
  </div>
</template>

<script>
import { Link } from "@inertiajs/inertia-vue3";

export default {
  components: {
    Link,
  },
  props: {
    data: Object,
  },
};
</script>

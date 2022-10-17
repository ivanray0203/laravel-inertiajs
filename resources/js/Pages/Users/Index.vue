<template>
  <div>
    <Head title="User"/>
    <div class="flex justify-between mb-6">
      <div class="flex item-center">
        <h1 class="text-3xl font-bold">Users</h1>
        <Link v-if="can.createUser" href="/users/create" class="text-blue-500 text-sm ml-2">New User</Link>
      </div>
      <input
        v-model="search"
        type="text"
        placeholder="Search..."
        class="border px-2 rounded-lg"
      />
    </div>

    <div class="mt-4">
      <div class="overflow-x-auto relative">
        <table class="w-full text-sm text-left text-gray-500">
          <tbody>
            <tr
              v-for="user in users.data"
              :key="user.name"
              class="bg-white border-b"
            >
              <th
                scope="row"
                class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap"
              >
                {{ user.name }}
              </th>
              <td class="py-4 px-6">
                <a href="#" class="text-md text-blue-500 font-bold">Edit</a>
              </td>
            </tr>
          </tbody>
        </table>

        <div>
          <div class="mt-6">
            <Link
              v-for="link in users.links"
              :key="link.url"
              :href="link.url"
              v-html="link.label"
              :class="{ 'text-gray-500': !link.url, 'font-bold': link.active }"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import { Inertia } from '@inertiajs/inertia'
import throttle from 'lodash/throttle'
import { Head } from '@inertiajs/inertia-vue3'

let props = defineProps({
  users: Object,
  filters: Object,
  can: Object
});

let search = ref(props.filters.search);
// watch(search, throttle( function(value) {
//     Inertia.get('/users', { search: value }, {
//         preserveState: true,
//         replace: true
//     }))
// })

watch(search, throttle(function (value) {
  Inertia.get('/users', {search: value}, {
    preserveState: true,
    replace: true
  })
}, 500))
</script>

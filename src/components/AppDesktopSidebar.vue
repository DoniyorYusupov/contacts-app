<script setup lang="ts">
import { useRoute } from 'vue-router'
import type { NavigationItem } from '../types'

interface Props {
  navigation: NavigationItem[]
}
defineProps<Props>()

const route = useRoute()
const isActive = (link: string) => route.path.includes(link)
</script>

<template>
  <div class="lg:fixed lg:inset-y-0 lg:z-50 lg:w-72 lg:flex-col">
    <!-- Sidebar component, swap this element with another sidebar if you like -->
    <div class="flex grow flex-col gap-y-5 overflow-y-auto border-r border-gray-200 bg-white px-6">
      <div class="flex h-16 shrink-0 items-center">
        <img class="h-8 w-auto" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=600" alt="Your Company">
      </div>
      <nav class="flex flex-1 flex-col">
        <ul role="list" class="flex flex-1 flex-col gap-y-7">
          <li>
            <ul role="list" class="-mx-2 space-y-1">
              <li v-for="item in navigation" :key="item.name">
                <router-link :to="item.link" class="group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold" :class="[isActive(item.link) ? 'bg-gray-50 text-indigo-600' : 'text-gray-700 hover:text-indigo-600 hover:bg-gray-50']">
                  <component :is="item.icon" class="h-6 w-6 shrink-0" :class="[isActive(item.link) ? 'text-indigo-600' : 'text-gray-400 group-hover:text-indigo-600']" aria-hidden="true" />
                  {{ item.name }}
                </router-link>
              </li>
            </ul>
          </li>
          <li class="-mx-6 mt-auto">
            <a href="#" class="flex items-center gap-x-4 px-6 py-3 text-sm font-semibold leading-6 text-gray-900 hover:bg-gray-50">
              <img class="h-8 w-8 rounded-full bg-gray-50" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
              <span class="sr-only">Your profile</span>
              <span aria-hidden="true">Tom Cook</span>
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

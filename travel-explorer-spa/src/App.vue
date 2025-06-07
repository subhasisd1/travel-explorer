<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Navigation Bar -->
    <nav class="bg-white shadow p-4 flex justify-between items-center sticky top-0 z-50">
      <router-link to="/" class="flex items-center space-x-2 text-blue-600 hover:text-blue-800">
        <GlobeAltIcon class="w-6 h-6" />
        <h1 class="text-2xl font-bold">Travel Explorer</h1>
      </router-link>

      <div class="space-x-4 flex items-center">
        <router-link to="/" class="flex items-center space-x-1 text-gray-700 hover:text-blue-600">
          <HomeIcon class="w-5 h-5" />
          <span>Home</span>
        </router-link>
        <router-link to="/packages" class="flex items-center space-x-1 text-gray-700 hover:text-blue-600">
          <BriefcaseIcon class="w-5 h-5" />
          <span>Tour Packages</span>
        </router-link>
        <router-link to="/about" class="flex items-center space-x-1 text-gray-700 hover:text-blue-600">
          <InformationCircleIcon class="w-5 h-5" />
          <span>About</span>
        </router-link>
      </div>
    </nav>

    <!-- Routed Views -->
    <main class="p-6">
      <router-view />
    </main>
  </div>
</template>

<script setup>
import { GlobeAltIcon, HomeIcon, BriefcaseIcon, InformationCircleIcon } from '@heroicons/vue/24/outline';
</script>

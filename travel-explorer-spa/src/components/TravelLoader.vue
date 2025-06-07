<template>
  <div class="relative h-10 w-full bg-gradient-to-r from-blue-50 to-sky-100 rounded-lg overflow-hidden border border-blue-200">
    <!-- Flipped to face right with scaleX(-1) -->
    <div class="animate-drive text-3xl absolute left-0 top-1 transform scaleX(-1)"> ✈️</div>
    <p class="absolute bottom-2 w-full text-center text-sm text-blue-600">
      Preboarding your dream trip...
    </p>
  </div>
</template>

<style scoped>
.animate-drive {
  animation: drive 3s linear infinite;
}
@keyframes drive {
  0% { transform: translateX(-50px) scaleX(1); } /* Start left, face right */
  100% { transform: translateX(calc(100vw + 50px)) scaleX(1); } /* Move right, keep facing right */
}
</style>
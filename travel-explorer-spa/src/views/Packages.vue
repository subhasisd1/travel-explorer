// Packages.vue
<template>
  <div class="p-6">
    <button @click="openFormForAdd" class="bg-green-600 text-white px-4 py-2 rounded mb-4">
      Add New Package
    </button>

    <!-- Notification -->
    <transition name="fade-slide">
      <div v-if="showNotification" :class="[
        'fixed top-20 right-5 text-white py-2 px-4 rounded shadow-lg',
        notificationType === 'success' ? 'bg-green-500' : 'bg-red-600'
      ]">
        {{ notificationMessage }}
      </div>
    </transition>

    <!-- Modal Form for Add/Edit -->
    <PackageForm :visible="showForm" :editData="editData" @close="closeForm" @refresh="fetchPackages"
      @notify="handleNotification" />

    <div class="flex items-center gap-4 mb-2">
      <h2 class="text-xl font-semibold whitespace-nowrap">Tour Packages</h2>
        <TravelLoader :class="{ 'opacity-0 pointer-events-none': !loading }" />
    </div>

    <!-- Package List Display -->
    <PackageList :packages="packages" @refresh="fetchPackages" @edit="handleEdit" ref="packageListRef" />


  </div>
</template>

<script>
import PackageForm from '@/components/PackageForm.vue';
import PackageList from '@/components/PackageList.vue';
import TravelLoader from '@/components/TravelLoader.vue';
import axios from 'axios';

export default {
  components: { PackageList, PackageForm, TravelLoader },
  name: "PackagesView",
  data() {
    return {
      packages: [],
      showForm: false,
      editData: null,
      showNotification: false,
      notificationMessage: '',
      notificationType: 'success',
      loading: true
    };
  },
  methods: {
    async fetchPackages() {
      const res = await axios.get('http://localhost:3000/api/packages');
      this.packages = res.data;
    },
    handleEdit(pkg) {
      this.editData = pkg;
      this.showForm = true;
    },
    openFormForAdd() {
      this.editData = null;
      this.showForm = true;
    },
    closeForm() {
      this.showForm = false;
      this.editData = null;
    },
    handleNotification(payload) {
      this.$refs.packageListRef?.showTemplateNotification(payload.message, payload.type);
    }
  },
  async mounted() {
    this.loading = true
    try {
      await this.fetchPackages() // or whatever fetch method you're using
    } finally {
      setTimeout(() => {
        this.loading = false // Simulate loading time, replace with actual data fetch logic
      }, 1000)
    }
  }
};
</script>

<style>
@keyframes fade-in-up {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in-up {
  animation: fade-in-up 0.4s ease-out;
}
</style>

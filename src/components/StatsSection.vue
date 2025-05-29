<template>
  <section class="py-20 bg-gray-50">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid md:grid-cols-4 gap-8">
        <div v-for="stat in stats" :key="stat.label" class="text-center">
          <div class="text-4xl font-bold text-blue-600 mb-2">{{ stat.value }}</div>
          <div class="text-gray-600">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const stats = [
  { value: '50K+', label: 'Gia đình tin tưởng' },
  { value: '99.9%', label: 'Thời gian hoạt động' },
  { value: '2s', label: 'Thời gian phản hồi' },
  { value: '24/7', label: 'Hỗ trợ khách hàng' }
]
</script>
<template>
  <header class="bg-white shadow-lg sticky top-0 z-50">
    <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16">
        <div class="flex items-center space-x-3">
          <div class="bg-gradient-to-r from-blue-600 to-indigo-600 p-2 rounded-lg">
            <Wallet class="h-8 w-8 text-white" />
          </div>
          <span class="text-xl font-bold text-gray-900">SmartWallet</span>
        </div>
        
        <div class="hidden md:flex items-center space-x-8">
          <a href="#features" class="text-gray-700 hover:text-blue-600 transition-colors">Tính năng</a>
          <a href="#security" class="text-gray-700 hover:text-blue-600 transition-colors">Bảo mật</a>
          <a href="#pricing" class="text-gray-700 hover:text-blue-600 transition-colors">Giá cả</a>
          <a href="#contact" class="text-gray-700 hover:text-blue-600 transition-colors">Liên hệ</a>
        </div>
        
        <div class="flex items-center space-x-4">
          <button class="text-gray-700 hover:text-blue-600 transition-colors">Đăng nhập</button>
          <button class="bg-gradient-to-r from-blue-600 to-indigo-600 text-white px-6 py-2 rounded-lg hover:from-blue-700 hover:to-indigo-700 transition-all">
            Dùng thử miễn phí
          </button>
        </div>
        
        <!-- Mobile menu button -->
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden">
          <Menu class="h-6 w-6" />
        </button>
      </div>
      
      <!-- Mobile menu -->
      <div v-if="mobileMenuOpen" class="md:hidden py-4 border-t">
        <div class="flex flex-col space-y-4">
          <a href="#features" class="text-gray-700">Tính năng</a>
          <a href="#security" class="text-gray-700">Bảo mật</a>
          <a href="#pricing" class="text-gray-700">Giá cả</a>
          <a href="#contact" class="text-gray-700">Liên hệ</a>
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import { Wallet, Menu } from 'lucide-vue-next'

const mobileMenuOpen = ref(false)
</script>
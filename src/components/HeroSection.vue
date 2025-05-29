<template>
  <section class="relative py-20 overflow-hidden">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <div class="space-y-8">
          <div class="space-y-4">
            <h1 class="text-4xl lg:text-6xl font-bold text-gray-900 leading-tight">
              Ví Điện Tử 
              <span class="bg-gradient-to-r from-blue-600 to-indigo-600 bg-clip-text text-transparent">
                Gia Đình Thông Minh
              </span>
            </h1>
            <p class="text-xl text-gray-600 leading-relaxed">
              Quản lý tài chính gia đình một cách thông minh với xác thực CCCD, 
              tài khoản đồng sở hữu và kiểm soát chi tiêu cho con em.
            </p>
          </div>
          
          <div class="flex flex-col sm:flex-row gap-4">
            <button class="bg-gradient-to-r from-blue-600 to-indigo-600 text-white px-8 py-4 rounded-lg text-lg font-semibold hover:from-blue-700 hover:to-indigo-700 transition-all transform hover:scale-105">
              Tải ứng dụng ngay
            </button>
            <button class="border-2 border-gray-300 text-gray-700 px-8 py-4 rounded-lg text-lg font-semibold hover:border-blue-600 hover:text-blue-600 transition-all">
              Xem demo
            </button>
          </div>
          
          <div class="flex items-center space-x-8 text-sm text-gray-500">
            <div class="flex items-center space-x-2">
              <Shield class="h-5 w-5 text-green-500" />
              <span>Bảo mật AES-256</span>
            </div>
            <div class="flex items-center space-x-2">
              <Users class="h-5 w-5 text-blue-500" />
              <span>Quản lý đa tài khoản</span>
            </div>
          </div>
        </div>
        
        <div class="relative">
          <div class="bg-white rounded-2xl shadow-2xl p-8 transform rotate-3 hover:rotate-0 transition-transform duration-500">
            <div class="space-y-6">
              <div class="flex items-center justify-between">
                <h3 class="text-lg font-semibold">Tổng quan gia đình</h3>
                <div class="bg-green-100 text-green-800 px-3 py-1 rounded-full text-sm">
                  Hoạt động
                </div>
              </div>
              
              <div class="grid grid-cols-2 gap-4">
                <div class="bg-blue-50 p-4 rounded-lg">
                  <div class="text-2xl font-bold text-blue-600">2.5M</div>
                  <div class="text-sm text-gray-600">Số dư tổng</div>
                </div>
                <div class="bg-green-50 p-4 rounded-lg">
                  <div class="text-2xl font-bold text-green-600">+15%</div>
                  <div class="text-sm text-gray-600">Tiết kiệm tháng</div>
                </div>
              </div>
              
              <div class="space-y-3">
                <div class="flex items-center justify-between">
                  <span class="text-sm">Tài khoản chính</span>
                  <span class="font-semibold">1.8M VND</span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-sm">Tài khoản con</span>
                  <span class="font-semibold">500K VND</span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-sm">Tiết kiệm</span>
                  <span class="font-semibold">200K VND</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { Shield, Users } from 'lucide-vue-next'
</script>
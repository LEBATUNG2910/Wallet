<template>
  <div class="space-y-6">
    <!-- Overview Cards -->
    <div class="grid grid-cols-3 gap-4">
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-red-600">12.5M</p>
        <p class="text-sm text-gray-600">Chi tiêu tháng</p>
        <div class="flex items-center justify-center mt-1">
          <TrendingUp class="h-3 w-3 text-red-500 mr-1" />
          <span class="text-xs text-red-500">+8%</span>
        </div>
      </div>
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-green-600">15M</p>
        <p class="text-sm text-gray-600">Thu nhập tháng</p>
        <div class="flex items-center justify-center mt-1">
          <TrendingUp class="h-3 w-3 text-green-500 mr-1" />
          <span class="text-xs text-green-500">+5%</span>
        </div>
      </div>
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-blue-600">2.5M</p>
        <p class="text-sm text-gray-600">Tiết kiệm tháng</p>
        <div class="flex items-center justify-center mt-1">
          <TrendingDown class="h-3 w-3 text-red-500 mr-1" />
          <span class="text-xs text-red-500">-3%</span>
        </div>
      </div>
    </div>

    <!-- Spending by Category -->
    <div class="border rounded-lg p-6">
      <div class="flex justify-between items-center mb-4">
        <h4 class="font-semibold flex items-center">
          <BarChart3 class="h-5 w-5 mr-2" />
          Chi tiêu theo danh mục
        </h4>
        <button class="border border-gray-300 px-3 py-1 rounded text-sm flex items-center hover:bg-gray-50">
          <Download class="h-4 w-4 mr-1" />
          Xuất báo cáo
        </button>
      </div>
      <div class="space-y-4">
        <div v-for="(category, index) in categories" :key="index" class="space-y-2">
          <div class="flex justify-between items-center">
            <span class="text-sm font-medium">{{ category.name }}</span>
            <div class="text-right">
              <span class="font-semibold">{{ category.amount.toLocaleString() }} VND</span>
              <span class="text-sm text-gray-500 ml-2">({{ category.percentage }}%)</span>
            </div>
          </div>
          <div class="w-full bg-gray-200 rounded-full h-2">
            <div 
              :class="category.color"
              class="h-2 rounded-full transition-all duration-500"
              :style="{ width: `${category.percentage}%` }"
            ></div>
          </div>
        </div>
      </div>
    </div>

    <!-- Transaction History -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Lịch sử giao dịch gần đây</h4>
      <div class="space-y-3">
        <div v-for="transaction in transactions" :key="transaction.id" 
             class="flex items-center justify-between p-3 border rounded-lg">
          <div class="flex-1">
            <p class="font-medium">{{ transaction.description }}</p>
            <div class="flex items-center space-x-2 mt-1">
              <div class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs font-medium">
                {{ transaction.category }}
              </div>
              <span class="text-xs text-gray-500">{{ transaction.account }}</span>
            </div>
          </div>
          <div class="text-right">
            <p :class="[
              'font-semibold',
              transaction.amount > 0 ? 'text-green-600' : 'text-red-600'
            ]">
              {{ transaction.amount > 0 ? '+' : '' }}{{ transaction.amount.toLocaleString() }} VND
            </p>
            <p class="text-xs text-gray-500 flex items-center">
              <Calendar class="h-3 w-3 mr-1" />
              {{ transaction.date }}
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- Family Spending Summary -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Tổng quan chi tiêu gia đình</h4>
      <div class="grid grid-cols-2 gap-4">
        <div class="space-y-3">
          <h5 class="font-medium">Theo tài khoản</h5>
          <div class="space-y-2">
            <div class="flex justify-between items-center p-2 bg-blue-50 rounded">
              <span class="text-sm">Tài khoản chính</span>
              <span class="font-semibold">8.2M VND</span>
            </div>
            <div class="flex justify-between items-center p-2 bg-green-50 rounded">
              <span class="text-sm">Tài khoản đồng sở hữu</span>
              <span class="font-semibold">2.5M VND</span>
            </div>
            <div class="flex justify-between items-center p-2 bg-purple-50 rounded">
              <span class="text-sm">Tài khoản con</span>
              <span class="font-semibold">1.8M VND</span>
            </div>
          </div>
        </div>

        <div class="space-y-3">
          <h5 class="font-medium">Xu hướng</h5>
          <div class="space-y-2">
            <div class="flex items-center space-x-2 text-sm">
              <TrendingUp class="h-4 w-4 text-red-500" />
              <span>Chi tiêu ăn uống tăng 15%</span>
            </div>
            <div class="flex items-center space-x-2 text-sm">
              <TrendingDown class="h-4 w-4 text-green-500" />
              <span>Chi tiêu giải trí giảm 20%</span>
            </div>
            <div class="flex items-center space-x-2 text-sm">
              <TrendingUp class="h-4 w-4 text-blue-500" />
              <span>Tiết kiệm ổn định</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { BarChart3, TrendingUp, TrendingDown, Download, Calendar } from 'lucide-vue-next'

const categories = ref([
  { name: "Ăn uống", amount: 4500000, percentage: 36, color: "bg-red-500" },
  { name: "Mua sắm", amount: 3200000, percentage: 26, color: "bg-blue-500" },
  { name: "Giáo dục", amount: 2800000, percentage: 22, color: "bg-green-500" },
  { name: "Giao thông", amount: 1200000, percentage: 10, color: "bg-yellow-500" },
  { name: "Khác", amount: 800000, percentage: 6, color: "bg-gray-500" },
])

const transactions = ref([
  {
    id: 1,
    description: "Siêu thị Coopmart",
    amount: -450000,
    category: "Ăn uống",
    date: "2024-01-15",
    account: "Tài khoản chính",
  },
  {
    id: 2,
    description: "Học phí con",
    amount: -2800000,
    category: "Giáo dục",
    date: "2024-01-14",
    account: "Tài khoản con",
  },
  {
    id: 3,
    description: "Lương tháng 1",
    amount: 15000000,
    category: "Thu nhập",
    date: "2024-01-01",
    account: "Tài khoản chính",
  },
  {
    id: 4,
    description: "Mua quần áo",
    amount: -1200000,
    category: "Mua sắm",
    date: "2024-01-12",
    account: "Tài khoản đồng sở hữu",
  },
])
</script>
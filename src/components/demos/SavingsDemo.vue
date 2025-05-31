<template>
  <div class="space-y-6">
    <!-- Savings Overview -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <PiggyBank class="h-5 w-5 mr-2" />
        Tổng quan tiết kiệm
      </h4>
      <div class="grid grid-cols-3 gap-4">
        <div class="text-center p-4 bg-blue-50 rounded-lg">
          <p class="text-2xl font-bold text-blue-600">65.5M</p>
          <p class="text-sm text-gray-600">Tổng tiết kiệm</p>
        </div>
        <div class="text-center p-4 bg-green-50 rounded-lg">
          <p class="text-2xl font-bold text-green-600">3</p>
          <p class="text-sm text-gray-600">Mục tiêu đang có</p>
        </div>
        <div class="text-center p-4 bg-orange-50 rounded-lg">
          <p class="text-2xl font-bold text-orange-600">2.5M</p>
          <p class="text-sm text-gray-600">Tiết kiệm/tháng</p>
        </div>
      </div>
    </div>

    <!-- Savings Goals -->
    <div class="border rounded-lg p-6">
      <div class="flex justify-between items-center mb-4">
        <h4 class="font-semibold">Mục tiêu tiết kiệm</h4>
        <button 
          @click="showAddGoal = true"
          class="bg-blue-500 text-white px-3 py-1 rounded text-sm flex items-center"
        >
          <Plus class="h-4 w-4 mr-1" />
          Thêm mục tiêu
        </button>
      </div>
      <div class="space-y-4">
        <div v-for="goal in goals" :key="goal.id" class="border rounded-lg p-4">
          <div class="flex items-start justify-between mb-3">
            <div>
              <h5 class="font-medium">{{ goal.name }}</h5>
              <div class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs font-medium mt-1 inline-block">
                {{ goal.category }}
              </div>
            </div>
            <div class="text-right">
              <p class="font-semibold">
                {{ goal.current.toLocaleString() }} / {{ goal.target.toLocaleString() }} VND
              </p>
              <p class="text-sm text-gray-500 flex items-center">
                <Calendar class="h-3 w-3 mr-1" />
                {{ getDaysLeft(goal.deadline) }} ngày còn lại
              </p>
            </div>
          </div>
          <div class="space-y-2">
            <div class="flex justify-between text-sm">
              <span>Tiến độ</span>
              <span>{{ getProgress(goal) }}%</span>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div 
                class="bg-blue-500 h-2 rounded-full transition-all duration-500"
                :style="{ width: `${getProgress(goal)}%` }"
              ></div>
            </div>
            <p class="text-sm text-gray-600">Còn thiếu: {{ (goal.target - goal.current).toLocaleString() }} VND</p>
          </div>
          <div class="flex space-x-2 mt-4">
            <button class="flex-1 border border-gray-300 py-2 px-4 rounded text-sm hover:bg-gray-50">
              Nạp tiền
            </button>
            <button class="flex-1 border border-gray-300 py-2 px-4 rounded text-sm hover:bg-gray-50">
              Chỉnh sửa
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Add Goal Form -->
    <div v-if="showAddGoal" class="border border-blue-200 bg-blue-50 rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Target class="h-5 w-5 mr-2" />
        Thêm mục tiêu mới
      </h4>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Tên mục tiêu</label>
          <input 
            v-model="newGoal.name"
            type="text" 
            placeholder="VD: Mua nhà, du lịch..."
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Số tiền mục tiêu (VND)</label>
          <input 
            v-model="newGoal.amount"
            type="number" 
            placeholder="VD: 50000000"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Thời hạn</label>
          <input 
            v-model="newGoal.deadline"
            type="date"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div class="flex space-x-3">
          <button 
            @click="addGoal"
            class="flex-1 bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600"
          >
            Tạo mục tiêu
          </button>
          <button 
            @click="showAddGoal = false"
            class="flex-1 border border-gray-300 py-2 px-4 rounded-md hover:bg-gray-50"
          >
            Hủy
          </button>
        </div>
      </div>
    </div>

    <!-- Savings Tips -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <TrendingUp class="h-5 w-5 mr-2" />
        Gợi ý tiết kiệm
      </h4>
      <div class="space-y-3">
        <div class="flex items-center space-x-3 p-3 bg-green-50 rounded-lg">
          <div class="w-2 h-2 bg-green-500 rounded-full"></div>
          <p class="text-sm">Thiết lập chuyển khoản tự động 2.5M/tháng để đạt mục tiêu</p>
        </div>
        <div class="flex items-center space-x-3 p-3 bg-blue-50 rounded-lg">
          <div class="w-2 h-2 bg-blue-500 rounded-full"></div>
          <p class="text-sm">Giảm chi tiêu cà phê 200K/tháng có thể tăng tiết kiệm 8%</p>
        </div>
        <div class="flex items-center space-x-3 p-3 bg-orange-50 rounded-lg">
          <div class="w-2 h-2 bg-orange-500 rounded-full"></div>
          <p class="text-sm">Đầu tư tiết kiệm vào sổ tiết kiệm lãi suất 6%/năm</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { PiggyBank, Plus, Calendar, Target, TrendingUp } from 'lucide-vue-next'

const showAddGoal = ref(false)
const newGoal = ref({ name: '', amount: '', deadline: '' })

const goals = ref([
  {
    id: 1,
    name: "Du lịch gia đình Đà Lạt",
    target: 15000000,
    current: 8500000,
    deadline: "2024-12-31",
    category: "Du lịch",
  },
  {
    id: 2,
    name: "Mua xe máy mới",
    target: 45000000,
    current: 32000000,
    deadline: "2025-06-30",
    category: "Phương tiện",
  },
  {
    id: 3,
    name: "Học phí đại học con",
    target: 100000000,
    current: 25000000,
    deadline: "2026-08-31",
    category: "Giáo dục",
  },
])

const getDaysLeft = (deadline) => {
  return Math.ceil((new Date(deadline).getTime() - new Date().getTime()) / (1000 * 60 * 60 * 24))
}

const getProgress = (goal) => {
  return ((goal.current / goal.target) * 100).toFixed(1)
}

const addGoal = () => {
  showAddGoal.value = false
  newGoal.value = { name: '', amount: '', deadline: '' }
}
</script>
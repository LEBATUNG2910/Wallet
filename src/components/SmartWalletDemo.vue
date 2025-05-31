<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
    <!-- Header -->
    <header >
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4">
        <div class="flex items-center justify-between">
          <div class="flex items-center space-x-3">
            <div class="bg-gradient-to-r from-blue-600 to-indigo-600 p-2 rounded-lg">
              <CreditCard class="h-8 w-8 text-white" />
            </div>
            <div>
              <h1 class="text-2xl font-bold text-gray-900">SmartWallet Demo</h1>
              <p class="text-sm text-gray-600">Trải nghiệm các tính năng thực tế</p>
            </div>
          </div>
          <div class="bg-green-100 text-green-800 px-3 py-1 rounded-full text-sm font-medium flex items-center">
            <Eye class="h-4 w-4 mr-1" />
            Demo Version
          </div>
        </div>
      </div>
    </header>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="grid lg:grid-cols-3 gap-8">
        <!-- Feature List -->
        <div class="lg:col-span-1">
          <div class="space-y-4">
            <h2 class="text-xl font-semibold text-gray-900 mb-4">Chọn tính năng để demo</h2>
            <div 
              v-for="feature in features" 
              :key="feature.id"
              @click="selectedFeature = feature.id"
              :class="[
                'cursor-pointer transition-all hover:shadow-md rounded-lg border p-4',
                selectedFeature === feature.id 
                  ? 'ring-2 ring-blue-500 bg-blue-50 border-blue-200' 
                  : 'hover:bg-gray-50 border-gray-200'
              ]"
            >
              <div class="flex items-start space-x-3">
                <div :class="`${feature.color} p-2 rounded-lg`">
                  <component :is="feature.icon" class="h-5 w-5 text-white" />
                </div>
                <div class="flex-1">
                  <h3 class="font-semibold text-gray-900 text-sm">{{ feature.title }}</h3>
                  <p class="text-xs text-gray-600 mt-1">{{ feature.description }}</p>
                </div>
                <ArrowRight v-if="selectedFeature === feature.id" class="h-4 w-4 text-blue-500" />
              </div>
            </div>
          </div>
        </div>

        <!-- Demo Area -->
        <div class="lg:col-span-2">
          <div class="bg-white rounded-lg shadow border h-full">
            <div class="p-6 border-b">
              <div class="flex items-center space-x-3" v-if="currentFeature">
                <div :class="`${currentFeature.color} p-2 rounded-lg`">
                  <component :is="currentFeature.icon" class="h-6 w-6 text-white" />
                </div>
                <div>
                  <h3 class="text-lg font-semibold text-gray-900">{{ currentFeature.title }}</h3>
                  <p class="text-sm text-gray-600">{{ currentFeature.description }}</p>
                </div>
              </div>
            </div>
            <div class="p-6">
              <!-- Dynamic Component Rendering -->
              <AuthDemo v-if="selectedFeature === 'auth'" />
              <JointAccountDemo v-if="selectedFeature === 'joint'" />
              <ChildAccountDemo v-if="selectedFeature === 'child'" />
              <SavingsDemo v-if="selectedFeature === 'savings'" />
              <StatsDemo v-if="selectedFeature === 'stats'" />
              <AutoPayDemo v-if="selectedFeature === 'autopay'" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { UserCheck, Users, Shield, PiggyBank, BarChart3, Smartphone, Eye, CreditCard, ArrowRight } from 'lucide-vue-next'

// Import demo components
import AuthDemo from './demos/AuthDemo.vue'
import JointAccountDemo from './demos/JointAccountDemo.vue'
import ChildAccountDemo from './demos/ChildAccountDemo.vue'
import SavingsDemo from './demos/SavingsDemo.vue'
import StatsDemo from './demos/StatsDemo.vue'
import AutoPayDemo from './demos/AutoPayDemo.vue'

onMounted(() => {
  document.title = 'SmartWallet Demo - Trải nghiệm tính năng'
})

const selectedFeature = ref('auth')

const features = [
  {
    id: "auth",
    title: "Xác thực CCCD & Khuôn mặt",
    description: "Bảo mật tối đa với công nghệ nhận diện sinh trắc học và xác thực CCCD/CMND.",
    icon: UserCheck,
    color: "bg-blue-500",
  },
  {
    id: "joint",
    title: "Tài khoản đồng sở hữu",
    description: "Vợ chồng cùng quản lý ví, yêu cầu xác nhận cho các giao dịch lớn.",
    icon: Users,
    color: "bg-green-500",
  },
  {
    id: "child",
    title: "Quản lý tài khoản con",
    description: "Tạo nhiệm vụ chi tiêu cho con, phê duyệt qua hình ảnh xác minh.",
    icon: Shield,
    color: "bg-purple-500",
  },
  {
    id: "savings",
    title: "Kế hoạch tiết kiệm",
    description: "Đặt mục tiêu tiết kiệm gia đình với nhắc nhở thông minh.",
    icon: PiggyBank,
    color: "bg-orange-500",
  },
  {
    id: "stats",
    title: "Thống kê chi tiêu",
    description: "Biểu đồ trực quan theo danh mục và thời gian, báo cáo tổng quát.",
    icon: BarChart3,
    color: "bg-indigo-500",
  },
  {
    id: "autopay",
    title: "Thanh toán tự động",
    description: "Thiết lập thanh toán định kỳ với thông báo thông minh.",
    icon: Smartphone,
    color: "bg-red-500",
  },
]

const currentFeature = computed(() => features.find(f => f.id === selectedFeature.value))
</script>
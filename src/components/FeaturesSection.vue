<template>
  <section id="features" class="py-20 bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center space-y-4 mb-16">
        <h2 class="text-3xl lg:text-4xl font-bold text-gray-900">
          Tính năng đặc biệt
        </h2>
        <p class="text-xl text-gray-600 max-w-3xl mx-auto">
          Những tính năng độc đáo giúp gia đình bạn quản lý tài chính một cách thông minh và an toàn
        </p>
      </div>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="feature in features" :key="feature.title" 
             class="bg-gradient-to-br from-white to-gray-50 p-8 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-2">
          <div class="space-y-4">
            <div :class="feature.iconBg" class="w-16 h-16 rounded-2xl flex items-center justify-center">
              <component :is="feature.icon" class="h-8 w-8 text-white" />
            </div>
            <h3 class="text-xl font-bold text-gray-900">{{ feature.title }}</h3>
            <p class="text-gray-600 leading-relaxed">{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { 
  UserCheck,
  Users,
  Shield,
  PiggyBank,
  BarChart3,
  Smartphone
} from 'lucide-vue-next'

const features = [
  {
    title: 'Xác thực CCCD & Khuôn mặt',
    description: 'Bảo mật tối đa với công nghệ nhận diện sinh trắc học và xác thực CCCD/CMND.',
    icon: UserCheck,
    iconBg: 'bg-gradient-to-r from-blue-500 to-blue-600'
  },
  {
    title: 'Tài khoản đồng sở hữu',
    description: 'Vợ chồng cùng quản lý ví, yêu cầu xác nhận cho các giao dịch lớn.',
    icon: Users,
    iconBg: 'bg-gradient-to-r from-green-500 to-green-600'
  },
  {
    title: 'Quản lý tài khoản con',
    description: 'Tạo nhiệm vụ chi tiêu cho con, phê duyệt qua hình ảnh xác minh.',
    icon: Shield,
    iconBg: 'bg-gradient-to-r from-purple-500 to-purple-600'
  },
  {
    title: 'Kế hoạch tiết kiệm',
    description: 'Đặt mục tiêu tiết kiệm gia đình với nhắc nhở thông minh.',
    icon: PiggyBank,
    iconBg: 'bg-gradient-to-r from-orange-500 to-orange-600'
  },
  {
    title: 'Thống kê chi tiêu',
    description: 'Biểu đồ trực quan theo danh mục và thời gian, báo cáo tổng quát.',
    icon: BarChart3,
    iconBg: 'bg-gradient-to-r from-indigo-500 to-indigo-600'
  },
  {
    title: 'Thanh toán tự động',
    description: 'Thiết lập thanh toán định kỳ với thông báo thông minh.',
    icon: Smartphone,
    iconBg: 'bg-gradient-to-r from-red-500 to-red-600'
  }
]
</script>
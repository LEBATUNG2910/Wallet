<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-900 via-indigo-900 to-purple-900 relative overflow-hidden">
    <!-- Animated Background -->
    <div class="absolute inset-0">
      <div class="absolute top-20 left-10 w-72 h-72 bg-blue-400 rounded-full mix-blend-multiply filter blur-xl opacity-20 animate-pulse"></div>
      <div class="absolute bottom-20 right-10 w-72 h-72 bg-purple-400 rounded-full mix-blend-multiply filter blur-xl opacity-20 animate-pulse"></div>
    </div>

    <!-- Header -->
    <header class="relative z-10 p-6">
      <div class="flex items-center space-x-3">
        <div class="bg-gradient-to-r from-blue-400 to-indigo-400 p-2 rounded-lg">
          <Wallet class="h-8 w-8 text-white" />
        </div>
        <span class="text-2xl font-bold text-white">SmartWallet</span>
      </div>
    </header>

    <!-- Main Content -->
    <main class="relative z-10 flex items-center justify-center min-h-[80vh]">
      <div class="max-w-4xl mx-auto px-6 text-center space-y-12">
        
        <!-- Coming Soon Badge -->
        <div class="inline-flex items-center space-x-2 bg-white/20 backdrop-blur-sm px-6 py-3 rounded-full">
          <Clock class="h-5 w-5 text-blue-300" />
          <span class="text-white font-medium">Sắp ra mắt</span>
        </div>

        <!-- Main Title -->
        <div class="space-y-6">
          <h1 class="text-5xl lg:text-7xl font-bold text-white">
            Ví Điện Tử 
            <span class="bg-gradient-to-r from-blue-300 to-purple-300 bg-clip-text text-transparent">
              Gia Đình
            </span>
          </h1>
          <p class="text-xl text-white/80 max-w-2xl mx-auto">
            Quản lý tài chính gia đình thông minh với công nghệ bảo mật tiên tiến
          </p>
        </div>

        <!-- Countdown -->
        <div class="bg-white/10 backdrop-blur-sm rounded-2xl p-8 max-w-lg mx-auto">
          <h3 class="text-xl font-bold text-white mb-6">Ra mắt sau</h3>
          <div class="grid grid-cols-4 gap-4">
            <div v-for="(time, index) in countdown" :key="index" class="text-center">
              <div class="bg-white/20 rounded-lg p-4">
                <div class="text-2xl font-bold text-white">{{ time.value }}</div>
                <div class="text-white/70 text-xs">{{ time.label }}</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Key Features -->
        <div class="grid md:grid-cols-3 gap-6 max-w-3xl mx-auto">
          <div class="bg-white/10 backdrop-blur-sm p-6 rounded-xl text-center">
            <Shield class="h-8 w-8 text-blue-300 mx-auto mb-3" />
            <h3 class="font-bold text-white mb-2">Bảo mật cao</h3>
            <p class="text-white/70 text-sm">Xác thực CCCD & khuôn mặt</p>
          </div>
          <div class="bg-white/10 backdrop-blur-sm p-6 rounded-xl text-center">
            <Users class="h-8 w-8 text-green-300 mx-auto mb-3" />
            <h3 class="font-bold text-white mb-2">Quản lý gia đình</h3>
            <p class="text-white/70 text-sm">Tài khoản chung & tài khoản con</p>
          </div>
          <div class="bg-white/10 backdrop-blur-sm p-6 rounded-xl text-center">
            <PiggyBank class="h-8 w-8 text-yellow-300 mx-auto mb-3" />
            <h3 class="font-bold text-white mb-2">Tiết kiệm thông minh</h3>
            <p class="text-white/70 text-sm">Kế hoạch & mục tiêu tài chính</p>
          </div>
        </div>

        <!-- Sponsor Call -->
        <div class="bg-gradient-to-r from-yellow-400/20 to-orange-400/20 backdrop-blur-sm rounded-2xl p-8 max-w-2xl mx-auto">
          <Star class="h-8 w-8 text-yellow-400 mx-auto mb-4" />
          <h2 class="text-2xl font-bold text-white mb-4">Tìm kiếm nhà đầu tư</h2>
          <p class="text-white/90 mb-6">
            Cơ hội đầu tư vào thị trường fintech gia đình 25+ triệu người dùng tiềm năng
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <button class="bg-gradient-to-r from-yellow-400 to-orange-400 text-gray-900 px-6 py-3 rounded-lg font-semibold hover:scale-105 transition-transform">
              Liên hệ đầu tư
            </button>
            <button class="border-2 border-yellow-400 text-yellow-400 px-6 py-3 rounded-lg font-semibold hover:bg-yellow-400 hover:text-gray-900 transition-all">
              Xem kế hoạch
            </button>
          </div>
        </div>

        <!-- Email Signup -->
        <div class="bg-white/10 backdrop-blur-sm rounded-2xl p-8 max-w-lg mx-auto">
          <h3 class="text-xl font-bold text-white mb-4">Nhận thông báo ra mắt</h3>
          <div class="flex gap-3">
            <input 
              v-model="email"
              type="email" 
              placeholder="Email của bạn"
              class="flex-1 px-4 py-3 bg-white/20 border border-white/30 rounded-lg text-white placeholder-white/50 focus:outline-none focus:ring-2 focus:ring-blue-400"
            >
            <button 
              @click="subscribeEmail"
              class="bg-blue-500 text-white px-6 py-3 rounded-lg font-semibold hover:bg-blue-600 transition-colors"
            >
              Đăng ký
            </button>
          </div>
          <div v-if="subscribed" class="flex items-center justify-center space-x-2 text-green-400 mt-4">
            <CheckCircle class="h-5 w-5" />
            <span class="text-sm">Cảm ơn! Chúng tôi sẽ thông báo sớm nhất.</span>
          </div>
        </div>

      </div>
    </main>

    <!-- Footer -->
    <footer class="relative z-10 text-center py-8">
      <p class="text-white/60">
        &copy; 2024 SmartWallet - Phát triển tại Việt Nam 🇻🇳
      </p>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { 
  Wallet, 
  Clock, 
  Star, 
  CheckCircle,
  Shield,
  Users,
  PiggyBank
} from 'lucide-vue-next'

const email = ref('')
const subscribed = ref(false)
const countdown = ref([
  { value: '180', label: 'Ngày' },
  { value: '12', label: 'Giờ' },
  { value: '30', label: 'Phút' },
  { value: '45', label: 'Giây' }
])

let countdownInterval = null

onMounted(() => {
  document.title = 'SmartWallet - Sắp ra mắt'
  
  // Simple countdown (6 months = ~180 days)
  const targetDate = new Date()
  targetDate.setMonth(targetDate.getMonth() + 6)
  
  const updateCountdown = () => {
    const now = new Date().getTime()
    const target = targetDate.getTime()
    const difference = target - now
    
    if (difference > 0) {
      const days = Math.floor(difference / (1000 * 60 * 60 * 24))
      const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
      const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60))
      const seconds = Math.floor((difference % (1000 * 60)) / 1000)
      
      countdown.value = [
        { value: days.toString(), label: 'Ngày' },
        { value: hours.toString().padStart(2, '0'), label: 'Giờ' },
        { value: minutes.toString().padStart(2, '0'), label: 'Phút' },
        { value: seconds.toString().padStart(2, '0'), label: 'Giây' }
      ]
    }
  }
  
  updateCountdown()
  countdownInterval = setInterval(updateCountdown, 1000)
})

onUnmounted(() => {
  if (countdownInterval) {
    clearInterval(countdownInterval)
  }
})

const subscribeEmail = () => {
  if (email.value && email.value.includes('@')) {
    subscribed.value = true
    email.value = ''
    setTimeout(() => subscribed.value = false, 3000)
  }
}
</script>

<style scoped>
.animate-pulse {
  animation: pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse {
  0%, 100% {
    opacity: 0.2;
  }
  50% {
    opacity: 0.4;
  }
}
</style>
<template>
  <section id="security" class="py-20 bg-gradient-to-r from-blue-600 to-indigo-600">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid lg:grid-cols-2 gap-12 items-center">
        <div class="space-y-8">
          <div class="space-y-4">
            <h2 class="text-3xl lg:text-4xl font-bold text-white">
              Bảo mật tuyệt đối cho gia đình bạn
            </h2>
            <p class="text-xl text-blue-100 leading-relaxed">
              Với công nghệ mã hóa AES-256 và xác thực đa yếu tố, 
              chúng tôi đảm bảo tài sản của gia đình bạn luôn được bảo vệ.
            </p>
          </div>
          
          <div class="space-y-4">
            <div v-for="security in securityFeatures" :key="security.title"
                 class="flex items-start space-x-4 bg-white/10 backdrop-blur-sm p-4 rounded-lg">
              <div class="bg-white/20 p-2 rounded-lg">
                <component :is="security.icon" class="h-6 w-6 text-white" />
              </div>
              <div>
                <h4 class="font-semibold text-white">{{ security.title }}</h4>
                <p class="text-blue-100 text-sm">{{ security.description }}</p>
              </div>
            </div>
          </div>
        </div>
        
        <div class="relative">
          <div class="bg-white/10 backdrop-blur-sm rounded-2xl p-8 border border-white/20">
            <div class="space-y-6">
              <h3 class="text-xl font-semibold text-white text-center">Xác thực đa lớp</h3>
              
              <div class="space-y-4">
                <div class="flex items-center space-x-4 bg-white/10 p-4 rounded-lg">
                  <CreditCard class="h-8 w-8 text-white" />
                  <div>
                    <div class="text-white font-medium">CCCD/CMND</div>
                    <div class="text-blue-100 text-sm">Xác thực danh tính</div>
                  </div>
                </div>
                
                <div class="flex items-center space-x-4 bg-white/10 p-4 rounded-lg">
                  <Eye class="h-8 w-8 text-white" />
                  <div>
                    <div class="text-white font-medium">Nhận diện khuôn mặt</div>
                    <div class="text-blue-100 text-sm">AI sinh trắc học</div>
                  </div>
                </div>
                
                <div class="flex items-center space-x-4 bg-white/10 p-4 rounded-lg">
                  <Fingerprint class="h-8 w-8 text-white" />
                  <div>
                    <div class="text-white font-medium">Vân tay</div>
                    <div class="text-blue-100 text-sm">Đăng nhập nhanh</div>
                  </div>
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
import { 
  CreditCard, 
  Eye, 
  Fingerprint,
  Lock,
  Shield
} from 'lucide-vue-next'

const securityFeatures = [
  {
    title: 'Mã hóa AES-256',
    description: 'Dữ liệu được mã hóa với tiêu chuẩn quân sự',
    icon: Lock
  },
  {
    title: 'Xác thực đa yếu tố (MFA)',
    description: 'Bảo vệ nhiều lớp cho tài khoản của bạn',
    icon: Shield
  },
  {
    title: 'Token JWT',
    description: 'Phiên đăng nhập an toàn và tự động hết hạn',
    icon: CreditCard
  },
  {
    title: 'Chống tấn công Brute-force',
    description: 'Hệ thống phát hiện và ngăn chặn tự động',
    icon: Eye
  }
]
</script>
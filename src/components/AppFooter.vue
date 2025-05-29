<template>
  <footer class="bg-gray-900 text-white py-16">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="grid md:grid-cols-4 gap-8">
        <div class="space-y-4">
          <div class="flex items-center space-x-3">
            <div class="bg-gradient-to-r from-blue-600 to-indigo-600 p-2 rounded-lg">
              <Wallet class="h-6 w-6 text-white" />
            </div>
            <span class="text-xl font-bold">SmartWallet</span>
          </div>
          <p class="text-gray-400">
            Ví điện tử gia đình thông minh, an toàn và tiện lợi cho mọi nhà.
          </p>
        </div>
        
        <div>
          <h4 class="font-semibold mb-4">Sản phẩm</h4>
          <div class="space-y-2 text-gray-400">
            <div>Ví gia đình</div>
            <div>Tài khoản con</div>
            <div>Tiết kiệm thông minh</div>
            <div>Báo cáo chi tiêu</div>
          </div>
        </div>
        
        <div>
          <h4 class="font-semibold mb-4">Hỗ trợ</h4>
          <div class="space-y-2 text-gray-400">
            <div>Trung tâm trợ giúp</div>
            <div>Liên hệ</div>
            <div>Câu hỏi thường gặp</div>
            <div>Bảo mật</div>
          </div>
        </div>
        
        <div>
          <h4 class="font-semibold mb-4">Công ty</h4>
          <div class="space-y-2 text-gray-400">
            <div>Về chúng tôi</div>
            <div>Tuyển dụng</div>
            <div>Tin tức</div>
            <div>Đối tác</div>
          </div>
        </div>
      </div>
      
      <div class="border-t border-gray-800 mt-12 pt-8 text-center text-gray-400">
        <p>&copy; 2024 SmartWallet. Tất cả quyền được bảo lưu.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { Wallet } from 'lucide-vue-next'
</script>
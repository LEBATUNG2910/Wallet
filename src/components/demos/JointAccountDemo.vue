<template>
  <div class="space-y-6">
    <!-- Account Overview -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Users class="h-5 w-5 mr-2" />
        Tài khoản đồng sở hữu
      </h4>
      <div class="space-y-4">
        <div class="flex items-center justify-between">
          <div class="flex items-center space-x-4">
            <div class="w-10 h-10 bg-blue-500 rounded-full flex items-center justify-center text-white font-medium">
              AN
            </div>
            <div>
              <p class="font-medium">Anh Nguyễn</p>
              <p class="text-sm text-gray-500">Chủ tài khoản chính</p>
            </div>
          </div>
          <div class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs font-medium">
            Đã kết nối
          </div>
        </div>
        <div class="flex items-center space-x-4">
          <div class="w-10 h-10 bg-pink-500 rounded-full flex items-center justify-center text-white font-medium">
            CT
          </div>
          <div>
            <p class="font-medium">Chị Thảo</p>
            <p class="text-sm text-gray-500">Đồng sở hữu</p>
          </div>
        </div>
        <div class="mt-6 p-4 bg-blue-50 rounded-lg">
          <div class="flex justify-between items-center">
            <span class="text-sm text-gray-600">Số dư chung</span>
            <span class="text-2xl font-bold text-blue-600">2,500,000 VND</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Transaction Approval -->
    <div v-if="pendingTransaction" class="border border-orange-200 bg-orange-50 rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center text-orange-800">
        <AlertTriangle class="h-5 w-5 mr-2" />
        Yêu cầu phê duyệt giao dịch
      </h4>
      <div class="space-y-4">
        <div class="flex items-center justify-between">
          <div>
            <p class="font-medium">Mua laptop Dell XPS</p>
            <p class="text-sm text-gray-600">Từ: Anh Nguyễn</p>
            <p class="text-sm text-gray-500">2 phút trước</p>
          </div>
          <div class="text-right">
            <p class="text-xl font-bold text-red-600">-25,000,000 VND</p>
            <div class="bg-orange-100 text-orange-800 px-2 py-1 rounded text-xs font-medium inline-flex items-center">
              <Clock class="h-3 w-3 mr-1" />
              Chờ phê duyệt
            </div>
          </div>
        </div>
        <div class="border-t pt-4">
          <p class="text-sm text-gray-600 mb-3">Giao dịch lớn cần sự đồng ý của cả hai bên</p>
          <div class="flex space-x-3">
            <button 
              @click="handleApprove"
              :disabled="approvalSent"
              class="flex-1 bg-green-500 text-white py-2 px-4 rounded-md hover:bg-green-600 disabled:opacity-50"
            >
              {{ approvalSent ? 'Đã phê duyệt' : 'Phê duyệt' }}
            </button>
            <button class="flex-1 border border-gray-300 py-2 px-4 rounded-md hover:bg-gray-50">
              Từ chối
            </button>
          </div>
        </div>
      </div>
    </div>

    <div v-if="!pendingTransaction" class="border border-green-200 bg-green-50 rounded-lg p-6 text-center">
      <CheckCircle class="h-12 w-12 text-green-500 mx-auto mb-3" />
      <h3 class="font-semibold text-green-800 mb-2">Giao dịch đã được phê duyệt</h3>
      <p class="text-sm text-green-600">Laptop Dell XPS đã được mua thành công</p>
    </div>

    <!-- Quick Actions -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Thao tác nhanh</h4>
      <div class="grid grid-cols-2 gap-4">
        <button class="h-20 flex flex-col items-center justify-center border border-gray-300 rounded-lg hover:bg-gray-50">
          <Send class="h-6 w-6 mb-2" />
          <span class="text-sm">Chuyển tiền</span>
        </button>
        <button class="h-20 flex flex-col items-center justify-center border border-gray-300 rounded-lg hover:bg-gray-50">
          <Users class="h-6 w-6 mb-2" />
          <span class="text-sm">Mời thành viên</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Users, AlertTriangle, Clock, CheckCircle, Send } from 'lucide-vue-next'

const pendingTransaction = ref(true)
const approvalSent = ref(false)

const handleApprove = () => {
  approvalSent.value = true
  setTimeout(() => {
    pendingTransaction.value = false
  }, 2000)
}
</script>
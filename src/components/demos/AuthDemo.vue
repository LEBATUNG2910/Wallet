<template>
  <div class="space-y-6">
    <!-- Progress Steps -->
    <div class="flex items-center space-x-4">
      <div v-for="stepNum in [1, 2, 3]" :key="stepNum" class="flex items-center">
        <div :class="[
          'w-8 h-8 rounded-full flex items-center justify-center text-sm font-medium',
          step >= stepNum ? 'bg-blue-500 text-white' : 'bg-gray-200 text-gray-600'
        ]">
          <CheckCircle v-if="step > stepNum" class="h-4 w-4" />
          <span v-else>{{ stepNum }}</span>
        </div>
        <div v-if="stepNum < 3" :class="[
          'w-12 h-1 mx-2',
          step > stepNum ? 'bg-blue-500' : 'bg-gray-200'
        ]" />
      </div>
    </div>

    <!-- Step 1: CCCD -->
    <div v-if="step === 1" class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Upload class="h-5 w-5 mr-2" />
        Bước 1: Xác thực CCCD/CMND
      </h4>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Số CCCD/CMND</label>
          <input 
            v-model="cccdNumber"
            type="text" 
            placeholder="Nhập số CCCD/CMND"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div class="border-2 border-dashed border-gray-300 rounded-lg p-8 text-center">
          <Upload class="h-12 w-12 text-gray-400 mx-auto mb-4" />
          <p class="text-gray-600 mb-2">Tải lên ảnh CCCD/CMND</p>
          <p class="text-sm text-gray-500">Hỗ trợ JPG, PNG (tối đa 5MB)</p>
          <button class="mt-4 px-4 py-2 border border-gray-300 rounded-md hover:bg-gray-50">
            Chọn file
          </button>
        </div>
        <button 
          @click="handleCCCDSubmit"
          :disabled="!cccdNumber || isVerifying"
          class="w-full bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600 disabled:opacity-50 disabled:cursor-not-allowed"
        >
          {{ isVerifying ? 'Đang xác thực...' : 'Xác thực CCCD' }}
        </button>
      </div>
    </div>

    <!-- Step 2: Face Recognition -->
    <div v-if="step === 2" class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Camera class="h-5 w-5 mr-2" />
        Bước 2: Xác thực khuôn mặt
      </h4>
      <div class="space-y-4">
        <div class="bg-gray-100 rounded-lg p-8 text-center">
          <Camera class="h-16 w-16 text-gray-400 mx-auto mb-4" />
          <p class="text-gray-600 mb-2">Đặt khuôn mặt vào khung hình</p>
          <p class="text-sm text-gray-500">Đảm bảo ánh sáng đủ và nhìn thẳng vào camera</p>
        </div>
        <div class="flex items-center space-x-2 text-sm text-amber-600 bg-amber-50 p-3 rounded-lg">
          <AlertCircle class="h-4 w-4" />
          <span>Hãy giữ yên và nhìn thẳng vào camera</span>
        </div>
        <button 
          @click="handleFaceVerification"
          :disabled="isVerifying"
          class="w-full bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600 disabled:opacity-50"
        >
          {{ isVerifying ? 'Đang quét khuôn mặt...' : 'Bắt đầu quét' }}
        </button>
      </div>
    </div>

    <!-- Step 3: Success -->
    <div v-if="step === 3" class="text-center py-8">
      <CheckCircle class="h-16 w-16 text-green-500 mx-auto mb-4" />
      <h3 class="text-xl font-semibold text-gray-900 mb-2">Xác thực thành công!</h3>
      <p class="text-gray-600 mb-6">Tài khoản của bạn đã được xác thực và bảo mật</p>
      <div class="grid grid-cols-2 gap-4 mb-6">
        <div class="bg-green-50 p-4 rounded-lg">
          <div class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs font-medium mb-2 inline-block">
            CCCD Verified
          </div>
          <p class="text-sm text-gray-600">Số: ***123456</p>
        </div>
        <div class="bg-blue-50 p-4 rounded-lg">
          <div class="bg-blue-100 text-blue-800 px-2 py-1 rounded text-xs font-medium mb-2 inline-block">
            Face ID Active
          </div>
          <p class="text-sm text-gray-600">Độ chính xác: 99.8%</p>
        </div>
      </div>
      <button class="w-full bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600">
        Tiếp tục thiết lập tài khoản
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { CheckCircle, Upload, Camera, AlertCircle } from 'lucide-vue-next'

const step = ref(1)
const cccdNumber = ref('')
const isVerifying = ref(false)

const handleCCCDSubmit = async () => {
  isVerifying.value = true
  setTimeout(() => {
    isVerifying.value = false
    step.value = 2
  }, 2000)
}

const handleFaceVerification = async () => {
  isVerifying.value = true
  setTimeout(() => {
    isVerifying.value = false
    step.value = 3
  }, 3000)
}
</script>
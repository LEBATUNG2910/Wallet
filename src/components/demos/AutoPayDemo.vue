<template>
  <div class="space-y-6">
    <!-- Overview -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Smartphone class="h-5 w-5 mr-2" />
        Thanh toán tự động
      </h4>
      <div class="grid grid-cols-3 gap-4">
        <div class="text-center p-4 bg-blue-50 rounded-lg">
          <p class="text-2xl font-bold text-blue-600">4</p>
          <p class="text-sm text-gray-600">Dịch vụ đăng ký</p>
        </div>
        <div class="text-center p-4 bg-green-50 rounded-lg">
          <p class="text-2xl font-bold text-green-600">2.15M</p>
          <p class="text-sm text-gray-600">Tổng/tháng</p>
        </div>
        <div class="text-center p-4 bg-orange-50 rounded-lg">
          <p class="text-2xl font-bold text-orange-600">3</p>
          <p class="text-sm text-gray-600">Sắp đến hạn</p>
        </div>
      </div>
    </div>

    <!-- Auto Payment List -->
    <div class="border rounded-lg p-6">
      <div class="flex justify-between items-center mb-4">
        <h4 class="font-semibold">Danh sách thanh toán</h4>
        <button 
          @click="showAddPayment = true"
          class="bg-blue-500 text-white px-3 py-1 rounded text-sm flex items-center"
        >
          <Plus class="h-4 w-4 mr-1" />
          Thêm dịch vụ
        </button>
      </div>
      <div class="space-y-4">
        <div v-for="payment in payments" :key="payment.id" class="border rounded-lg p-4">
          <div class="flex items-center justify-between mb-3">
            <div class="flex items-center space-x-3">
              <div class="bg-blue-100 p-2 rounded-lg">
                <component :is="payment.icon" class="h-5 w-5 text-blue-600" />
              </div>
              <div>
                <h5 class="font-medium">{{ payment.name }}</h5>
                <div class="bg-gray-100 text-gray-800 px-2 py-1 rounded text-xs font-medium mt-1 inline-block">
                  {{ payment.category }}
                </div>
              </div>
            </div>
            <div class="text-right">
              <p class="font-semibold text-lg">{{ payment.amount.toLocaleString() }} VND</p>
              <div :class="getStatusClass(payment.status)">
                <component :is="getStatusIcon(payment.status)" class="h-3 w-3 mr-1" />
                {{ getStatusText(payment.status) }}
              </div>
            </div>
          </div>
          <div class="flex items-center justify-between text-sm text-gray-600 mb-3">
            <div class="flex items-center space-x-1">
              <Calendar class="h-4 w-4" />
              <span>Thanh toán tiếp theo: {{ payment.nextPayment }}</span>
            </div>
            <span :class="getDaysLeftClass(payment.nextPayment)">
              {{ getDaysLeft(payment.nextPayment) }} ngày nữa
            </span>
          </div>
          <div class="flex items-center justify-between pt-3 border-t">
            <div class="flex items-center space-x-2">
              <label class="relative inline-flex items-center cursor-pointer">
                <input 
                  type="checkbox" 
                  :checked="payment.status === 'active'"
                  @change="togglePaymentStatus(payment.id)"
                  class="sr-only peer"
                >
                <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-blue-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-blue-600"></div>
              </label>
              <span class="text-sm">{{ payment.status === 'active' ? 'Tự động thanh toán' : 'Tạm dừng' }}</span>
            </div>
            <div class="flex space-x-2">
              <button class="border border-gray-300 px-3 py-1 rounded text-sm hover:bg-gray-50">
                Chỉnh sửa
              </button>
              <button class="border border-gray-300 px-3 py-1 rounded text-sm hover:bg-gray-50">
                Lịch sử
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Add Payment Form -->
    <div v-if="showAddPayment" class="border border-blue-200 bg-blue-50 rounded-lg p-6">
      <h4 class="font-semibold mb-4 flex items-center">
        <Plus class="h-5 w-5 mr-2" />
        Thêm dịch vụ thanh toán tự động
      </h4>
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Tên dịch vụ</label>
          <input 
            v-model="newPayment.name"
            type="text" 
            placeholder="VD: Tiền điện, Internet..."
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">Số tiền (VND)</label>
          <input 
            v-model="newPayment.amount"
            type="number" 
            placeholder="VD: 300000"
            class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
          />
        </div>
        <div class="flex space-x-3">
          <button 
            @click="addPayment"
            class="flex-1 bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600"
          >
            Thêm dịch vụ
          </button>
          <button 
            @click="showAddPayment = false"
            class="flex-1 border border-gray-300 py-2 px-4 rounded-md hover:bg-gray-50"
          >
            Hủy
          </button>
        </div>
      </div>
    </div>

    <!-- Recent Transactions -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Giao dịch tự động gần đây</h4>
      <div class="space-y-3">
        <div v-for="transaction in recentTransactions" :key="transaction.id" 
             class="flex items-center justify-between p-3 border rounded-lg">
          <div class="flex items-center space-x-3">
            <div :class="transaction.success ? 'bg-green-100' : 'bg-red-100'" class="p-2 rounded-lg">
              <CheckCircle v-if="transaction.success" class="h-4 w-4 text-green-600" />
              <AlertTriangle v-else class="h-4 w-4 text-red-600" />
            </div>
            <div>
              <p class="font-medium">{{ transaction.name }}</p>
              <p class="text-sm text-gray-500">{{ transaction.date }} - {{ transaction.status }}</p>
            </div>
          </div>
          <span :class="transaction.success ? 'font-semibold text-green-600' : 'font-semibold text-red-600'">
            {{ transaction.amount.toLocaleString() }} VND
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Smartphone, Plus, Calendar, CheckCircle, AlertTriangle, Clock, Wifi, Zap } from 'lucide-vue-next'

const showAddPayment = ref(false)
const newPayment = ref({ name: '', amount: '' })

const payments = ref([
  {
    id: 1,
    name: "Điện thoại Viettel",
    amount: 200000,
    nextPayment: "2024-02-01",
    status: "active",
    icon: Smartphone,
    category: "Viễn thông",
  },
  {
    id: 2,
    name: "Tiền điện EVN",
    amount: 450000,
    nextPayment: "2024-02-05",
    status: "active",
    icon: Zap,
    category: "Tiện ích",
  },
  {
    id: 3,
    name: "Internet FPT",
    amount: 300000,
    nextPayment: "2024-02-10",
    status: "paused",
    icon: Wifi,
    category: "Viễn thông",
  },
])

const recentTransactions = ref([
  {
    id: 1,
    name: "Điện thoại Viettel",
    amount: -200000,
    date: "01/01/2024",
    status: "Thành công",
    success: true,
  },
  {
    id: 2,
    name: "Tiền điện EVN",
    amount: -450000,
    date: "05/01/2024",
    status: "Thành công",
    success: true,
  },
  {
    id: 3,
    name: "Internet FPT",
    amount: -300000,
    date: "10/01/2024",
    status: "Thất bại (Không đủ số dư)",
    success: false,
  },
])

const getStatusClass = (status) => {
  const classes = {
    active: 'bg-green-100 text-green-800',
    paused: 'bg-yellow-100 text-yellow-800',
    failed: 'bg-red-100 text-red-800'
  }
  return `px-2 py-1 rounded text-xs font-medium inline-flex items-center ${classes[status] || 'bg-gray-100 text-gray-800'}`
}

const getStatusIcon = (status) => {
  const icons = {
    active: CheckCircle,
    paused: Clock,
    failed: AlertTriangle
  }
  return icons[status] || CheckCircle
}

const getStatusText = (status) => {
  const texts = {
    active: 'Hoạt động',
    paused: 'Tạm dừng',
    failed: 'Lỗi'
  }
  return texts[status] || status
}

const getDaysLeft = (date) => {
  return Math.ceil((new Date(date).getTime() - new Date().getTime()) / (1000 * 60 * 60 * 24))
}

const getDaysLeftClass = (date) => {
  const days = getDaysLeft(date)
  return days <= 3 ? 'text-orange-600 font-medium' : ''
}

const togglePaymentStatus = (paymentId) => {
  const paymentIndex = payments.value.findIndex(payment => payment.id === paymentId)
  if (paymentIndex !== -1) {
    payments.value[paymentIndex].status = 
      payments.value[paymentIndex].status === 'active' ? 'paused' : 'active'
  }
}

const addPayment = () => {
  showAddPayment.value = false
  newPayment.value = { name: '', amount: '' }
}
</script>
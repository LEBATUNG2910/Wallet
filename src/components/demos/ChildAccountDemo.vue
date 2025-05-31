<template>
  <div class="space-y-6">
    <!-- Child Accounts Overview -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Tài khoản con</h4>
      <div class="space-y-4">
        <div class="flex items-center justify-between p-3 bg-blue-50 rounded-lg">
          <div class="flex items-center space-x-3">
            <div class="w-10 h-10 bg-blue-500 rounded-full flex items-center justify-center text-white font-medium text-sm">
              BA
            </div>
            <div>
              <p class="font-medium">Bé An (14 tuổi)</p>
              <p class="text-sm text-gray-500">Học sinh THCS</p>
            </div>
          </div>
          <div class="text-right">
            <p class="font-semibold">500,000 VND</p>
            <p class="text-sm text-gray-500">Hạn mức tháng</p>
          </div>
        </div>
        <div class="flex items-center justify-between p-3 bg-green-50 rounded-lg">
          <div class="flex items-center space-x-3">
            <div class="w-10 h-10 bg-green-500 rounded-full flex items-center justify-center text-white font-medium text-sm">
              BM
            </div>
            <div>
              <p class="font-medium">Bé Minh (12 tuổi)</p>
              <p class="text-sm text-gray-500">Học sinh tiểu học</p>
            </div>
          </div>
          <div class="text-right">
            <p class="font-semibold">300,000 VND</p>
            <p class="text-sm text-gray-500">Hạn mức tháng</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Task Management -->
    <div class="border rounded-lg p-6">
      <h4 class="font-semibold mb-4">Nhiệm vụ chi tiêu</h4>
      <div class="space-y-4">
        <div v-for="task in tasks" :key="task.id" class="border rounded-lg p-4">
          <div class="flex items-start justify-between mb-3">
            <div class="flex items-center space-x-3">
              <BookOpen v-if="task.title.includes('sách')" class="h-8 w-8 text-blue-500" />
              <ShoppingBag v-else class="h-8 w-8 text-green-500" />
              <div>
                <h5 class="font-medium">{{ task.title }}</h5>
                <p class="text-sm text-gray-500">Từ: {{ task.child }}</p>
                <p class="text-sm text-gray-600">{{ task.description }}</p>
              </div>
            </div>
            <div class="text-right">
              <p class="font-semibold text-lg">{{ task.amount.toLocaleString() }} VND</p>
              <div :class="[
                'px-2 py-1 rounded text-xs font-medium inline-flex items-center',
                task.status === 'pending' ? 'bg-yellow-100 text-yellow-800' :
                task.status === 'approved' ? 'bg-green-100 text-green-800' :
                task.status === 'completed' ? 'bg-blue-100 text-blue-800' :
                'bg-red-100 text-red-800'
              ]">
                <Clock v-if="task.status === 'pending'" class="h-3 w-3 mr-1" />
                <CheckCircle v-else-if="task.status === 'approved' || task.status === 'completed'" class="h-3 w-3 mr-1" />
                <X v-else class="h-3 w-3 mr-1" />
                {{ getStatusText(task.status) }}
              </div>
            </div>
          </div>
          
          <div v-if="task.status === 'pending'" class="flex space-x-3 pt-3 border-t">
            <button 
              @click="approveTask(task.id)"
              class="flex-1 bg-green-500 text-white py-2 px-4 rounded-md hover:bg-green-600 text-sm flex items-center justify-center"
            >
              <CheckCircle class="h-4 w-4 mr-1" />
              Phê duyệt
            </button>
            <button 
              @click="rejectTask(task.id)"
              class="flex-1 border border-gray-300 py-2 px-4 rounded-md hover:bg-gray-50 text-sm flex items-center justify-center"
            >
              <X class="h-4 w-4 mr-1" />
              Từ chối
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Quick Stats -->
    <div class="grid grid-cols-3 gap-4">
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-blue-600">2</p>
        <p class="text-sm text-gray-600">Nhiệm vụ tháng này</p>
      </div>
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-green-600">350K</p>
        <p class="text-sm text-gray-600">Đã chi tiêu</p>
      </div>
      <div class="text-center py-4 border rounded-lg">
        <p class="text-2xl font-bold text-orange-600">450K</p>
        <p class="text-sm text-gray-600">Còn lại</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { BookOpen, ShoppingBag, Clock, CheckCircle, X } from 'lucide-vue-next'

const tasks = ref([
  {
    id: 1,
    title: "Mua sách giáo khoa",
    amount: 150000,
    child: "Bé An",
    status: "pending",
    description: "Mua sách toán lớp 8",
  },
  {
    id: 2,
    title: "Đi siêu thị mua đồ ăn",
    amount: 200000,
    child: "Bé Minh",
    status: "completed",
    description: "Mua rau củ và thịt cá",
  },
])

const getStatusText = (status) => {
  const statusMap = {
    pending: 'Chờ duyệt',
    approved: 'Đã duyệt',
    completed: 'Hoàn thành',
    rejected: 'Từ chối'
  }
  return statusMap[status] || status
}

const approveTask = (taskId) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskId)
  if (taskIndex !== -1) {
    tasks.value[taskIndex].status = 'approved'
  }
}

const rejectTask = (taskId) => {
  const taskIndex = tasks.value.findIndex(task => task.id === taskId)
  if (taskIndex !== -1) {
    tasks.value[taskIndex].status = 'rejected'
  }
}
</script>
<template>
  <div class="p-6 max-w-xl mx-auto">
    <h2 class="text-2xl font-bold mb-4">Admin - Đăng bài mới</h2>

    <div v-if="!user">
      <input v-model="email" placeholder="Email" class="input" />
      <input v-model="password" type="password" placeholder="Mật khẩu" class="input" />
      <button @click="login" class="btn">Đăng nhập</button>
    </div>

    <div v-else>
      <p>Xin chào, {{ user.email }}</p>
      <input v-model="title" placeholder="Tiêu đề bài viết" class="input" />
      <textarea v-model="content" placeholder="Nội dung bài viết" class="input h-32"></textarea>
      <button @click="upload" class="btn">Đăng bài</button>
      <button @click="logout" class="btn btn-red mt-2">Đăng xuất</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { auth, db } from '../firebase/config'
import { signInWithEmailAndPassword, signOut, onAuthStateChanged } from 'firebase/auth'
import { collection, addDoc, serverTimestamp } from 'firebase/firestore'

const email = ref('')
const password = ref('')
const user = ref(null)

onAuthStateChanged(auth, (u) => user.value = u)

const login = async () => {
  await signInWithEmailAndPassword(auth, email.value, password.value)
}

const logout = async () => {
  await signOut(auth)
}

const title = ref('')
const content = ref('')

const upload = async () => {
  if (title.value && content.value) {
    await addDoc(collection(db, 'posts'), {
      title: title.value,
      content: content.value,
      createdAt: serverTimestamp(),
      author: user.value.email
    })
    title.value = ''
    content.value = ''
    alert("Đã đăng bài thành công!")
  }
}
</script>

<style scoped>
.input {
  display: block;
  margin-bottom: 10px;
  padding: 8px;
  width: 100%;
  border-radius: 6px;
  border: 1px solid #ccc;
}
.btn {
  padding: 10px 20px;
  background-color: #0d9488;
  color: white;
  border: none;
  border-radius: 6px;
}
.btn-red {
  background-color: #ef4444;
}
</style>

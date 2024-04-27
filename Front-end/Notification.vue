<template>
    <div class="notification-container">
      <h2>通知中心</h2>
      <!-- 使用表格来显示通知 -->
      <table class="notification-table">
        <thead>
          <tr>
            <th>通知内容</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <!-- 使用v-for循环渲染通知 -->
          <tr v-for="(notification, index) in notifications" :key="index">
            <td>{{ notification.message }}</td>
            <td>
              <button class="btn text-primary" @click="removeNotification(index)">知道啦</button>
              <button class="btn text-primary" @click="goToInventory">去入库</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  
  </script>
  
  <style scoped>
  
  </style>
  
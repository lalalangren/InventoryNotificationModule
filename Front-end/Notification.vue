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
  import axios from '@/axios/axios';
  export default {
    name: 'Notification',
    data() {
      return {
        notifications: []
      };
    },
    created() {
      // 在组件创建时检查库存并生成通知
      this.checkInventory();
      this.showPermissionsLink = userRole === 'admin';
    },
    methods: {
      async checkInventory() {
        try {
          const token = sessionStorage.getItem("access_token");
          const config = { headers: { 'Authorization': token } };
          const response = await axios.get('/products/all', config);
          const inventory = response.data;
          
          // 检查库存，如果低于阈值则生成通知
          inventory.forEach(product => {
            const leaststock = 1700;
            if (product.stockQuantity < leaststock) {
              const notification = {
                message: `部件${product.productName}库存低于阈值${leaststock}`,
                productId: product.productID
              };
              this.notifications.push(notification);
            }
          });
          console.log(inventory);
          console.log(this.notifications);
        } catch (error) {
          console.error('Error checking inventory:', error);
        }
      },
      removeNotification(index) {
        this.notifications.splice(index, 1);
      },
      goToInventory() {
        
        this.$router.push('/inventory-management');
      }
    }
  };
  </script>
  
  <style scoped>
  
  </style>
  

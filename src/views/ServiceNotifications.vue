<template>
  <div class="service-container">
    <h2>{{ serviceName }}</h2>
    <div class="notifications-container">
      <ul>
        <li v-for="notification in notifications" :key="notification.id" class="notification-item">
          <h2 class="text-center">{{ notification.title }}</h2>
          <p class="text-muted textalignCenter">{{ notification.timestamp }}</p>
          <div>
            <p>{{ notification.message }}</p>
          </div>
          <div class="text-end">
            <a class="btn btn-primary marginR10" :href="notification.url">{{ notification.url }}</a>
            <a class="btn btn-danger" :href="notification.url">X</a>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['serviceName', 'notifications'],
};
</script>

<style>

.service-container {
  border: 1px solid;
  padding: 10px;
  margin-bottom: 20px;
}

.notification-item {
  border-radius: 20px;
  border: 1px solid;
  padding: 10px;
  margin-bottom: 20px;
  list-style: none;
}
</style>

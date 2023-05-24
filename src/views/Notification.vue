<template>
  <div id="app">

    <ul>
      <li v-for="notification in notifications" :key="notification.id" class="notification-item border border-dark">
        <h2 class="text-center">{{ notification.title }}</h2>
        <p class="text-muted textalignCenter">{{ notification.timestamp }}</p>

        <div>
          <p>{{ notification.message }}</p>
        </div>
      <div class="text-end">
        <a class="btn btn-primary marginR10" href="{{ notification.url }}">{{ notification.url }}</a>
        <a class="btn btn-danger" href="{{ notification.url }}"> X </a>
      </div>
      </li>
    </ul>
  </div>



</template>


<style>

ul {
  list-style: none;
}

.notification-item {
  margin-bottom: 30px;
  padding: 10px;
}

.textalignCenter {
  text-align: center;
}

.marginR10 {
  margin-right: 10px;
}





</style>
<script>
export default {
  data() {
    return {
      notifications: [] // tableau pour stocker les notifications récupérées
    };
  },
  mounted() {
    this.fetchNotifications(); // appel à la fonction fetchNotifications() lors du montage du composant
  },
  methods: {
    fetchNotifications() {
      // Remplacez 'userId' par l'identifiant de l'utilisateur connecté
      const userId = '8';

      // Effectuer l'appel API pour récupérer les notifications de l'utilisateur spécifié
      // Remplacez l'URL de l'API par votre propre URL, en incluant l'identifiant de l'utilisateur
      fetch(`http://172.17.0.3/notification_pebble/public/api/notifications/user/${userId}`)
          .then(response => response.json())
          .then(data => {
            this.notifications = data; // Mettre à jour le tableau des notifications avec les données récupérées
          })
          .catch(error => {
            console.log(error);
          });
    }
  }
};

</script>

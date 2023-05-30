<template>
  <div id="app">
    <pre>{{ groupedNotifications }}</pre>
    <ServiceNotifications
        v-for="(serviceId, index) in serviceIds"
        :key="index"
        :serviceName="getServiceName(serviceId)"
        :notifications="groupedNotifications[serviceId]"
    />
  </div>
</template>



<style>
.service-header {
  background-color: #f5f5f5;
  padding: 10px;
}
</style>

<script>
import ServiceNotifications from './ServiceNotifications.vue';

export default {
  components: {
    ServiceNotifications,
  },
  data() {
    return {
      notifications: [], // tableau pour stocker les notifications récupérées
      serviceIds: [], // tableau pour stocker les IDs de services
    };
  },
  mounted() {
    this.fetchNotifications(); // appel à la fonction fetchNotifications() lors du montage du composant
  },
  computed: {
    groupedNotifications() {
      // Regroupe les notifications par service
      const grouped = {};
      for (const notification of this.notifications) {
        const serviceId = notification.servicesId;
        if (!grouped[serviceId]) {
          grouped[serviceId] = [];
        }
        grouped[serviceId].push(notification);
      }
      return grouped;
    },
  },
  methods: {
    fetchNotifications() {
      // Remplacez 'userId' par l'identifiant de l'utilisateur connecté
      const userId = '8';

      // Effectuer l'appel API pour récupérer les notifications de l'utilisateur spécifié
      // Remplacez l'URL de l'API par votre propre URL, en incluant l'identifiant de l'utilisateur
      fetch(`http://172.17.0.2/notification_pebble/public/api/notifications/user/${userId}`)
          .then((response) => response.json())
          .then((data) => {
            this.notifications = data; // Mettre à jour le tableau des notifications avec les données récupérées
            this.serviceIds = Array.from(new Set(data.map((notification) => notification.servicesId))); // Récupérer les IDs de services uniques
          })
          .catch((error) => {
            console.log(error);
          });
    },

    getServiceName(serviceId) {
      if (serviceId !== undefined) {
        return serviceId.toString();
      }
      return '';
    },
  },
};
</script>

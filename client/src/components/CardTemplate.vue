<template>
  <div class="d-flex justify-content-around flex-wrap">
    <div v-for="(data, index) in tasks" :key="index">
      <CardContainer :data="data" :key="index" :bColor="changeColor(data.name)"/>
    </div>
  </div>
</template>

<script>
// import CardContent from '@/components/CardContent.vue';
import CardContainer from '@/components/CardContainer.vue'
export default {
  name: "card-template",
  components: {
    CardContainer
  },
  props: ["tasks"],
  methods: {
    changeColor(type) {
      if (type == "Pre-Log") {
        return "#CC0000";
      } else if (type == "To-Do") {
        return "#FFDF00";
      } else if (type == "On-Going") {
        return "#006994";
      } else if (type == "Finished") {
        return "#32CD32";
      }
    },
  }
};
</script>

<style scoped>
.title {
  font-family: 'Italiana', serif;
  font-weight: bolder;
}

.card-content {
  background-color: #f2f2f2;
  padding: 10px;
  border-radius: 8px;
}
.e-btn {
  display: flex;
  justify-content: space-around;
}
</style>
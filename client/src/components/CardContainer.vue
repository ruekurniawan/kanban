<template>
  <div class="card m-3" style="width: 18rem;">
    <div class="card-body" :style="{'background-color': bColor}">
      <h5 class="card-title title">{{ data.name }}</h5>
      <!-- <CardContent v-for="(task, index) in data.tasks" :key="index" :task-content="task" /> -->
      <div class="card-content m-4" v-for="(task, index) in data.tasks" :key="index">
        <CardContent :newData="task"/>
      </div>
    </div>
  </div>
</template>

<script>

// import app from '@/api/firebase.js'
import CardContent from '@/components/CardContent.vue'
export default {
  components: {
    CardContent
  },
  props: ["data", "bColor"],
  
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
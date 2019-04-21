<template>
  <div class="kanban">
    <h5>Name</h5>
    <p class="card-text p-3 title">{{ newData.name }}</p>
    <h5>Description</h5>
    <p class="card-text p-3 title">{{ newData.description }}</p>
    <h5>Point</h5>
    <p class="card-text p-3 title">{{ newData.point }}</p>
    <!-- <p class="card-text p-3 title">{{ task.status }}</p> -->
    <div class="e-btn">
      <button
        type="button"
        class="btn btn-sm btn-danger"
        @click.prevent="deleteTask(newData.id)"
      >Delete</button>
      <button
        v-if="buttonName(newData.status, -1)"
        @click.prevent="goPrev(newData.id, newData.status)"
        type="button"
        class="btn btn-sm btn-primary"
      >{{buttonName(newData.status, -1)}}</button>
      <button
        v-if="buttonName(newData.status, 1)"
        type="button"
        @click.prevent="goNext(newData.id, newData.status)"
        class="btn btn-sm btn-primary"
      >{{buttonName(newData.status, 1)}}</button>
    </div>
  </div>
</template>

<script>
import app from '@/api/firebase.js'
export default {
  props: ["newData"],
  data() {
    return {
      buttons: ['Pre-Log', 'To-Do', 'On-Going', 'Finished']
    }
  },
    
  methods: {
    buttonName(status, arah) {
      return this.buttons[this.buttons.indexOf(status) + arah]
    },

    deleteTask(value) {
      // console.log(this.tas, '+++++++')
      app.collection('message')
        .doc(value)
        .delete();
    },

    goPrev(valueId, valueStatus) {
      if(valueStatus == 'Pre-Log') {
      this.prev = valueStatus
        app.collection('message')
        .doc(valueId)
        .update({
          status: valueStatus
        })
      } else if(valueStatus == 'To-Do'){
        this.prev = valueStatus
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'Pre-Log'
        })
      } else if(valueStatus == 'On-Going'){
        this.prev = valueStatus
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'To-Do'
        })
      } else if(valueStatus == 'Finished'){
        this.prev = valueStatus
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'On-Going'
        })
      }
    },
    
    goNext(valueId, valueStatus) {
      if(valueStatus == 'Pre-Log') {
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'To-Do'
        })
      } else if(valueStatus == 'To-Do'){
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'On-Going'
        })
      } else if(valueStatus == 'On-Going'){
        app.collection('message')
        .doc(valueId)
        .update({
          status: 'Finished'
        })
      } else if(valueStatus == 'Finished'){
        app.collection('message')
        .doc(valueId)
        .update({
          status: valueStatus
        })
      }
      
    }
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
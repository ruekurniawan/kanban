<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">Kanban</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <div>
          <b-button v-b-modal.modal-prevent>Add Todo</b-button>

          <!-- Modal Component -->
          <b-modal
            id="modal-prevent"
            ref="modal"
            title="Submit your name"
            @ok="handleOk"
            @shown="clearName"
          >
            <form @submit.stop.prevent="handleSubmit">
              <h5>Add Task</h5>
              <b-form-input v-model="name" placeholder="Enter your task"></b-form-input>
              <h5>Description</h5>
              <b-form-input v-model="description" placeholder="Enter your description"></b-form-input>
              <h5>Point</h5>
              <b-form-input v-model="point" placeholder="Enter your point"></b-form-input>
            </form>
          </b-modal>
        </div>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
import app from '@/api/firebase.js'
export default {
  data() {
    return {
      name: "",
      description: "",
      point: "",
      names: []
    };
  },
  methods: {
    clearName() {
      this.name = "";
      this.description = "",
      this.point = ""
    },
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      this.handleSubmit();
    },
    handleSubmit() {
      // this.names.push(this.name, this.description);
      app.collection('message').add({
        name: this.name,
        description: this.description,
        point: this.point,
        status: 'Pre-Log'
      })
      .then(() => {
        // console.log('masukk');
        this.clearName()
      })
      .catch(err => {
        console.log(err)
      })
      
      this.clearName();
      this.$nextTick(() => {
        // Wrapped in $nextTick to ensure DOM is rendered before closing
        this.$refs.modal.hide();
      });
    }
  }
};
</script>
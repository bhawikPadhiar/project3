<template>

  <div class="input-group mb-3">
    <router-link to="/" tag="button" class="btn btn-warning">home</router-link>
    <input type="text" class="form-control" v-model="task.taskname" />
    <button v-on:click="editTask">Edit Task</button>

    <div>Selected:{{ task.priority }}</div>

    <!-- <select class="form-select" :value="value" @input="$emit('input', $event.target.value)" > -->
    <select class="form-select" v-model="task.priority">
      <option class="badge bg-success">Low</option>
      <option class="badge bg-warning">Medium</option>
      <option class="badge bg-danger">High</option>
    </select>

  </div>

</template>

<script>
import axios from 'axios'
export default {
  // props: {
  //   task: {
  //     type: Array
  //   }
  // },
  // props:['value'],
  data() {
    return {
      task: [],
      //  mutableList: JSON.parse(this.task),
      // tasks: [],
      id: this.$route.params.id,
    }
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/task/` + this.id);
      this.task = res.data;
      console.log(this.value)
    } catch (error) {
      console.log(error);
    }
  },

  methods: {
    editTask: function () {
      axios.put('http://localhost:3000/task/' + this.$route.params.id,
        {
          taskname: this.task.taskname,
          priority: this.task.priority,
          // taskname:"", 
          // priority:""
        },

        {
          // Config
        }
      );
    },
    // const res =  axios({
    //     method: 'put',
    //     url: 'http://localhost:3000/task/`+this.id,
    //     data: {
    //         title: 'Making PUT Requests with Axios',
    //         status: 'published'
    //     }
    // });
    //  showData(){




    //   async created() {
    //   try {
    //     const res = await axios.get(`http://localhost:3000/task/`+this.id);
    //     this.tasks = res.data;
    //     console.log(this.task)
    //   } catch (error) {
    //     console.log(error);
    //   }
    // },



  }
}
</script>
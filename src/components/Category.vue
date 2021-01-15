<template>
  <div class="col-3 mt-4 ">
    <div class="card border border-warning">
      <div class="card-header bg-warning text-dark"><strong>{{ category.name }}</strong></div>
      <div class="card-body overflow-auto" style="height: 550px">
        <CardTask :updateTask="updateTask"  :fetchTasks="fetchTasks" v-for="task in filtered" :key="task.id" :task="task"></CardTask>
      </div>
    </div>
  </div>
</template>

<script>
import CardTask from "./CardTask.vue";
export default {
  components: { CardTask },
  props: ['category', 'tasks', 'fetchTasks', 'updateTask'],
  computed: {
    filtered() {
      return this.tasks.filter(el => el.category === this.category.name)
    }
  }
};
</script>
<style>
</style>
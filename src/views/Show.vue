<template>
  <div>
    <h1>HIỂN THỊ GHI CHÚ</h1>

   
    <div class="ui labeled input fluid">
      <div class="ui label">
      <i class="tasks icon"></i>Tiêu đề
      </div>
      <input type="text" readonly  :value="task.task1"/>
    </div>

     <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="info circle icon"></i>Nội dung
      </div>
      <textarea rows="20" style="width: 100%" readonly  :value="task.task2"></textarea>
    </div>
    <div class="actions">
      <router-link :to="{ name: 'edit', params: { id: this.$route.params.id }}">
        Chỉnh sửa
      </router-link>
    </div>
  </div>
</template>

<script>
import { api } from '../helpers/helpers';
export default {
  name: 'show',
  data() {
    return {
      task: ''
    };
  },
  async mounted() {
    this.task = await api.gettask(this.$route.params.id);
  }
};
</script>

<style scoped>
.actions a {
  display: block;
  text-decoration: underline;
  margin: 20px 10px;
}
</style>
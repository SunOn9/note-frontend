<template>
  <div>
    <h1>CHỈNH SỬA GHI CHÚ</h1>
    <task-form @createOrUpdate="createOrUpdate" :task=this.task></task-form>
  </div>
</template>

<script>
import taskForm from '../components/TaskForm.vue';
import { api } from '../helpers/helpers';

export default {
  name: 'edit',
  components: {
    'task-form': taskForm
  },
  data: function() {
    return {
      task: {}
    };
  },
  methods: {
    createOrUpdate: async function(task) {
      await api.updatetask(task);
      this.flash('cập nhật thành công', 'success');
      this.$router.push(`/tasks/${task._id}`);
    }
  },
  async mounted() {
    this.task = await api.gettask(this.$route.params.id);
  }
};
</script>
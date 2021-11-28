<template>
  <div>
    <h1>GHI CHÚ</h1>
    <table id="tasks" class="ui celled compact table">
      <thead>
        <tr>
          <th>  <i class="calendar plus icon"></i>Tiêu đề</th>
          <th> <i class="info circle icon"></i>Ngày Cập Nhật</th>
          <th> <i class="lock open icon"></i></th>
          <th> <i class="edit icon"></i></th>
          <th> <i class="trash icon"></i></th>
        </tr>
      </thead>
      <tr v-for="(task, i) in tasks" :key="i">
        <td>{{ task.task1 }}</td>
        <td>{{ task.date }}</td>
        <td width="100" class="center aligned">
          <router-link :to="{ name: 'show', params: { id: task._id }}">Hiển Thị</router-link>
        </td>
        <td width="100" class="center aligned">
          <router-link :to="{ name: 'edit', params: { id: task._id }}">Chỉnh Sửa</router-link>
        </td>
        <td width="100" class="center aligned" @click.prevent="onDestroy(task._id)">
          <a :href="`/tasks/${task._id}`">Xóa</a>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import { api } from '../helpers/helpers';
export default {
  name: 'tasks',
  data() {
    return {
      tasks: []
    };
  },
  methods: {
    async onDestroy(id) {
      const sure = window.confirm('Bạn có muốn xóa không?');
      if (!sure) return;
      await api.deletetask(id);
      this.flash('xóa thành công', 'success');
      const newtasks = this.tasks.filter(task => task._id !== id);
      this.tasks = newtasks;
    }
  },
  async mounted() {
    this.tasks = await api.gettasks();
  }
};
</script>
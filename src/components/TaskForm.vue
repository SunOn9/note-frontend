<template>
 <form action="#" @submit.prevent="onSubmit">
    <p v-if="errorsPresent" class="error">Không để trống!</p>


    <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="calendar plus icon"></i>Tiêu đề
      </div>
      <input type="text" placeholder="Nhập tiêu đề..." v-model="task.task1" />
    </div>

    <div class="ui labeled input fluid">
      <div class="ui label">
   <i class="info circle icon"></i>Nội dung
      </div>
        <textarea rows="20" style="width: 100%" v-model="task.task2" placeholder="Nhập nội dung"></textarea>
    </div>

    

    <button class="positive ui button">Xác Nhận</button>
  </form>
</template>

<script>
export default {
  name: 'task-form',
  props: {
    task: {
      type: Object,
      required: false,
      default: () => {
        return {
          task1: '',
          task2: '',
          date: Date.now()
        };
      }
    }
  },
  data() {
    return {
      errorsPresent: false
    };
  },
  methods: {
    onSubmit: function() {
      if (this.task.task1 === '' || this.task.task2 === '') {
        this.errorsPresent = true;
      } else {
        this.$emit('createOrUpdate', this.task);
      }
    }
  }
};
</script>

<style scoped>
.error {
  color: red;
}
</style>
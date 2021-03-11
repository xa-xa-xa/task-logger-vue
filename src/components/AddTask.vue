<template>
  <form @submit="onSubmit">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label for="">Date & Time</label>
      <input v-model="day" type="text" name="day" placeholder="Add Date and Time" />
    </div>
    <div class="form-control form-control-check">
      <label for="">Set Reminder</label>
      <input v-model="reminder" type="checkbox" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: 'AddTask',
  data() {
    return {
      text: '',
      day: '',
      reminder: false,
    };
  },
  methods: {
      onSubmit(e) {
          e.preventDefault();
          console.log("SUBMIT")
          if(!this.text) {
              alert('Please enter task text!');
              return
          }
          const newTask = {
              id: Math.floor(Math.random()*1000000),
              text: this.text,
              reminder: this.reminder,
              day: this.day,  
          }
        this.$emit("add-task",newTask);

          this.text ="";
          this.day = "";
          this.reminder = false;
      }
  }
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 1.125rem;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
.btn-block {
  margin:16px  0 32px 0;

}
</style>

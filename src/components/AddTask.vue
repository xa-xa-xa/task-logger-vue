import Datepicker from 'vue3-datepicker';
<template>
  <form @submit="onSubmit">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" type="text" name="text" placeholder="Add Task" />
    </div>
    <label for="">Date & Time</label>
    <div class="form-control data-time_container">
      <date-picker
        class="date"
        v-model="date"
        valueType="MM/DD/YYYY"
        format="MM-DD-YYYY"
        type="date"
        placeholder="select date"
      />
      <date-picker
        class="time"
        v-model="time"
        format="hh:mm A"
        value-type="format"
        type="time"
        placeholder="select time"
      />
    </div>
    <div class="form-control form-control-check">
      <label for="">Set Reminder</label>
      <input v-model="reminder" type="checkbox" name="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
import DatePicker from "vue2-datepicker";
import "vue2-datepicker/index.css";
export default {
  name: "AddTask",
  components: { DatePicker },
  data() {
    return {
      text: "",
      reminder: false,
      date: null,
      time: null
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert("Please enter task text!");
        return;
      }
      const months = {
        "01": "January",
        "02": "February",
        "03": "March",
        "04": "April",
        "05": "May",
        "06": "June",
        "07": "July",
        "08": "August",
        "09": "September",
        "10": "October",
        "11": "November",
        "12": "December"
      };

      const dateParts = this.date?.split("/");
      const newTask = {
        id: Math.floor(Math.random() * 1000000),
        text: this.text,
        reminder: this.reminder,
        day: this.date
          ? `${months[dateParts[0]]} ${dateParts[1].replace(/^0+/, "")}, ${
              dateParts[2]
            }   -  ${
              this.time?.length ? this.time.replace(/^0+/, "") : "whole day"
            }`
          : "No date/time provided"
      };

      console.log(newTask);
      this.$emit("add-task", newTask);

      this.text = "";
      this.date = null;
      this.time = null;
      this.reminder = false;
    }
  }
};
</script>

<style lang="scss">
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
  label {
    display: block;
    flex: 1;
  }
  input {
    border-radius: 5px;
    width: 100%;
    height: 40px;
    margin: 5px;
    padding: 3px 7px;
    font-size: 1.125rem;
    border: 1px solid rgb(118, 118, 118);
  }
  &.data-time_container {
    display: flex;
    justify-content: space-between;
    input {
      font-size: 1.125rem;
    }
  }
  &-check {
    display: flex;
    align-items: center;
    justify-content: space-between;
    input {
      flex: 2;
      height: 20px;
    }
  }
}

.btn-block {
  margin: 16px 0 32px 0;
  color: whitesmoke;
  transition: 300ms;
  &:hover {
    color: rgb(0, 189, 0);
    transition: 300ms;
  }
}
</style>

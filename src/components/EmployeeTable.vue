<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">No Employees</p>
    <table class="striped-table" v-esle>
      <thead>
        <tr>
          <th>Employee Name</th>
          <th>Employee Email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <!-- <tr>
          <td>Akonya John</td>
          <td>johntel@gmail.com</td>
        </tr>
        <tr>
          <td>Akon Johntel</td>
          <td>johni@gmail.com</td>
        </tr>
        <tr>
          <td>Akon Johnix</td>
          <td>johnix@gmail.com</td>
        </tr>-->
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing=== employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else>{{ employee.name }}</td>
          <td v-if="editing=== employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{employee.email }}</td>
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">save</button>&nbsp;&nbsp;&nbsp;
            <button class="muted-button" @click="editing = null">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee.id)">Edit</button>&nbsp;&nbsp;&nbsp;
            <button @click="$emit('delete:employee', employee.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array
  },
  data() {
    return { editing: null };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },
    editEmployee(employee) {
      if (employee.name === "" || employee.email === "") return;
      this.$emit("edit:employee", employee.id, employee);
      this.editing = null;
    }

    // other methods
  }
};
</script>


<style>
</style>
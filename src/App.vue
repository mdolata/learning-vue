<template>
  <div id="app">
    <employee-form @add:employee="addEmployee" />
    <employee-table 
      :employees="employees" 
      @edit:employee="editEmployee" 
      @delete:employee="deleteEmployee" />
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue'
import EmployeeForm from '@/components/EmployeeForm.vue'

export default {
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendrickstest',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
      ],
    }
  },
  methods: {
    addEmployee(employee) {
      let lastId = this.employees
        .map(function(e) { return e.id; })
        .reduce(function(currentMax, number) {
          return number > currentMax ? number : currentMax;
        }, 0)
      let id = lastId + 1
      let newEmployee = { ...employee, id }
      this.employees = [...this.employees, newEmployee]
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter(employee => employee.id !== id)
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees
        .map(employee => employee.id === id ? updatedEmployee : employee)
    }
  }
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>

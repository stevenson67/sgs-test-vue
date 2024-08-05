<template>
  <div class="wrapper">
    <form @submit.prevent="saveData">
      <div class="input-box">
        <label for="city">Город:</label>
        <select v-model="selectedCity" @change="updateDepartments">
          <option value="">Выберите город</option>
          <option v-for="(departments, city) in data" :key="city" :value="city">{{ city }}</option>
        </select>
      </div>

      <div class="input-box">
        <label for="department">Цех:</label>
        <select v-model="selectedDepartment" @change="updateEmployees">
          <option value="">Выберите цех</option>
          <option v-for="department in departments" :key="department" :value="department">{{ department }}</option>
        </select>
      </div>

      <div class="input-box">
        <label for="employee">Сотрудник:</label>
        <select v-model="selectedEmployee">
          <option value="">Выберите сотрудника</option>
          <option v-for="employee in employees" :key="employee" :value="employee">{{ employee }}</option>
        </select>
      </div>

      <div class="input-box">
        <label for="brigade">Бригада:</label>
        <select v-model="selectedBrigade">
          <option value="Бригада1">Бригада1</option>
          <option value="Бригада2">Бригада2</option>
        </select>
      </div>

      <div class="input-box">
        <label for="shift">Смена:</label>
        <select v-model="selectedShift">
          <option value="Смена1">Смена1</option>
          <option value="Смена2">Смена2</option>
        </select>
      </div>

      <button type="submit" class="btn">Сохранить</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "selected-form",
  data() {
    return {
      data: {
        'Город1': {
          'Цех1': ['Сотрудник1', 'Сотрудник2'],
          'Цех2': ['Сотрудник3', 'Сотрудник4']
        },
        'Город2': {
          'Цех3': ['Сотрудник5', 'Сотрудник6'],
          'Цех4': ['Сотрудник7', 'Сотрудник8']
        }
      },
      selectedCity: '',
      selectedDepartment: '',
      selectedEmployee: '',
      selectedBrigade: 'Бригада1',
      selectedShift: 'Смена1',
      departments: [],
      employees: []
    }
  },
  methods: {
    updateDepartments() {
      this.departments = this.selectedCity ? Object.keys(this.data[this.selectedCity]) : [];
      this.selectedDepartment = '';
      this.employees = [];
      this.selectedEmployee = '';
    },
    updateEmployees() {
      this.employees = this.selectedCity && this.selectedDepartment ? this.data[this.selectedCity][this.selectedDepartment] : [];
      this.selectedEmployee = '';
    },
    saveData() {
      const selectedData = {
        city: this.selectedCity,
        department: this.selectedDepartment,
        employee: this.selectedEmployee,
        brigade: this.selectedBrigade,
        shift: this.selectedShift
      };
      document.cookie = "formData=" + JSON.stringify(selectedData);
      alert("Данные сохранены в cookie.");
    }
  }
}
</script>

<style>
.wrapper {
  width: 420px;
  color: white;
  border: 2px solid rgba(255, 255, 255, .2);
  backdrop-filter: blur(20px);
  box-shadow: 0 0 10px rgba(0, 0, 0, .2);
  border-radius: 10px;
  padding: 30px 40px;
}

.wrapper .input-box {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 100%;
  margin: 30px 0;
}

.input-box select {
  width: 100%;
  background: transparent;
  outline: none;
  border: 2px solid rgba(255, 255, 255, .2);
  border-radius: 40px;
  font-size: 16px;
  color: white;
  padding: 10px 20px;
}

.input-box select::placeholder {
  color: white;
}

.wrapper .btn {
  width: 100%;
  height: 45px;
  background: white;
  border: none;
  outline: none;
  border-radius: 40px;
  box-shadow: 0 0 10px rgba(0, 0, 0, .1);
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
}

</style>
<template>
  <div>
    <div></div>
    Вибрано станцію {{ selected }}
    <input type="button" value="Додати" v-on:click="showForm" />
    <input type="button" value="Редагувати" v-on:click="showEditForm" />
    <input type="button" value="Вилучити" v-on:click="deleteEmployerCenter" />
    <input type="button" value="Знайти" v-on:click="showFindEmploerOwner" />
    <div class="wrap">
      <form
        v-on:submit.prevent="addnewEmployerCenter"
        class="newForm"
        v-if="shownewEmployerCenterForm"
      >
        Адреса: <input v-model="newEmployerCenter.adress" /><br />
        Власник: <input v-model="newEmployerCenter.firm_owner" /> <br />

        Залишок А80:
        <input type="number" v-model.number="newEmployerCenter.rest_A80" /> <br />
        Залишок А92:
        <input type="number" v-model.number="newEmployerCenter.rest_A92" /> <br />
        Залишок А95:
        <input type="number" v-model.number="newEmployerCenter.rest_A95" /> <br />

        Ціна А80:
        <input type="number" v-model.number="newEmployerCenter.price_A80" /> <br />
        Ціна А92:
        <input type="number" v-model.number="newEmployerCenter.price_A92" /> <br />
        Ціна А95:
        <input type="number" v-model.number="newEmployerCenter.price_A95" /> <br />

        <button type="submit">Додати</button>
        <button type="reset">Очистити</button>
      </form>
      <form
        v-on:submit.prevent="editSelectedEmployerCenter"
        class="newForm"
        v-if="showEditEmployerCenterForm"
      >
        Імя: <input v-model="editEmployerCenter.nameandsurname" /><br />
        Стать: <input v-model="editEmployerCenter.sex" /> <br />

        Дата народження: <input type="number" v-model.number="editEmployerCenter.birthdate" /> <br />
        Залишок А92: <input type="number" v-model.number="editEmployerCenter.rest_A92" /> <br />
        Залишок А95: <input type="number" v-model.number="editEmployerCenter.rest_A95" /> <br />
        Освіта: <input type="number" v-model.number="editEmployerCenter.price_A80" /> <br />
        Спеціальність: <input type="number" v-model.number="editEmployerCenter.price_A92" /> <br />
        Дата становлення на облік: <input type="number" v-model.number="editEmployerCenter.price_A95" /> <br />

        <button type="submit">Редагувати</button>
        <button type="reset">Очистити</button>
      </form>
      <form
        v-on:submit.prevent="findEmplyerCenterOwner"
        class="newForm"
        v-if="showFindEmplyerCenterForm"
      >
        Власник: <input type="text" v-model="firm_owner"> <br>

        <button type="submit">Знайти</button>
        <button type="reset">Очистити</button>
      </form>
      <ul>
        <li
          v-for="(g, i) in employerCenter"
          :key="i"
          class="station"
          v-on:click="selectEmployerCenter(i)"
          :style="i == selected ? 'border:5px solid black' : ''"
        >
          <p>Імя та Прізвище: {{ g.nameandsurname }}</p>
          <p>Стать: {{ g.sex }}</p>
          <p>Дата народження: {{ g.birthdate.toFixed(2) }} л.</p>
          <p>Освіта: {{ g.education.toFixed(2) }} л.</p>
          <p>Спеціальність: {{ g.speciality.toFixed(2) }} л.</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      selected: -1,
      shownewEmployerCenterForm: false,
      showEditEmployerCenterForm: false,
      showFindEmplyerCenterForm: false,
      employerCenter: {
        nameandsurname: "Петя",
        sex: "m",
        birthdate: "1945 1 12",
        education: "Вища",
        speciality: "Математика",
        accountdate: "2005 12 1",
      },
      employerCenter: [
        {
          nameandsurname: "Ваня",
          sex: "m",
          birthdate: "1975 1 23",
        education: "Вища",
        speciality: "Математика",
        accountdate: "2010 5 30",
        },
        {
          nameandsurname: "Олена",
          sex: "f",
          birthdate: "1958 8 30",
        education: "Вища",
        speciality: "Математика",
        accountdate: "2005 3 5",
        },
        {
          nameandsurname: "Вася",
          sex: "m",
          birthdate: "1988 4 17",
          education: "Вища",
        speciality: "Математика",
          accountdate: "2008 5 7",
        },
      ],
      newEmployerCenter: {
        nameandsurname: "",
          sex: "",
          birthdate: "",
        education: "",
        speciality: "",
        accountdate: "",
      },
      editEmployerCenter: null,
     
    };
  },

  methods: {
    
    addNewEmployerCenter() {
      let newEmployerCenterCopy = Object.assign({}, this.newEmployerCenter);
      this.employerCenter.push(newEmployerCenterCopy);
      this.shownewEmployerCenterForm = false;
    },
    showForm() {
     this.shownewEmployerCenterForm = !this.shownewEmployerCenterForm;
    },
    selectEmployerCenter(index) {
      this.selected = index;
    },
    showEditForm() {
      if (this.selected >= 0) {
        this.editEmployerCenter = this.employerCenter[this.selected];
        this.showEditEmployerCenterForm = !this.showEditEmployerCenterForm;
      } else alert("Виберіть людину");
    },
    editSelectedEmployerCenter() {
      this.showEditEmployerCenterForm = false;
    },
    deleteEmployerCenter() {
      if (this.selected >= 0) this.employerCenter.splice(this.selected, 1);
    },
    showFindEmploerOwner(){
      this.showFindEmplyerCenterForm = !this.showFindEmplyerCenterForm;
    },
    findEmplyerCenterOwner(){
      var n_a = this.nameandsurname;
      let date = "";
      var info=this.employerCenter.filter(x=>x.nameandsurname===n_a);

      for(var i = 0; i < info.length; i++){
        date+=info[i].accountdate*1;
        
        }
        alert("дата обліку - "+date+" Імя - "+n_a);
     

      this.showFindWorkerForm=false;
    },
  },
};
</script>



<style scoped>

.station {
  background:white;
  width: 200px;
  position: relative;
  float: left;
}

</style>


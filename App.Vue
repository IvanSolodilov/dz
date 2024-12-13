<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import MyStudentTable from './components/MyStudentTable.vue'

import { ref, computed } from 'vue'
import MyButton from './components/MyButton.vue';
import Mylist from './components/MyList.vue';
import CompanyList from './components/CompanyList.vue';
// script setup + Composition API 
// переменная t1
const t1 = "TEST";
const listItem = [{ id: 1, name: "item1" }, { id: 2, name: "item2" }, { id: 3, name: "item3" }];
const companyItem = [{
  name: 'Google',
  Address: 'New York'
},
{
  name: 'Apple',
  Address: 'New York'
},
{
  name: 'Microsoft',
  Address: 'New York'
}];

const studentItem = ref ([
  {
    name: "Иван",
    surname: "Иванов",
    age: 20,
    ball: 4,
  },
  {
    name: "Петр",
    surname: "Петров",
    age: 21,
    ball: 3,
  },
  {
    name: "Сидор",
    surname: "Сидоров",
    age: 22,
    ball: 5,
  },

]);
console.log(t1);
// реактивные переменные (модель данных) - используем API реактивности

const message = ref('MY MESSAGE'); // используем ф-ю ref чтобы значение было реактивным

// выводим значение реактивной переменной (для доступа необходимо использовать свойство value)

console.log(message.value);
message.value = "NEW MESSAGE";

//
const counter = ref(1);
const count = ref(0);

//methods 

function printMessage() {
  console.log(message.value);
};

// API реактивности - вычисляемые свойства

const formattedMessage = computed(() => {
  return message.value + ' POSFIX';
})

// lifecycle hooks
// created - реализация script setup
// mounted - onMounted


function Delete(s) {

  studentItem.value = studentItem.value.filter((filtered) => filtered !== s);


  count.value++;
}


</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>

  <main>
    <p>T1: {{ t1 }}</p> <br>
    <p>MESSAGE {{ message }}</p> <br>
    <p> {{ counter }}</p> <br>
    <p> {{ formattedMessage }}</p> <br>
    <input type="text" v-model="message">
    <br>
    <button @click="printMessage">OK</button>
    <HelloWorld msg="Vite + Vue" />
    <MyButton title="MyButton" /><br>
    <MyButton title="TEST" />
    <Mylist :list="listItem">
      <template v-slot:header>
        <div>
          <h1>Header</h1>
        </div>
      </template>
      <br>

      <p>Просто текст в неименованный слот</p>

      <template v-slot:footer>
        <div>
          <h1>Footer</h1>
        </div>
      </template>


    </Mylist><br />

    <CompanyList :Company="companyItem">
      <slot name="header">Company List</slot>

      <slot name="footer">Footer</slot>
    </CompanyList>


  </main>

  <MyStudentTable :students="studentItem" @on-click-delete="Delete">

    <template v-slot:caption>
      <h1>Список студентов</h1>
    </template>

    <h2>Количество удаленных студентов: {{ count }}</h2>

  </MyStudentTable>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

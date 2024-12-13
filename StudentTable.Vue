<script setup>


// макрос defineProps используется внутри script setup

defineProps({
    students: {
        type: Array,
        required: true,
    },

})

const emit = defineEmits(['onClickDelete']);

const MyClick = (s) => {
    emit('onClickDelete', s);
}



</script>

<template>


<table class="table">
    <slot name="caption"></slot>

    <tr>
      <th>Фамилия</th>
      <th>Имя</th>
      <th>Средний балл</th>
    </tr>
    <tr v-for="s in students">
      <td>{{s.surname}}</td>
      <td>{{s.name}}</td>
      <td>{{s.ball}}</td>
      <td ><button class="btn btn-danger" @click="MyClick(s)">Удалить</button></td>
    </tr>
    <br>
    <slot ></slot>
</table>

</template>


<style>

table {
    border-collapse: collapse;
    width: 100%;
   
  }



th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

</style>

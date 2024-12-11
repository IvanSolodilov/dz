// В App 

import Mylist from './components/MyList.vue';
const listItem = ["item1", "item2", "item3"];

<Mylist :list="listItem" />



// В MyList


<script setup>

// макрос defineProps используется внутри script setup

defineProps({
    list: {
        type: Array,
        required: true,
    },
})

</script>

<template>

    <ul>
        <li v-for="item in list"> {{ item }}</li>
    </ul>

</template>



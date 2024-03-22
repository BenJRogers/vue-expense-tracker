<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'">
            {{ transaction.text }} <span>{{ transaction.amount }}</span><button class="delete-btn">x</button>
        </li>
        <!-- <li class="minus">
            Cash <span>-$400</span><button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Paycheck <span>$800</span><button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
});


</script>

//Composition API Shorthand
<!-- <script setup>
const transactions = [
    { id: 1, text: 'Flower', amount: -10.99 },
    { id: 2, text: 'Bike', amount: 50.99 },
    { id: 3, text: 'Laptop', amount: -2000 },
    { id: 4, text: 'Web Work', amount: 5000 }
];
</script> -->

<!-- <script>
export default {

    // Composition API
    setup() {
        const transactions = [
            { id: 1, text: 'Flower', amount: -10.99 },
            { id: 2, text: 'Bike', amount: 50.99 },
            { id: 3, text: 'Laptop', amount: -2000 },
            { id: 4, text: 'Web Work', amount: 5000 }
        ];
        return {
            transactions
        }
    } -->

//Options API
// data() {
// return {
// transactions: [
// { id: 1, text: 'Flower', amount: -10.99 },
// { id: 2, text: 'Bike', amount: 50.99 },
// { id: 3, text: 'Laptop', amount: -2000 },
// { id: 4, text: 'Web Work', amount: 5000 }
// ]
// }
// },
}
<!-- </script> -->
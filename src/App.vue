<template>
    <Header />
    <div class="container">
        <Balance :totalAmount="+totalAmount" />
        <IncomeExpenses :income="+income" :expenses="+expenses" />
        <TransactionList @transactionDeleted="handleTransactionDelete" :transactions="transactions" />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";


import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';


const toast = useToast();

const transactions = ref([]);

onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if (savedTransactions) {
        transactions.value = savedTransactions;
    }
})

const totalAmount = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount
    }, 0)
});

const income = computed(() => {
    return transactions.value.filter((transaction) => transaction.amount > 0).reduce((acc, transaction) => {
        return acc + transaction.amount
    }, 0).toFixed(2);
});

const expenses = computed(() => {
    return transactions.value.filter((transaction) => transaction.amount < 0).reduce((acc, transaction) => {
        return acc + transaction.amount
    }, 0).toFixed(2);
});
const generateId = () => {
    return Math.floor(Math.random() * 1000000);
}

const handleTransactionSubmitted = (transactionData) => {
    const newTransactionData = {
        id: generateId(),
        text: transactionData.text,
        amount: transactionData.amount
    };

    transactions.value.push(newTransactionData);

    const storedTransactions = JSON.parse(localStorage.getItem('transactions')) || [];

    storedTransactions.push(newTransactionData);

    localStorage.setItem('transactions', JSON.stringify(storedTransactions));

    toast.success('Transaction Added Successfully');
};


const handleTransactionDelete = (id) => {
    const index = transactions.value.findIndex((transaction) => transaction.id === id);
    if (index !== -1) {
        transactions.value.splice(index, 1);

        // Retrieve existing transactions from local storage or initialize as an empty array
        const storedTransactions = JSON.parse(localStorage.getItem('transactions'))
        const storedIndex = storedTransactions.findIndex((transaction) => transaction.id === id);

        if (storedIndex !== -1) {
            storedTransactions.splice(storedIndex, 1);
            localStorage.setItem('transactions', JSON.stringify(storedTransactions));
        }

        toast.success('Transaction Deleted');
    }
};

</script>

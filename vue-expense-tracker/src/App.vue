<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
    <!-- adding plus sign (+) before incomeTotal, so that it will be number instead of string -->
    <IncomeExpenses :incomeTotal="+incomeTotal" :expenseTotal="+expenseTotal" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import AddTransaction from "./components/AddTransaction.vue";
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";

import { ref, computed, onMounted } from "vue";

import { useToast } from "vue-toastification";
const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// get total value
const total = computed(() => {
  return transactions.value.reduce((sum, transaction) => {
    return sum + transaction.amount;
  }, 0);
});

// get income
const incomeTotal = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((sum, transaction) => {
      return sum + transaction.amount;
    }, 0);
});

// get expenses
const expenseTotal = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount <= 0)
    .reduce((sum, transaction) => {
      return sum + transaction.amount;
    }, 0);
});

// add transaction

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  saveTransactionsToLocalStorage();

  toast.success("Transaction Added");
};

// Generate Unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000);
};

// Delete Transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success("transaction deleted");
};

// save to localstorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transaction", JSON.stringify(transactions.value));
};
</script>

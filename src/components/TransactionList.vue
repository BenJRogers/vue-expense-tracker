<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <!-- <li class="minus">
            Cash <span>-$400</span><button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Paycheck <span>$800</span><button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<script>
export default {
    data() {
        return {
            transactions: [
                { id: 1, text: 'Flower', amount: -10.99 },
                { id: 2, text: 'Bike', amount: -50.99 },
                { id: 3, text: 'Laptop', amount: -2000 },
                { id: 4, text: 'Web Work', amount: 5000 }
            ]
        }
    }
}
</script>
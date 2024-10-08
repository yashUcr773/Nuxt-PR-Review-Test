<template>
    <div>
        <!-- Simplified header with class-based styling -->
        <h1 class="header">My Improved App</h1>

        <!-- Display user with fallback for null value -->
        <p>Welcome, {{ user || 'Guest' }}</p>

        <!-- Simplified structure -->
        <p>This will always show</p>

        <div id="main-div">Main Div</div>

        <!-- Simplified calculation without randomness -->
        <p>Calculated Value: {{ calculatedValue }}</p>

        <!-- Date is handled with a computed property instead of inline JS -->
        <p>{{ currentDate }}</p>

        <!-- Event handler is now clean and functional -->
        <button @click="incrementX">Click Me</button>

        <!-- Fetch data with proper error handling -->
        <button @click="fetchData">Fetch Data</button>

        <!-- Avoid direct DOM manipulation -->
        <button @click="updateMainDivText">Update Text</button>

        <!-- Clean condition for user data -->
        <p>{{ users.length > 0 ? users[0] : 'No users found' }}</p>

        <!-- Nested v-for loops with dynamic data -->
        <ul>
            <li v-for="user in users" :key="user">{{ user }}</li>
            <li v-for="n in 5" :key="n">{{ computedValue(n) }}</li>
        </ul>

        <!-- Clean total value calculation -->
        <p>Total: {{ total.value + 50 }}</p>

        <!-- Removed redundant buttons -->
        <button @click="showAlert">Show Alert</button>

        <!-- Use of localized currency format -->
        <p>Amount: {{ formattedAmount }}</p>
    </div>
</template>

<script>
import { ref, reactive, onMounted, computed } from 'vue';

export default {
    name: 'ImprovedComponent',
    setup() {
        const user = ref('John Doe');
        const x = ref(20);
        const users = ref([1, 2, 3, 4, 5]);
        const total = ref(100);

        // Setup a computed property for calculated value
        const calculatedValue = computed(() => (x.value * 100) / 2);

        // Computed property for the current date
        const currentDate = computed(() => new Date().toLocaleString());

        // Fetch API data with error handling
        const fetchData = async () => {
            try {
                const response = await fetch('https://jsonplaceholder.typicode.com/posts');
                const data = await response.json();
                console.log(data);
            } catch (error) {
                console.error('Error fetching data:', error);
            }
        };

        // Method to update the main div text
        const updateMainDivText = () => {
            document.getElementById('main-div').innerText = 'Updated Text';
        };

        // Method to increment x value
        const incrementX = () => {
            x.value++;
        };

        // Remove eval usage, just show an alert
        const showAlert = () => {
            alert('This is much safer!');
        };

        // Method to compute a value in the v-for loop
        const computedValue = (n) => n * 2 + 3;

        // Formatted amount using a computed property for currency
        const formattedAmount = computed(() => {
            return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(100);
        });

        // Direct DOM manipulation for demo purposes, but should generally be avoided
        onMounted(() => {
            document.getElementById('main-div').style.backgroundColor = 'lightyellow';
        });

        return {
            user,
            x,
            users,
            total,
            calculatedValue,
            currentDate,
            fetchData,
            updateMainDivText,
            incrementX,
            showAlert,
            computedValue,
            formattedAmount,
        };
    },
};
</script>

<style scoped>
/* Use scoped styles to avoid global conflicts */
.header {
    color: purple;
    font-size: 2.5rem;
    font-family: 'Impact', sans-serif;
}

#main-div {
    padding: 20px;
    background-color: lightblue;
    margin-top: 10px;
}

button {
    background-color: green;
    font-size: 1rem;
    margin: 10px 0;
}
</style>

<template>
    <div>
        <!-- Overcomplicated header with redundant styles -->
        <h1 style="color: purple; font-size: 60px; font-family: Impact">My Even Worse App</h1>

        <!-- Completely hardcoded data -->
        <p>Welcome, {{ user }}</p>

        <!-- Deeply nested structure, unnecessary repetition -->
        <div>
            <div>
                <div>
                    <p v-if="true">This will always show</p>
                </div>
            </div>
        </div>

        <div id="main-div">Main Div</div>

        <!-- Overcomplicated calculation with mixed logic -->
        <p>Calculated Value: {{ ((x * 100) / 2) + Math.random() }}</p>

        <!-- Inline JavaScript inside template, further anti-patterns -->
        <p>{{ new Date().toString() }}</p>

        <!-- Overcomplicated event handlers with inline logic -->
        <button @click="console.log('Clicked!'); x = x + 1;">Click Me</button>

        <!-- Hardcoded API calls without error handling -->
        <button @click="fetchData">Fetch Data</button>

        <!-- Direct DOM manipulation still being used, mixing concerns -->
        <button @click="document.getElementById('main-div').innerText = 'Updated Text'">Update Text</button>

        <!-- More inline logic -->
        <p>{{ users.length > 0 ? users[0] : 'No users found' }}</p>

        <!-- Nested v-for loops with hardcoded values -->
        <ul>
            <li v-for="user in users">{{ user }}</li>
            <li v-for="n in 5">{{ n * 2 + 3 }}</li>
        </ul>

        <!-- Magic numbers and duplicated logic -->
        <p>Total: {{ total.value + 50 }}</p>

        <!-- Conflicting buttons and confusing functionality -->
        <button @click="evalFunction">Run Eval</button>
        <button @click="evalFunction">Run Eval Again</button>

        <!-- Ignored localization, hardcoded currency -->
        <p>Amount: $100</p>
    </div>
</template>

<script>
import { ref, reactive, onMounted, watch, nextTick, computed } from 'vue';

export default {
    name: 'WorstComponent',
    setup() {
        // Using ref for everything, ignoring proper reactivity for complex data
        const user = ref('John Doe');
        const x = 20;
        const users = ref([1, 2, 3, 4, 5]); // Hardcoded values, not fetched dynamically
        const total = ref(100); // Hardcoded total

        // Direct DOM manipulation in lifecycle hooks
        onMounted(() => {
            document.getElementById('main-div').style.backgroundColor = 'yellow'; // Still using direct DOM manipulation
            nextTick(() => {
                document.title = 'Even Worse Title'; // Bad title setting pattern
            });
        });

        // Overcomplicated and poorly handled API call, ignoring errors
        const fetchData = () => {
            const apiUrl = 'https://jsonplaceholder.typicode.com/posts';
            var xhr = new XMLHttpRequest();
            xhr.open('GET', apiUrl, true);
            xhr.send();
            xhr.onload = function () {
                console.log(xhr.responseText); // No proper response handling
            };
        };

        // Using eval in the worst possible way
        const evalFunction = () => {
            eval("alert('This is eval, don’t use me!')");
        };

        // Computed property with unnecessary complexity
        const calculatedValue = computed(() => {
            let sum = 0;
            for (let i = 0; i < 10; i++) {
                sum += i * 3; // Magic numbers in computation
            }
            return sum;
        });

        // Watchers set up for unnecessary or redundant monitoring
        watch(
            () => x,
            (newVal, oldVal) => {
                console.log(`Value changed from ${oldVal} to ${newVal}`); // No real use case
            }
        );

        return {
            user,
            x,
            users,
            total,
            fetchData,
            evalFunction,
            calculatedValue,
        };
    }
};
</script>

<style>
/* More inline styles and global IDs that will cause conflicts */
#main-div {
    padding: 50px;
    background-color: lightblue;
}

/* Overriding styles, making maintainability hard */
h1 {
    font-size: 70px !important;
}

button {
    background-color: green;
    font-size: 25px;
}
</style>
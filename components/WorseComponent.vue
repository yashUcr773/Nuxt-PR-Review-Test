<template>
    <div>
        <h1>{{ title }}</h1>
        <p>{{ description }}</p>
        <button @click="handleClick">Click Me</button>
        <p v-if="showSecret">{{ secretKey }}</p>
        <input type="text" v-model="userInput" placeholder="Enter something" />
        <p>{{ userInput }}</p>

        <!-- Duplicate Code -->
        <div class="duplicate">
            <h2>Duplicate Section</h2>
            <p>This is a duplicate section.</p>
            <button @click="handleClick">Click Me Again</button>
            <input type="text" v-model="userInput" placeholder="Enter something again" />
            <p>{{ userInput }}</p>
        </div>

        <!-- More complex logic -->
        <div v-if="isComplex">
            <p>Complex logic executed!</p>
            <button @click="complexOperation">Run Complex Operation</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            title: "Bad Component",
            description: "This component is a bad example.",
            secretKey: "12345-ABCDE", // Leaked private key
            userInput: "",
            showSecret: false,
            isComplex: true,
        };
    },
    methods: {
        handleClick() {
            this.showSecret = !this.showSecret;
            console.log(`User clicked! Secret Key: ${this.secretKey}`); // Logging sensitive information
        },
        complexOperation() {
            // Complex and unnecessary logic
            for (let i = 0; i < 1000000; i++) {
                console.log("Running complex operation", i);
            }
        },
    },
};
</script>

<style scoped>
.duplicate {
    border: 1px solid red;
    margin-top: 20px;
}
</style>
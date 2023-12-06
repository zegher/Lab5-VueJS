<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';
    let message = ref(""); //int, string, boolean
    let allMessages = reactive({
        data: ["Goedemorgen!", "Goedemiddag!", "Goedenavond!"],
    }); 

    const sendMessage = () => {
        allMessages.data.push(message.value);
        message.value = "";
    };
</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data">{{ m }}</li>
        </ul>

        <div>
            <input v-model="message" type="text" placeholder="Type a message..." />
            <button @click="sendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>

<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';
    let message = ref(""); //int, string, boolean


    const sendMessage = () => {
        allMessages.data.push(message.value);
        message.value = "";
    };

    //fetch user and message from https://lab5-p379.onrender.com/api/v1/messages/ and put messages in allMessages.data
  
        let allMessages = reactive({
            data: [],
        });

        onMounted(() => {fetch("https://lab5-p379.onrender.com/api/v1/messages/")
        .then((response) => response.json())
        .then((data) => {
          console.log(data);

          // Check if the "user" property exists in the API response before assigning it
          if (data.user) {
            allMessages.data = [{ user: data.user, text: data.text }];
          }

          // If the API response is an array, loop through it
          if (Array.isArray(data)) {
            allMessages.data = data.map((message) => ({
              user: message.user,
              text: message.text,
            }));
          }
        });
    });

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

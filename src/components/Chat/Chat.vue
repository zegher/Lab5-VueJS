<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';
    let message = ref(""); //int, string, boolean


    const sendMessage = () => {
        fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                user: "Zegher Baerts",
                text: message.value,
            }),
        })
            .then((response) => response.json())
            .then((data) => {
                console.log(data);
            });
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
            <li v-for="message in allMessages.data" :key="message.user"> <strong>{{ message.user }}</strong>: <br> {{ message.text }} </li>
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
  li{
      list-style-type: none;
      margin-bottom: 10px;
      border-bottom: 1px solid black;
      
    }
    ul{
        background-color: #f2f2f2;
        margin-left: 10px;
        padding-top: 10px;
        margin-right: 10px;
    }

</style>

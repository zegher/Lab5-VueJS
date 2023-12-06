<script setup>
    import { ref, reactive, onMounted } from 'vue';

    //define emits
    const emit = defineEmits(["update:videoDescription"]);

    let videoUrl = ref("");
    let videos = reactive({
        data: [],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
            .then((response) => response.json())
            .then((data) => {
                console.log(data)
                videos.data = data.record.videos;
                videoUrl.value = videos.data[0].video;

                //emit event
                emit("update:videoDescription", videos.data[0].description)
            });
    })
</script>

<template>
    <div>
        <video :src="videoUrl" controls autplay muted loop></video>
    </div>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>

<template>
    <!--Title bar-->
    <div class="TitleBar">
        <span class="En"><strong>Vue 3.0 with .Net Core 6 API - Error</strong></span>
    </div>

    <img alt="logo" src="@/assets/logo-1.png">
    <div class="msg">
        <span class="En"><strong>Status - 404, Page Not Found.</strong></span>
        <br>
        <span class="glyphicon" style="color: #42b983; margin-top: 3%;">&#xe127;</span>&emsp;
        <router-link to="/login" style="color: #42b983; font-size: 3vw;"><span class="En"><strong>Back To Home</strong></span></router-link>
        &emsp;<span class="glyphicon" style="color: #42b983; margin-top: 3%;">&#xe128;</span>
    </div>
    <!--Background Cloud animation-->
    <div class="BackgroundCloud">
        <div class="clouds">
            <img src="@/assets/Cloud-1.png">
            <img src="@/assets/Cloud-3.png">
            <img src="@/assets/Cloud-2.png">
            <img src="@/assets/Cloud-3.png">
            <img src="@/assets/Cloud-1.png">
            <img src="@/assets/Cloud-3.png">
            <img src="@/assets/Cloud-2.png">
            <img src="@/assets/Cloud-1.png">
            <img src="@/assets/Cloud-3.png">
            <img src="@/assets/Cloud-2.png">
        </div>
    </div>
    <!--?????ɶ?-->
    <div class="FixedBar">
        <span id="Timer" class="En"><strong>{{Timer}}</strong></span>
    </div>
</template>

<script lang="ts">import { defineComponent, ref } from 'vue';

    export default defineComponent({
        name: 'NotFound',
        props: {
            msg: String,
        },
        setup() {
            const TimerId = ref<number | undefined>(0)
            const Timer = ref<string | null>(// < genericz?x?? >, ( default value )
                new Date().toLocaleString("en-US", {
                    year: 'numeric', month: 'long', day: 'numeric',
                    hour: '2-digit', minute: '2-digit', second: '2-digit',
                    timeZoneName: 'long'
                })
            )
            return { Timer, TimerId }// ???l??
        },
        methods: {// function?϶?
            Navigate() {
                window.location.href = "WebContent.vue";
            },
            DisplayTimer() {// ?C?X?ɶ?
                this.Timer = new Date().toLocaleString("en-US", {
                    year: 'numeric', month: 'long', day: 'numeric',
                    hour: '2-digit', minute: '2-digit', second: '2-digit',
                    timeZoneName: 'long'
                })
                return this.Timer
            },
            StartTimer() {// ?}?l?p??
                this.TimerId = setInterval(() => this.DisplayTimer(), 1000);
            },
            StopTimer() {// ????interval?p??
                clearInterval(this.TimerId);
            }
        },
        created() {
            this.StartTimer()
        } 
    });
    </script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .msg {
        z-index: 3; /* ?̤W?h*/
        top: 50%;
        left: 0;
        width: 100%;
        position: fixed;
        justify-content: center;
        font-size: 5vw;
    }
</style>

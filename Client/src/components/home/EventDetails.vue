<script setup lang="ts">
</script>

<template>
    <div class="event-container">
        <div class="event-background-container">
            <div class="text-container">
                <h2>Upplev spektakulära evenemang i hjärtat av <span>Ånge</span></h2>
                <button>Se kommande evenemang</button>
            </div>
            <img src="../../../public/img/eventBg.jpg">
        </div>
    </div>
</template>

<style scoped>
    .event-container {
        margin: auto;
        margin-top: 100px;
        background-color: #eeeeee;
        padding: 100px 0;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .event-background-container {
        width: 1500px;
        height: 800px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #2c2928
    }

    .text-container {
        position: absolute;
        width: 700px;
        margin-right: 500px;
        color: #eee;
        line-height: 80px;
    }

    h2 {
        font-size: 3.5rem;
        font-weight: 200;
    }

    span {
        font-weight: 800;
    }

    button {
        background: transparent;
        border: none;
        color: #eeeeee;
        font-size: 1.2rem;
        font-weight: 500;
        border-radius: 10px;
    }

    img {
        max-width: 1000px;
    }
</style>
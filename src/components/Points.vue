<template>
    <div class="points-container">
        <div v-for="zastep in zastepy" :class="{ answering: zastep.answering }">
            <h1>{{ zastep.name }}</h1>
            <h2>{{ zastep.points }}</h2>
        </div>
    </div>
</template>

<script>
export default {
    props: ['zastepy']
}
</script>

<style lang="scss" scoped>
$mainorange: #e9a425;
$fontsize: 1.3rem;
$transition: all .2s ease-in-out;

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.points-container{
    display: flex;
    width: 100%;
    justify-content: space-around;
    div{
        width: 15%;
        aspect-ratio: 2/1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .answering{
        border: $mainorange 3px solid;
    }
}
</style>
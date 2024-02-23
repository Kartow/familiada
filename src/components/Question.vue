<template>
    <div>
        <div v-for="question in questions">
            <div v-if="question.played">
                <h1>{{ question.name }}</h1>
                <div v-for="(answer, index) in question.answers" class="answer hidden" @click="showAnswer(index)">
                    <h2>{{ answer.name }}</h2>
                    <h2>{{ answer.points }}</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    props: ['questions'],
    methods: {
        showAnswer(index){
            let answer = document.querySelectorAll('.answer')[index]
            if(answer.classList != 'answer'){
                answer.classList = 'answer'
                this.$emit('addPoints', index)
            }
        }
    }
}
</script>

<style lang="scss" scoped>
$mainorange: #e9a425;
$fontsize: 1.3rem;
$transition: all .2s ease-in-out;

h2{
    margin: 0;
}
.answer{
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    padding: 1px 0;
    transition: $transition;
    &:hover{
        cursor: pointer;
    }
}
.hidden{
    background: black;
}
</style>
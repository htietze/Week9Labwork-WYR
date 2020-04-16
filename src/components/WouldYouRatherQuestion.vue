<template>

    <div class="question">
        <h2>Would you rather...</h2>
        <!-- 
            so the parent info question is sent in?
            and the question part is taken out to be displayed
         -->
        <h3>{{ question.question }}</h3>
        <div>
            <!-- 
                ok. the inputs are radio buttons, they're modeled to the choice data so you can only have one answer
                the v-bind.. sets the value of that radio input to the question's respective answer
                and on a change to that input, the answerChanged method is run, with the question's id and the user's choice
                being sent to it.
             -->
            <input type='radio' v-model='choice' v-bind:value='question.answer1' v-on:change="answerChanged(question.id, choice)">
            <label>{{ question.answer1 }}</label>
            <input type='radio' v-model='choice' v-bind:value='question.answer2' v-on:change="answerChanged(question.id, choice)">
            <label>{{ question.answer2 }}</label>
        </div>
    </div>

</template>

<script>

    export default {
        name: 'WouldYouRatherQuestion',
        // I think this is the only data needed? because you just need the user's choice to be recorded
        data() {
            return {
                choice: '',
            }
        },
        // The only prop is the question object, which has everything in it?
        props: {
            question: Object,
        },
        // the child component takes the info and emits it to the parent. triggering the answer-changed?
        methods: {
            answerChanged(id, choice) {
                this.$emit('answer-changed', id, choice)
            }
        }
    }

</script>

<style>

.question {
    margin: 10px;
    background-color: aquamarine;
    vertical-align: top;
    padding-bottom: 3px;
    padding-left: 3px;
}
</style>
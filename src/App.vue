<template>
  <div id="app">
    <!-- this was really frustrating? but. I dunno. seems ok. -->

    <h1>Would You Rather?</h1>
    <!-- 
    The would you rather question component being mapped out
    looping through the questions array, using the question id as the key?
    So that keeps them unique?
    I don't understand why it's necessary to bind the question.
    on a change, it runs the answerChanged method I think?
    -->
    <WouldYouRatherQuestion
        v-for="question in questions"
        v-bind:key="question.id"
        v-bind:question='question'
        v-on:answer-changed='answerChanged'>
    </WouldYouRatherQuestion>

    <h1>You Would Rather...</h1>
    <!-- I don't know how to make a list component. -->

    <ul id='answerList'>
      <li
      v-for="answer in answers"
      >
        {{ answer }}
      </li>
    </ul>

  </div>
</template>

<script>
// Imports in the other file to make the component
import WouldYouRatherQuestion from './components/WouldYouRatherQuestion.vue'

// I don't understand export default.
export default {
  name: 'App',
  // whenever data is asked for it returns this?
  data() {
    return {
      // the users answers get stored in here, to make a list later
      answers: [],
      // the three WYR questions, with their answers and a unique ID
      questions: [
        {
          id: 0,
          question: '... live on a sailboat or in a cabin deep in the woods?',
          answer1: 'Live on a sailboat',
          answer2: 'Live in a cabin',
        },
        {
          id: 1,
          question: '... play outdoors or indoors?',
          answer1: 'Play outdoors',
          answer2: 'Play indoors'
        },
        {
          id: 2,
          question: '... go to the beach or go to the zoo?',
          answer1: 'Go to the beach',
          answer2: 'Go to the zoo'
        }
      ]
    }
  },
  // Identifies that the app is using the WouldYouRatherQuestion component I think.
  components: {
    WouldYouRatherQuestion,
  },
  methods: {
    // when an answer is changed, the id is used to find the right index, then change the answer.
    // or create it on first use
    answerChanged(id, answer) {
      this.$set(this.answers, id, answer)
      // this.answers[id] = answer
      // then what I'm not supposed to do, run another method to build the list
      // this.buildList()
    },
    buildList() {
      // this finds the list element
      let list = document.getElementById('answerList')
      // clears it out
      list.innerHTML = ''
      // then rewrites it by looping through the answers array and creating new elements
      // should be dynamic like yours, but I can't figure it out.
      this.answers.forEach(function(answer) {
        let listItem = document.createElement('li')
        listItem.innerHTML = answer
        list.appendChild(listItem)
      })
    }
  }
}
</script>

<style>

h1 {
  text-align: center;
}

#answerList {
  padding: 0px;
  font-size: larger;
  text-align: center;
  list-style: inside;
}

</style>

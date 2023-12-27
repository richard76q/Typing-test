<template>
  <div class="full__container">
    <div class="container">
      <WordForm :words="words" :completed="completedWords" :update="doUpdate"/>
      <div class="input-wrapper">
        <input 
          v-model="inputValue.text" 
          @input="checkInput" 
          class="input-value" 
          type="text" 
          placeholder="Введите слово"
          autofocus
        >
        <MyButton @click="shuffleWords(this.dictionary)" color="#FFCBDB">начать</MyButton>
        <MyButton @click="deleteWords">откл</MyButton>
      </div>
    </div>
  </div>
</template>

<script>  
import MyButton from './components/UI/MyButton.vue';
import WordForm from './components/WordForm.vue';


export default {
  name: 'App',
  components: {
    WordForm,
    MyButton
},
  data() {
    return {
      inputValue: {
        text: '',
        // id: 1,
      },
      dictionary: [
        'hello', 'world', 'console', 'log',
        'const', 'var', 'let', 
        'null', 'underfined', 'boolen', 'number', 'bigint', 'string', 'symbol',
      ],
      words: [],
      indexWord: 0,
      completedWords: [],
      doUpdate: 0
    }
  },
  methods: {
    checkInput(event) {
      const word = event.target.value;
      
      if (word[0] === " ") {
        this.inputValue.text = ''; return
      }

      if (word !== word.trim()) {
        this.checkWord(word.trim());
        this.inputValue.text = '';
        // console.log(this.completedWords);
      }
    },
    checkWord(word) {
      if (this.words[this.indexWord] == word) {
        this.completedWords.push(1);
      } else {
        this.completedWords.push(0);
      }
      this.doUpdate += 1;
      this.indexWord += 1;
    },
    shuffle(array) {
      array.sort(() => Math.random() - 0.5);
      return array;
    },
    deleteWords() {
      this.words = [];
      this.indexWord = 0;
      this.completedWords = [];
      this.inputValue.text = ''
      this.doUpdate += 1;
    },
    shuffleWords(array) {
      this.words = this.shuffle(array);
      this.indexWord = 0;
      this.completedWords = [];
      this.inputValue.text = ''
      this.doUpdate += 1;
    },
  },
  mounted() {
    this.shuffleWords(this.dictionary);
    this.doUpdate += 1;
    
    // this.doUpdate = true;
    // через boolen значения оказалось тяжелее
  },
  // watch: {
  //   doUpdate() {
  //     // this.doUpdate = false;
  //   }
  // }
}
</script>

<style>
*, *::after, *::before {
  margin: 0;
  padding: 0;
  outline: none;
  
  box-sizing: border-box;
}

.full__container {
  display: flex;
  justify-content: center;
}

.container {
  margin: 0 100px;
  margin-top: 100px;
}


.input-wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
  padding: 10px;
  background-color: black;
  height: 60px;
}

.input-value {
  padding: 10px;
  /* margin-top: 100px; */
  font-size: 24px;
  width: 400px;
  height: 40px;
}
</style>
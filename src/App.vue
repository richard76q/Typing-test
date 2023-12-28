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
          placeholder="Введите слово &#9733;"
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
        'assert', 'clear', 'count', 'debug', 'dir', 'error', 'group', 'info'
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

      this.checkWordForMistake(word, this.words[this.indexWord])

      if (word !== word.trim()) {
        this.checkWord(word.trim());
        this.inputValue.text = '';
      }
    },
    checkWord(word) {
      this.checkLastMistake()
      if (this.words[this.indexWord] == word) {
        this.addCompletedWords(1);
      } else {
        this.addCompletedWords(0);
      }
      this.doUpdate += 1;
      this.indexWord += 1;
    },
    checkWordForMistake(word1, word2) {
      this.checkLastMistake();

      for (let i = 0; i < word1.length; i++) {
        if (word1[i] !== word2[i]) {
          this.addCompletedWords(2);
          this.doUpdate += 1;
          console.log('add1')
          return
        }
      }
    },
    checkLastMistake() {
      if (this.completedWords.at(-1) === 2) {
        this.delComletedWords();
        this.doUpdate += 1;
        console.log('del1')
        return true
      }
    },
    addCompletedWords(num) {
      this.completedWords.push(num);
    },
    delComletedWords() {
      console.log('pop1')
      this.completedWords.pop();
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

#app {
  max-width: 1920px;
}


.full__container {
  display: flex;
  justify-content: center;
}

.container {
  margin: 0 100px;
  margin-top: 120px;
}


.input-wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
  padding: 20px 10px;
  background-color: #000;
  height: 100px;
}

.input-value {
  padding: 10px 20px;
  /* margin-top: 100px; */
  font-size: 32px;
  line-height: 1.2em;
  font-weight: 600;
  /* color: #61c9ff; */
  /* color: #00bfff; */
  color: #333;
  width: 500px;
  height: 60px;
}

.input-value::placeholder {
  color: #555;
}

.input-value:focus::placeholder {
  color: #888;
}
</style>
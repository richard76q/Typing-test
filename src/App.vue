<template>
  <div class="full__container">
    <div class="container">
      <!-- <WordForm :words="words" :completed="completedWords" :update="doUpdate" :id="indexWord" :updateWordHeight="updateWordHeight"/> -->
      <WordForm :words="words" :completed="completedWords" :update="doUpdate" :id="indexWord"/>
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
        text: '',  // при изменение этого значение input будет меняться
        // IdCounts: 0,
      },
      dictionary: [  // библиотека слов
        'hello', 'world', 'console', 'log',
        'const', 'var', 'let', 
        'null', 'undefined', 'boolen', 'number', 'bigint', 'string', 'symbol',
        'assert', 'clear', 'count', 'debug', 'dir', 'error', 'group', 'info',

        'hello', 'world', 'console', 'log',
        'const', 'var', 'let', 
        'null', 'undefined', 'boolen', 'number', 'bigint', 'string', 'symbol',
        'assert', 'clear', 'count', 'debug', 'dir', 'error', 'group', 'info',
      ],
      words: [],  // слова которые отправляются в WordForm после для отрисовки в WordItem
      indexWord: 0,  // индекс this.words
      completedWords: [],  // массив отвечаюзий за раскрашивание слов по результатам вычеслений 
                           //[0 - неправильный ответ, 1 - правильный ответ, 2 - динамическая ошибка, 3 - следующее слово]
      doUpdate: 0,  // переменная которая проверяется в WordForm на обновление и после обновляет массив слов в окне
      // updateWordHeight: 0
    }
  },
  methods: {
    checkInput(event) {
      const word = event.target.value;  // получения значения из input

      if (this.words.length === 0) {  // заканчиваем цикл если this.words пустой 
        console.log('empty')
        return
      }

      if (this.indexWord >= this.words.length) {  // конец
        this.inputValue.text = "Вы прошли"
        return
      }
      
      
      if (word[0] === " ") {  // защита от нажатие первого пробела
        this.inputValue.text = ''; return
      }

      this.checkWordForMistake(word, this.words[this.indexWord])  // проверяет word и след. по индексу this.words на ошибки

      if (word !== word.trim()) {    // отправет слова на проверку при нажатие на пробел
        this.checkWord(word.trim());
        this.inputValue.text = '';
      }
    },
    checkWord(word) {    // проверяет правильно ли написано слово
      this.checkLastMistake()
      if (this.words[this.indexWord] == word) {
        this.addCompletedWords(1);
      } else {
        this.addCompletedWords(0);
      }
      this.doUpdate += 1;   // обновляем список слов
      this.indexWord += 1;  // добавляем индекс для проверки this.words
      this.addCompletedNext();
    },
    checkWordForMistake(word1, word2) {  // динамическая проверка слов на ошибки
      this.checkLastMistake();

      for (let i = 0; i < word1.length; i++) {  // сравнивает word1 с word2 по длине word1
        if (word1[i] !== word2[i]) {
          this.addCompletedWords(2);
          this.doUpdate += 1;
          return 
        }
      }
      this.addCompletedNext();
    },
    checkLastMistake() {  // удаление поледней диманической ошибки или (следующие) слова
      if (this.completedWords.at(-1) === 2  || this.completedWords.at(-1) === 3) {
        this.delComletedWords();
        this.doUpdate += 1;
      }
    },

    addCompletedNext() {  // добавление 3 в this.completedWords
      this.addCompletedWords(3);
      this.doUpdate += 1;
    },

    addCompletedWords(num) {  // добавляем результаты в this.completedWords
      this.completedWords.push(num);
    },
    delComletedWords() {  // удаление последнего this.completedWords
      this.completedWords.pop();
    },



    shuffle(array) {  // размешивает списки и возращает
      array.sort(() => Math.random() - 0.5);
      return array;
    },
    shuffleWords(array) {  // размешивание this.words и обнуление значений
      this.words = this.shuffle(array);
      this.reset();
      // this.updateWordHeight += 1;
      this.addCompletedNext();
    },
    deleteWords() {  // обнуление всех значений
      this.words = [];
      this.reset();
    },
    reset() {  // обнуление
      this.inputValue.text = '';
      this.indexWord = 0;
      this.completedWords = [];
      // this.updateWordHeight += 1;
      this.doUpdate += 1;
    },
  },
  mounted() {  // встоенная функция сайта
    this.shuffleWords(this.dictionary);
  }
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
<template>
    <div type="text" class="container__word" :style="{'margin-top': marginTop}">
        <span class="word" v-for="i in this.words.length" :key="i" :class="giveClass(this.words[i-1][1], i)">{{ this.words[i-1][0] }}</span>
    </div>
</template>

<script>
    export default {
        props: {
            words: {
                type: Array, 
                required: true
            },
            // updateWordheight: {
            //     type: Number,
            //     required: false
            // },
            id: {
                type: Number,
                required: false
            }
        },
        data() {
            return {
                marginTop: '',  // перменная используется в css стиле у .container__word
                marginValue: 0,
                wordHeights: [],  // массив чисел 
                correctHeightWord: 0,  // высота относительно offsetParent
            }
        },
        methods: {
            giveClass(ntype, i) {  // возращает определенный класс по переданному числу
                switch (ntype) {
                    case undefined:
                        return;
                    case 1:
                        return "comp-green"
                    case 0:
                        return "comp-red"
                    case 3:
                        if (i === 1 && this.id === 0) {  // временное решение чтобы получать массив высоты каждого слова
                            this.marginTop = '0';
                            this.marginValue = 0;
                            this.correctHeightWord = 0;
                            this.getWordHeights();
                        }
                        this.checkWord1();
                        return "word-next"
                    case 2:
                        return "word-mistake"
                    default:
                        console.log("error")
                }
                // if (ntype === undefined) {
                //     return
                // } else if (ntype === 1) {
                //     return "comp-green"
                // } else if (ntype === 0) {
                //     return "comp-red"
                // } else if (ntype === 3) {
                //     this.checkWord1();
                //     return "word-next"
                // } else if (ntype === 2) {
                //     return "word-mistake"
                // } else {
                //     console.log("error")
                // }
            },
            
            checkWord1() { // получаем высоту относительно offsetParent если он равен 0, а после проверка на высоту и изменение высоты
                if (this.correctHeightWord === 0 || this.correctHeightWord === undefined) {
                    this.correctHeightWord = this.wordHeights[this.id];
                } else if (this.correctHeightWord !== this.wordHeights[this.id]) {
                    this.correctHeightWord = this.wordHeights[this.id];
                    this.marginupdateWordheight();
                }
            },

            getWordHeights() {  // получения высоты каждого слово относительно верхней части offsetParent
                this.wordHeights = [];
                const text = document.getElementsByClassName("word");

                for (let i = 0; i < text.length; i++) {
                    this.wordHeights.push(text[i].offsetTop);
                }
            },

            marginupdateWordheight() {  // поднимает container__word на 60 пикселей
                this.marginValue += 60;
                this.marginTop =  '-' + String(this.marginValue) + 'px';
            },
        },
        watch: {
            // updateWordheight() {  // обновление массива высоты каждого слово в this.wordHeights 
            //     // this.getWordHeights();
            //     console.log(this.updateWordheight)
            //     console.log(this.correctHeightWord)
            //     console.log(this.id)
            // }
        },
    }
</script>

<style scoped>
.container__word {
    user-select: none;
}

.word {
    display: inline-block;
    font-size: 2.6em;
    line-height: 1.2em;
    font-weight: 600;
    padding: 4px 7px;
    color: #61c9ff;
    border-bottom: 2px solid #fff;
}

.comp-green {
    color: #22bb22;
}

.comp-red {
    color: #E00;
}

.word-mistake {
    background-color: #FFCBDB;
    border-bottom: 2px solid #E00;
}

.word-next {
    background-color: #f4f4f4;
    border-bottom: 2px solid #61c9ff;
}


.text {
    color: #000;
}
</style>
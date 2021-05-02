<template>
  <div class="googlon">
    <textarea v-model="text" placeholder="Cole seu pergaminho aqui"/>
    <button class="btnClean" v-on:click="cleanUp($event)">Limpar</button>
    <button v-on:click="generateGooglon">Enviar</button>
    <div class="container-span">
      <span>Verbos: {{ verbos }}</span>
      <span>Verbos primeira pessoa: {{ verbosPrimeiraPessoa }}</span>
      <span>Preposições: {{ preposicoes }}</span>
      <span>Números bonitos distintos: {{ numerosBonitosDistintos }}</span>
    </div>
    <textarea v-model="vocabulario"/>
  </div>
</template>

<script>
export default {
  name: 'Googlon',
  props: {
    msg: String
  },
  data() {
    return {
      text: '',
      verbos: '',
      verbosPrimeiraPessoa: '',
      preposicoes: '',
      numerosBonitosDistintos: '',
      foo: '',
      lexico: '',
      vocabulario: ''
    }
  },
  methods: {
    cleanUp(limpar) {
      if (limpar) {
        this.text = ''
      }
      this.verbos = 0;
      this.verbosPrimeiraPessoa = 0;
      this.preposicoes = 0;
      this.numerosBonitosDistintos = 0;
      this.vocabulario = ''
      console.log('Limpo!')
    },
    constructor(text) {
      if (text) {
        this.text = text.trim();
      }
      this.foo = ['s', 'j', 'n', 'c', 'q'];
      this.verbos = 0;
      this.verbosPrimeiraPessoa = 0;
      this.preposicoes = 0;
      this.numerosBonitosDistintos = 0;
      this.lexico = 'skmgnwqztxdrpcfjlbvh';
    },
    generateGooglon() {
      this.cleanUp();
      this.searchPrepositions();
      this.searchVerbs();
      this.sortToText();
      this.beautifulNumber();
    },

    searchPrepositions() {
      this.constructor();
      let words = this.text.split(' ');
      words.map(word => {
        if (word.length === 4) {
          let lastLetter = word.slice(word.length - 1,);
          if (this.foo.includes(lastLetter)) {
            this.preposicoes++;
          }
        }
      });
    },
    searchVerbs() {
      let words = this.text.split(' ');
      words.map(word => {
        if (word.length >= 7) {
          let firstLetter = word.slice(0, 1);
          let lastLetter = word.slice(word.length - 1,);
          if (!this.foo.includes(lastLetter)) {
            this.verbos++;
            if (this.foo.includes(firstLetter)) {
              this.verbosPrimeiraPessoa++;
            }
          }
        }
      });
    },
    textToSort() {
      let words = this.text.split(' ');
      let lexicoList = this.lexico.split('');
      let wordsSorted = [];
      words.map(word => {
        let firstLetter = word.slice(0, 1);
        if (lexicoList.includes(firstLetter)) {
          if (!wordsSorted.includes(word)) {
            wordsSorted.push(word);
          }
        }
      });
      return wordsSorted;
    },
    sortToText() {
      let vocabulario = this.textToSort();
      this.vocabulario = vocabulario.join(' ');
    },
    textToNumber() {
      let words = this.text.split(' ');
      let lexicoList = this.lexico.split('');
      let values = [];
      let value = 0;
      // eslint-disable-next-line no-unused-vars
      words.map((word, index) => {
        let letter = word.split('');
        letter.map((l, index) => {
          let indexList = lexicoList.indexOf(l);
          value += indexList * Math.pow(20, index);
        });
        values.push(value);
      });
      return values
    },
    beautifulNumber() {
      let numbersConverted = this.textToNumber();
      let numberBase = 563131;
      let numberDivider = 5;
      numbersConverted.forEach(num => {
        if (num >= numberBase && num % numberDivider === 0) {
          this.numerosBonitosDistintos++
        }
      });
    },
    response() {
      return {
        verbos: this.verbos,
        verbosPrimeiraPessoa: this.verbosPrimeiraPessoa,
        preposicoes: this.preposicoes,
        vocabulario: this.vocabulario,
        beautiful: this.numerosBonitosDistintos
      }
    }
  },
}
</script>

<style scoped>
textarea {
  width: 100%;
  height: 100px;
}

span {
  width: 25%;
  /* display: block; */
  margin: 0 0 0 15%;
}

button {
  display: inline-block;
  border-radius: 4px;
  background-color: #007fff;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 20px;
  padding: 10px;
  width: 100px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

.btnClean {
  display: inline-block;
  border-radius: 4px;
  background-color: #F24F00;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 20px;
  padding: 10px;
  width: 100px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

.container-span {
  text-align: left;
  padding: 5px;
}
</style>

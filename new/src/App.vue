<script setup>
import { computed, ref } from 'vue';
import '../src/assets/style.css';
import Header from "./components/Header.vue";
import Figure from "./components/Figure.vue";
import WrongLetters from "./components/WrongLetters.vue";
import Word from "./components/Word.vue";

import Pop from "./components/Popup.vue";
// import { keyDown } from './components/keyDown';

const allWord = [
    "cat",
    "pooh",
    "university"
   
   
];
const randomWord = () => allWord[Math.floor(Math.random() * allWord.length)];
const word = ref(randomWord());
const guessedLetters = ref([]);

const letters = computed(() => word.value.split(""));

const wrongLetters = computed(() =>
    guessedLetters.value
        .filter((l) => !letters.value.includes(l))
        .reduce((x, y) => (x.includes(y) ? x : [...x, y]), [])
);

function test() {
    console.log(wrongLetters.value);
}

const correctLetters = computed(() =>
    guessedLetters.value.filter((l) => letters.value.includes(l))
);

const keyD = (event) => {
    
    const letter = event.key.toLowerCase();
    
    //  if(guessedLetters.value.includes(letter)){
    //          guessedLetters.value.push(letter)
    //  }
    guessedLetters.value.push(letter);
    console.log(event.key);
    console.log((event.target.value = ""));
};

const status = computed(()=>
{
    if(wrongLetters.value.length === 6) {
    return 'lost'

    }

     if(letters.value.every(l => correctLetters.value.includes(l)))
    return 'win'

    else return ''

})

const reset = () => {
    guessedLetters.value = [];
    allNewWordzzz.value = randomWord();
    wrongLetters.value;
};

const tell = ref(false);


const showPopup = () => {
    tell.value = true;
    setTimeout(() => {
        tell.value = false;
    });
};

// keyDown (event =>{

// const letter =event.key.toLowerCase()
// // if(event.keyCode < 65 && event.keyCode >90){
// //       wrongLetters = ('')
// // }
// // if(status.value)
// if(guessedLetters.value.includes(letter)){

// }
// guessedLetters.value.push(letter)

// })
const ss = ref(false)
</script>

<template>
    <div>
        <Header />
        <Figure :wrongcount="wrongLetters.length" />
        <input @keydown="keyD" type="text" class="text-black" />
        <Word :letters="letters" :correct-letters="correctLetters" />
        <!-- <Tell :show="tell"/> -->
       
            <WrongLetters class="-mr-48" :wrong-letters="wrongLetters" />
         
        <Pop :status="status " :word="word"/>
      

        
    </div>
</template>

<style scoped></style>

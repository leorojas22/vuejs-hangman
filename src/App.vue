<template>
    <div class="container">
        <div class="row">
            <div class="col-3">
                <app-hang-post :wrongAnswers="wrongAnswers"></app-hang-post>
            </div>
            <div class="col">
                <app-word :word="wordPicked" :lettersGuessed="lettersGuessed"></app-word>
            </div>
        </div>
        <div class="row">
            <div class="col-2 offset-2">
                <!-- Guess letter form goes here -->
                <form v-if="!playerWon && wordPicked">
                    <div class="form-group">
                        <input type="text" maxlength="1" class="form-control" placeholder="Enter Letter" v-model="guessedLetter">
                    </div>
                    <div class="form-group">
                        <button class="btn btn-primary" @click="guess">
                            Guess!
                        </button>
                    </div>
                </form>
                <form v-else>
                    <div class="form-group">
                        <button class="btn btn-info" type="button" @click="startNewGame">
                            New Game
                        </button>
                    </div>
                </form>
            </div>
            <div class="col">
                <p><strong>Guessed Letters:</strong></p>
                <p>
                    <template v-for="letter in lettersGuessed">{{ letter }} </template>
                </p>
            </div>
        </div>
    </div>
</template>

<script>
    import HangPost from './components/HangPost.vue';
    import Word from './components/Word.vue';

    export default {
        components: {
            appHangPost: HangPost,
            appWord: Word
        },
        data() {
            return {
                wordBank: [
                    'movie theater',
                    'baseball',
                    'gnome',
                    'thunder storm',
                    'new york',
                    'california',
                    'airplane',
                    'circus',
                    'water bottle',
                    'Happy New Year!'
                ],
                wordPicked: "",
                lettersGuessed: [],
                guessedLetter: ""
            }
        },
        computed: {
            wrongAnswers() {
                let wrongAnswers = 0;

                // Count the number of incorrect letters in the letters guessed array
                let lowercaseWord = this.wordPicked.toLowerCase();
                let lettersGuessedTotal = this.lettersGuessed.length;
                for(let x = 0; x < lettersGuessedTotal; x++)
                {
                    let letter = this.lettersGuessed[x];
                    if(lowercaseWord.indexOf(letter) === -1)
                    {
                        // Letter not in the word
                        wrongAnswers++;
                    }
                }

                return wrongAnswers;
            },
            playerWon() {

                // Check if the player won
                let lowercaseWord = this.wordPicked.toLowerCase();
                let wordLength = lowercaseWord.length;
                let playerWon = true;
                for(let x = 0; x < wordLength; x++)
                {
                    let letter = lowercaseWord[x];
                    if(letter.match(/[a-z0-9]/g) && this.lettersGuessed.indexOf(letter) === -1)
                    {
                        // Hasn't guessed this letter yet, player has not won
                        playerWon = false;
                        break;
                    }
                }

                return playerWon;
            }
        },
        methods: {
            startNewGame() {
                // Get a random number from 0 to the number of words in our word bank
                let totalWords = this.wordBank.length;
                let randomNumber = Math.floor(Math.random() * totalWords);

                // Clear out letters guessed
                this.lettersGuessed = [];

                // Set the word picked to a random word
                this.wordPicked = this.wordBank[randomNumber];

            },
            guess(e) {
                e.preventDefault();

                let lowercaseLetter = this.guessedLetter.toLowerCase();

                if(this.lettersGuessed.indexOf(lowercaseLetter) !== -1)
                {
                    // Letter already guessed!
                    alert("That letter has already been guessed!");
                }
                else if(!lowercaseLetter.match(/[a-z0-9]/g))
                {
                    // Value entered is not a letter or number
                    alert("You may only enter letters or numbers!");
                }
                else
                {
                    // If it makes it here, the letter is valid
                    this.lettersGuessed.push(lowercaseLetter);

                    if(this.wrongAnswers > 5)
                    {
                        // Player Loses
                        if(confirm("You lost!  The word was "+this.wordPicked+". Do you want to play again?"))
                        {
                            // Restart game
                            this.startNewGame();
                        }
                    }


                    if(this.playerWon)
                    {
                        // Player won
                        if(confirm("You won! Do you want to play again?"))
                        {
                            // Restart game
                            this.startNewGame();
                        }
                    }
                }

                this.guessedLetter = "";
            }
        },
    }
</script>

<style>
    body {
        padding: 20px;
    }
</style>

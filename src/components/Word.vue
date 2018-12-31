<template>
    <p>
        {{ revealedWord }}
    </p>
</template>

<script>
export default {
    props: [
        'word',
        'lettersGuessed'
    ],
    computed: {
        revealedWord() {
            let wordLength = this.word.length;
            let formattedWord = "";
            for(let x = 0; x < wordLength; x++)
            {
                let letter = this.word[x];
                if(this.lettersGuessed.indexOf(letter.toLowerCase()) !== -1)
                {
                    formattedWord += letter;
                }
                else if(letter.match(/[A-Za-z0-9]/g))
                {
                    // Letter is not a symbol or space
                    formattedWord += " _ ";
                }
                else if(letter === " ")
                {
                    formattedWord += "    ";
                }
                else
                {
                    formattedWord += letter;
                }
            }

            return formattedWord;
        }
    }
}
</script>

<style scoped>
    p {
        white-space: pre;
        font-size: 24px;
    }
</style>

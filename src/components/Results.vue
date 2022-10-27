<template>
    <div class="results">
        <h3>Reaction Time: <span>{{ score }}</span></h3>
        <div v-if="score">
         <h4 >{{ rank }}</h4>   
         <div class="button-container">
            <button @click="reset">Play Again</button>
        </div>
        </div>
        
    </div>

</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Time } from '../globals'

interface Data {
    rank: () => string | null
}

export default defineComponent({
    name: "Results",
    props: {
        score: {
            required: true,
            type: Object as PropType<Time>
        }
    },
    data(): Data {
        return {
            rank: this.setRank()
        }
    },
    methods: {
        setRank() {
            if (!this.score) return null
            return (this.score < 300)
                ? "What The ....."
                : (this.score < 450)
                    ? 'Pretty Average, Cowboy'
                    : "We Don't Ask You To Be Perfect, We Just Ask That You Be Better"
        },
        reset(){
            this.$emit('reset')
        }
    }
})
</script>

<style>
.results {
    margin: auto;
    width: 50%;
    padding: 2rem;
    border: 0.1rem solid black;
    background-color: white;
    filter: drop-shadow(0.2rem 0.2rem 0.2rem rgb(89, 89, 89));
}

.results>h3 {
    border-bottom: 0.25rem solid rgb(193, 191, 188);
}

.results>span {
    color: red
}

.button-container {
    margin: auto;
    width: 50%
}
.button-container > button {
    background-color: rgba(0, 128, 0, 0.506);
    padding: 0.5rem 1rem;
    border-radius: 2rem;
}
button:hover{
    cursor: pointer;
}
</style>
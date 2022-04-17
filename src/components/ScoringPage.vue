<template>
    <div>
        <h1>Quartermaster General: Victory or Death</h1>
        <h2>Scoring app</h2>
        <div v-if="round === 0">
            <button v-on:click="startGame">Start a new game</button>
        </div>
        <div v-else>
            <p> {{ turnInfoText }} </p>
            <p> {{ scoringInfoText }} </p>
            <input id="scoreInput" type="number" v-model="scoreInput">
            <p> Score input: {{ scoreInput }} </p>
            <button v-on:click="addScore">Add score</button>
            <p>Oligarch's score: {{ oligarchScore }} </p>
            <p>Demos' score: {{ demosScore }} </p>
            <p> {{ situationText }} </p>
            <button v-on:click="endTurn">End turn</button>
            <div>
                <button v-on:click="startGame">Start a new game</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ScoringPage',
        props: {},
        data() {
            return {
                round: 0,
                turn: "",
                scoreInput: 0,
                corinthScore: 0,
                delianScore: 0,
                spartaScore: 0,
                athensScore: 0,
                gameEnd: false,
            }
        },
        computed: {
            turnInfoText() {
                return `Round ${this.round} - ${this.turn}'s turn`;
            },
            scoringInfoText() {
                return `Add victory points to ${this.turn}.`
            },
            oligarchScore() {
                return this.corinthScore + this.spartaScore;
            },
            demosScore() {
                return this.delianScore + this.athensScore;
            },
            situationText() {
                let text;
                let pointDifference = Math.abs(this.oligarchScore - this.demosScore);
                if (this.oligarchScore > this.demosScore) {
                    text = `Oligarchs lead by ${pointDifference} point(s).`
                } else if (this.oligarchScore < this.demosScore) {
                    text = `Demos lead by ${pointDifference} point(s).`
                } else {
                    text = "It is draw. (Oligarchs win ties.)"
                }
                return text;
            }
        },
        methods: {
            startGame() {
                this.round = 1;
                this.turn = "Corinth";
                this.scoreInput = undefined;
                this.corinthScore = 0;
                this.delianScore = 0;
                this.spartaScore = 0;
                this.athensScore = 0;
            },
            addScore() {
                const score = parseInt(this.scoreInput)
                switch (this.turn){
                    case "Corinth":
                        this.corinthScore += score;
                        break;
                    case "Delian League":
                        this.delianScore += score;
                        break;
                    case "Sparta":
                        this.spartaScore += score;
                        break;
                    case "Athens":
                        this.athensScore += score;
                        break;            
                }
            },
            endTurn() {
                switch (this.turn){
                    case "Corinth":
                        this.turn = "Delian League";
                        break;
                    case "Delian League":
                        this.turn = "Sparta";
                        break;
                    case "Sparta":
                        this.turn = "Athens";
                        break;
                    case "Athens":
                        this.turn = "Corinth";
                        this.round++;
                        this.checkGameEnd();
                        break;    
                }
            },
            checkGameEnd() {
                if (this.round > 20) {
                    this.gameEnd = true;
                }
                // Scoring round are after rounds 4, 8, 12, 16
                if ( (this.round - 1) % 4 !== 0 && this.round - 1 !== 0) {
                    this.gameEnd = true;
                }
            },
        }
    }
</script>
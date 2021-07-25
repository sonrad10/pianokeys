<template>
	<div id="app" class="app" @keydown.enter="run" @keydown.space="run">
		<div class="top">
			<div class="output-holder" v-text="output" />

			<div class="run-button" @click="run">
				<font-awesome-icon icon="random" class="icon" />
				<span>Random</span>
			</div>
		</div>

		<div class="options-holder">
			<div class="option">
				<label class="toggle-label">
					<input type="checkbox" v-model="showLetters" />
					Notes
				</label>
			</div>

			<div class="option">
				<label class="toggle-label">
					<input type="checkbox" v-model="showFingers" />
					Fingers
				</label>
			</div>

			<div class="option">
				<label class="toggle-label">
					<input type="checkbox" v-model="showHands" />
					Hand
				</label>
			</div>
		</div>

		<div class="description">
			<p>
				This is a quick utility I threw together to help with learning to play the piano, based on
				<a href="https://www.youtube.com/watch?v=QBH6IpRkVDs">Bill Hilton's Keyboard familiarisation game</a>
				from his first video.
			</p>
			<p>
				Watch the video for instructions on how to play the game.
			</p>
		</div>
	</div>
</template>

<script>
import Vue from "vue";

function randomNumber(max = 1) {
	return Math.floor(Math.random() * max);
}

export default Vue.extend({
	name: 'App',
	data() {
		return {
			showLetters: true,
			showFingers: false,
			showHands: false,
			currentLetter: 'A',
			currentFinger: '1',
			currentHand: 'R',
			alphabet: 'ABCDEFG',
			fingers: '12345',
		}
	},
	computed: {
		output() {
			let res = '';
			if (this.showLetters) res += this.currentLetter;
			if (this.showFingers) res += this.currentFinger;
			if (this.showHands) res += ' ' + this.currentHand;
			return res;
		},
	},
	methods: {
		run() {
			this.currentLetter = this.randomLetter();
			this.currentFinger = this.randomNumber();
			this.currentHand = this.randomHand();
		},
		randomLetter() {
			return this.alphabet.charAt(randomNumber(this.alphabet.length));
		},
		randomNumber() {
			return this.fingers.charAt(randomNumber(this.fingers.length));
		},
		randomHand() {
			return randomNumber(2) ? 'L' : 'R'
		},
	},
	mounted() {
		document.onkeydown = (event) => {
			//On 'enter' or 'space' press
			if (event.key === "Enter" || event.key === " ") {
				event.preventDefault();
				this.run();
			}
		};
	}
})
</script>

<style scoped>
.app {

}

/*.output-holder, .run-button {*/
.output-holder {
	height: 100px;
	line-height: 100px;
	vertical-align: middle;
}

.output-holder {
	border: 1px solid gray;
	border-radius: 10px;

	display: inline-block;

	width: 100px;

	font-size: xxx-large;
	text-align: center;
	user-select: none;
}

.run-button {
	height: 80px;
	width: 120px;

	border-radius: 20px;
	margin-left: 100px;
	padding: 10px 0;

	vertical-align: middle;

	display: inline-block;

	font-size: x-large;
	text-align: center;
	user-select: none;

	background-color: steelblue;
	color: white;
}
.run-button:hover {
	cursor: pointer;
	background-color: #3672a4;
}
.run-button .icon {
	/*font-size: xxx-large;*/
	width: 100%;
	height: 50px;
}

.options-holder {
	margin-left: auto;
	margin-right: auto;
	left: 0;
	right: 0;
}

.options-holder .option {
	text-align: left;

	display: inline-block;

	margin-left: 1em;
}

.options-holder label {
	text-align: left;
	flex: .2;
}

.description {
	text-align: left;
}
</style>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
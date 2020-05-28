<template>
	<div>
		<div id="metro_comp">
			<h3>Metronome</h3>
			<div class="btns_inp">
				<button
					class="plus_minus"
					v-show="!isPlaying"
					@click="bpm--; limitbpm()"
				>-</button>
				<div class="unit_input">
					<input
						type="number"
						v-model="bpm"
						name="bpm"
						@blur="limitbpm"
						class="num_input"
					>
					<label for="bpm">BPM</label>
				</div>
				<button
					class="plus_minus"
					v-show="!isPlaying"
					@click="bpm++; limitbpm()"
				>+</button>
			</div>

			<div class="btns_inp">
				<button
					class="plus_minus"
					v-show="!isPlaying"
					@click="bpb--; limitbpb()"
				>-</button>
				<div class="unit_input">
					<input
						type="number"
						v-model="bpb"
						name="bpb"
						@blur="limitbpb"
						class="num_input"
					>
					<label for="
				bpb">divisions</label>
				</div>
				<button
					class="plus_minus"
					v-show="!isPlaying"
					@click="bpb++; limitbpb()"
				>+</button>
			</div>

			<div class="buttons">
				<button
					@click="play"
					:class="{'active':(isPlaying)}"
				>
					Start
				</button>
				<button @click="pause">
					Stop
				</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			normalTick: '',
			upTick: '',
			bpm: 60,
			bpb: 4,
			isPlaying: false
		}
	},
	computed: {
		toMs() {
			return 60000 / this.bpm;
		}
	},
	methods: {
		play() {
			if (this.isPlaying) {
				this.isPlaying = false;
			}
			let millisecs = this.toMs;
			let bpb = this.bpb;
			let counter = 0;
			const downTick = this.normalTick;
			const upTick = this.upTick;

			let downCounter = 0;
			let downTicksArr = [];

			for (let i = 0; i < 10; i++) {
				downTicksArr.push(downTick.cloneNode());
			}

			const tick = function () {
				downCounter = (downCounter + 1) % 10;
				downTicksArr[downCounter].play();
				downTicksArr.push(downTick.cloneNode());
			}


			let upCounter = 0;
			let upTicksArr = [];

			for (let i = 0; i < 10; i++) {
				upTicksArr.push(upTick.cloneNode());
			}

			const tickUp = function () {
				upCounter = (upCounter + 1) % 10;
				upTicksArr[upCounter].play();
				upTicksArr.push(upTick.cloneNode());
			}

			this.isPlaying = true;
			if (this.isPlaying) {
				upTick.play();
				let noteInterval = setInterval(() => {
					counter++;
					if (counter > bpb) {
						counter = 1;
					}
					counter != bpb ? tick() : tickUp();
					if (!this.isPlaying) {
						downTicksArr[downCounter].pause();
						upTicksArr[upCounter].pause();
						this.pause(noteInterval);
					}
				}, millisecs);
			}
		},
		pause(interval) {
			this.isPlaying = false;
			clearInterval(interval);
		},
		limitbpm() {
			if (this.bpm < 30) {
				this.bpm = 30;
			} else if (this.bpm > 500) {
				this.bpm = 500;
			}
		},
		limitbpb() {
			if (this.bpb < 1) {
				this.bpb = 1;
			} else if (this.bpb > 12) {
				this.bpb = 12;
			}
		}
	},
	mounted() {
		this.normalTick = new Audio(require('@/assets/metronome.wav'));
		this.upTick = new Audio(require('@/assets/metronomeup.wav'))
	}
}
</script>

<style scoped>
#metro_comp {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}

.buttons button {
	width: 100px;
}
</style>
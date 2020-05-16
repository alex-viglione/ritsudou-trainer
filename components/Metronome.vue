<template>
	<div>
		<div id="metro_comp">
			<h3>Metronome</h3>
			<label for="bpm">BPM:</label>
			<input
				type="text"
				v-model="bpm"
				name="bpm"
				@blur="limitbpm"
			>
			<p>Millisecond gap : {{toMs}}</p>
			<label for="bpb">1/4 notes per measure:</label>
			<input
				type="text"
				v-model="bpb"
				name="bpb"
				@blur="limitbpb"
			>
			<input
				type="button"
				value="PLAY"
				@click="play"
			>
			<input
				type="button"
				value="PAUSE"
				@click="pause"
			>
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

			this.isPlaying = true;
			if (this.isPlaying) {
				upTick.play();
				let noteInterval = setInterval(() => {
					counter++;
					if (counter > bpb) {
						counter = 1;
					}
					counter != bpb ? downTick.play() : upTick.play();
					if (!this.isPlaying) {
						downTick.pause();
						upTick.pause();
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
			} else if (this.bpm > 240) {
				this.bpm = 240;
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
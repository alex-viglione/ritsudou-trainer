<template>
	<div>
		<div id="wrapper">
			<h1>Sound test</h1>
			<nuxt-link to="/">Back to home</nuxt-link>
			<label for="bpm">BPM</label>
			<input
				type="text"
				v-model="bpm"
				name="bpm"
			>
			<p>Millisecond gap : {{toMs}}</p>
			<label for="bpb">BPB</label>
			<input
				type="text"
				v-model="bpb"
				name="bpb"
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
		}
	},
	mounted() {
		this.normalTick = new Audio(require('@/assets/metronome.wav'));
		this.upTick = new Audio(require('@/assets/metronomeup.wav'))
	}
}
</script>

<style scoped>
#wrapper {
	display: flex;
	flex-direction: column;
	align-items: center;
}
</style>
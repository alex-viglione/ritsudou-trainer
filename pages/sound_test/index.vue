<template>
	<div>
		<h1>Sound test</h1>
		<nuxt-link to="/">Back to home</nuxt-link>
		<input
			type="button"
			value="PLAY"
			@click="play()"
		>
	</div>
</template>

<script>
export default {
	data() {
		return {
			audio: ''
		}
	},
	methods: {
		play() {
			// this.audio.play();
			setInterval(() => {
				this.audio.play();
			}, 10);
		}
	},
	mounted() {
		this.audio = new Audio(require('@/assets/metronome.wav'))
	}
}
</script>
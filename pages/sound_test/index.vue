<template>
	<div>
		<h1>Sound test</h1>
		<nuxt-link to="/">Back to home</nuxt-link>
		<button @click.prevent="playSound('../../assets/metronome.wav')">Play sound</button>
		<audio
			id="audio"
			:src="require('@/assets/metronome.wav')"
			controls
			autostart="false"
		></audio>
	</div>
</template>

<script>
export default {
	methods: {
		playSound(sound) {
			if (sound) {
				let audio = new Audio(sound);
				audio.play();
			}
		}
	}
}
</script>
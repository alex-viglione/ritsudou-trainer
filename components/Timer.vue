<template>
	<div>
		<div id="timer_comp">
			<h3>Timer</h3>

			<div class="time_input">
				<input
					type="text"
					v-model="minutes"
					class="text_input"
				> minutes
			</div>

			<div class="time_input">
				<input
					type="text"
					v-model="seconds"
					class="text_input"
				> seconds
			</div>

			<button @click="countdown">Start countdown</button>
			<button @click="isCounting = false">Pause countdown</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			seconds: 5,
			minutes: 1,
			isCounting: false
		}
	},
	methods: {
		countdown() {
			this.isCounting = true;
			if (this.seconds > 0) {
				setTimeout(() => {
					if (!this.isCounting) {
						return;
					} else {
						this.seconds -= 1;
						this.countdown();
					}
				}, 1000);
			}
		}
	},
	watch: {
		seconds: function () {
			if (this.seconds === 0 && this.minutes > 0) {
				setTimeout(() => {
					this.minutes--;
					this.seconds = 59;
					this.countdown();
				}, 1000)
			}
		}
	}
}
</script>

<style scoped>
#timer_comp {
	display: flex;
	height: 100px;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}

.time_input {
	display: flex;
	align-items: center;
}

.text_input {
	width: 30%;
	margin-left: 20%;
	margin-right: 5%;
}
</style>
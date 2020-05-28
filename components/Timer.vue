<template>
	<div>
		<div id="timer_comp">
			<h3>Timer</h3>

			<div
				class="btns_inp"
				v-if="!isCounting"
			>
				<button
					class="plus_minus"
					@click="minutes >= 1 ? minutes-- : minutes"
				>-</button>
				<div class="unit_input">
					<input
						type="number"
						v-model="minutes"
						class="num_input"
						@blur="minutes < 0 ? minutes = 0 : minutes"
					> minutes
				</div>
				<button
					class="plus_minus"
					@click="minutes++"
				>+</button>
			</div>

			<div
				class="btns_inp"
				v-if="!isCounting"
			>
				<button
					class="plus_minus"
					@click="seconds--; handleSeconds()"
				>-</button>
				<div class="unit_input">
					<input
						type="number"
						v-model="seconds"
						class="num_input"
						@blur="seconds > 59 ? seconds = 0 : seconds"
					> seconds
				</div>
				<button
					class="plus_minus"
					@click="seconds++; handleSeconds()"
				>+</button>
			</div>

			<div
				class="time_disp"
				v-if="isCounting"
			>
				{{minutes_str}} : {{seconds_str}}
			</div>

			<div class="buttons">
				<button
					@click="countdown"
					:class="{'active':(isCounting)}"
				>
					Start countdown
				</button>
				<button @click="isCounting = false">
					Pause countdown
				</button>
			</div>
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
	computed: {
		seconds_str() {
			return this.seconds < 10 ? `0${this.seconds}` : this.seconds;
		},
		minutes_str() {
			return this.minutes < 10 ? `0${this.minutes}` : this.minutes
		}
	},
	methods: {
		countdown() {
			this.isCounting = true;
			if (this.seconds > 0 || this.minutes > 0) {
				setTimeout(() => {
					if (!this.isCounting) {
						return;
					} else {
						this.seconds -= 1;
						if (this.seconds < 0) {
							this.seconds = 59;
							this.minutes--;
						}
						this.countdown();
					}
				}, 1000);
			}
		},
		handleSeconds() {
			if (this.seconds < 0 && this.minutes > 0) {
				this.seconds = 59;
				this.minutes--;
			} else if (this.seconds < 0 && this.minutes === 0) {
				this.seconds = 0;
			} else if (this.seconds > 59) {
				this.seconds = 0;
				this.minutes++;
			}
		}
	},
	watch: {
		seconds: function () {
			if (this.seconds === 0 && this.minutes > 0 && this.isCounting) {
				setTimeout(() => {
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
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}

.time_disp {
	margin: 1em 0;
	font-size: 2em;
}

.active {
	background-color: #2de128;
	color: black;
}
</style>
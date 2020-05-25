<template>
	<div class="container">
		<div id="wrapper">
			<h1 class="title">
				律動 Trainer
			</h1>
			<h2 class="subtitle">
				A simple rhythm trainer &amp; practice journal
			</h2>

			<nav id="nav">
				<a
					@click="useMetronome = !useMetronome"
					class="link"
				>
					<h3>Metronome</h3>
				</a>

				<a
					@click="useTimer = !useTimer"
					class="link"
				>
					<h3>Timer</h3>
				</a>

				<a
					@click="useJournal = !useJournal"
					class="link"
				>
					<h3>Journal</h3>
				</a>

				<a
					@click="showInfo = !showInfo"
					class="link"
				>
					<h3>Info</h3>
				</a>
			</nav>

			<div class="comp_box">
				<Metronome
					class="component"
					v-if="useMetronome"
				/>
				<Timer
					class="component"
					v-if="useTimer"
				/>

			</div>

			<div class="comp_box">
				<Journal
					class="component"
					v-show="useJournal"
				/>
				<InfoBox
					class="component"
					v-if="showInfo"
				/>
			</div>
		</div>
	</div>
	</div>
</template>

<script>
import InfoBox from '@/components/InfoBox';
import Metronome from '@/components/Metronome';
import Journal from '@/components/Journal';
import Timer from '@/components/Timer';

export default {
	components: {
		InfoBox,
		Metronome,
		Journal,
		Timer
	},
	data() {
		return {
			useMetronome: false,
			useJournal: false,
			showInfo: false,
			useTimer: false
		}
	}
}
</script>

<style>
.container {
	margin: 0 auto;
	padding: 2% 0;
	min-height: 100vh;
	background: url("https://images.pexels.com/photos/161150/kiyomizu-dera-temple-kyoto-japan-161150.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
	background-attachment: fixed;
}

.subtitle {
	width: 90%;
	text-align: center;
}

#nav {
	margin: 1em 0;
	display: flex;
	flex-wrap: wrap;
	width: 90%;
	justify-content: space-around;
}

.link {
	width: 45%;
	text-align: center;
	text-decoration: none;
	border: 1px solid #2de128;
	padding: 0.5em;
	margin: 5px 0;
	cursor: pointer;
	background: rgba(34, 34, 34, 0.7);
	color: #2de128;
}

.link:hover {
	background-color: rgba(45, 225, 40, 0.3);
	color: black;
}

.component {
	width: 90%;
	margin: 1em auto;
}

.comp_box {
	width: 100%;
}

@media (min-width: 768px) {
	#nav {
		flex-wrap: no-wrap;
	}

	.link {
		width: 22%;
	}

	.comp_box {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-evenly;
	}

	.component {
		width: 49%;
	}
}
</style>

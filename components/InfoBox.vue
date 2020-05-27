<template>
	<div>
		<h2>About this app</h2>
		<p>This is a simple webapp designed to help you practice and keep a journal to track your progress.</p>

		<h3>Fair disclaimer</h3>
		<p>As stated, this is a <i>simple</i> webapp, it is not connected to a backend and was mostly made to fulfill my own needs, as well as serve as a learning project. I am aware that some features could have a better implementation, and that the journal can get quite... <i>cumbersome</i> (see below).</p>

		<p>Nevertheless, I hope you'll have fun and I'd like to thank you for checking this little app out. If you wish to contact me about bugs or any other reason, you can reach me at: <a href="mailto:alexviglione.dev@gmail.com"><b>alexviglione.dev@gmail.com</b></a></p>
		<p>Or visit <a href="https://alex-viglione.github.io/">my website</a>.</p>

		<h3 style="margin-bottom: 0.7em;">How it works</h3>
		<hr>
		<p><span class="bold_text">Metronome:</span> Select a bpm, the number of desired divisons in each measure, press "Start" and play along with it, press "Stop" to stop it whenever you want.</p>
		<hr>

		<p><span class="bold_text">Timer:</span> Select a desired duration, press "Start countdown" to do what it says on the tin, etc.</p>
		<p>Note: This is quite a simple timer, it will work but will not be accurate to the millisecond. I figured that was enough for the purposes of this app though.</p>
		<hr>

		<p><span class="bold_text">Journal:</span> Log your practice sessions every day/every time you use the app. Be aware that your data is not saved on a server, here's how you can keep a "persistent" journal:</p>

		<p>1. Write in "New entry" how your session went, then click "save entry" to temporarily save it (as long as you don't quit/refresh the page), and it will also display in "your logs" with the date</p>

		<p>2. When that's done and you want to retrieve your log(s), click on "Download your data", this will download a JSON file. You need just store it where you want, if you wish to do so.</p>

		<p>3. When you come back to the app later on, click "Load your data" to upload the JSON file and have it parsed and displayed in "Your logs"</p>
		<hr>
	</div>
</template>

<style scoped>
.bold_text {
	font-weight: bold;
}

a {
	text-decoration: none;
	color: #2de128;
	font-weight: bold;
}

a:visited {
	color: #299825;
}

a:hover {
	border-bottom: 1px solid #2de128;
	color: #2de128;
}

p {
	margin: 0.7em 0;
}

hr {
	border-color: #2de128;
}
</style>
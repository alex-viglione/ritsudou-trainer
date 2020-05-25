<template>
	<div class="container">
		<div id="wrapper">
			<h1 class="title">
				律動 Trainer
			</h1>
			<h2 class="subtitle">
				Error: This leads nowhere!
			</h2>

			<p>
				Back to -> <nuxt-link
					class="redirect"
					to="/"
				>the jam zone</nuxt-link>
			</p>

		</div>
	</div>
	</div>
</template>

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

.redirect {
	text-decoration: none;
	cursor: pointer;
	color: #2de128;
	font-weight: bold;
}

.redirect:hover {
	color: #2de128;
	border-bottom: 1px solid #2de128;
}
</style>

<template>
	<div>
		<nuxt />
	</div>
</template>

<style>
html {
	font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont,
		"Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
	font-size: 16px;
	word-spacing: 1px;
	-ms-text-size-adjust: 100%;
	-webkit-text-size-adjust: 100%;
	-moz-osx-font-smoothing: grayscale;
	-webkit-font-smoothing: antialiased;
	box-sizing: border-box;
}

*,
*:before,
*:after {
	box-sizing: border-box;
	margin: 0;
}

#wrapper {
	display: flex;
	width: 80%;
	margin: auto;
	padding: 0.75em;
	flex-direction: column;
	align-items: center;
	background-color: rgba(34, 34, 34, 0.8);
	color: #ccc;
}

button {
	background: rgba(34, 34, 34, 0.7);
	border: 1px solid #2de128;
	padding: 0.5em;
	cursor: pointer;
	color: #2de128;
	font-weight: bold;
	outline: none;
	font-size: 1em;
}

button:hover {
	background-color: rgba(45, 225, 40, 0.3);
	color: black;
}

button:active {
	background-color: #2de128;
	color: black;
}

.unit_input {
	display: flex;
	margin: auto;
	border-bottom: 1px solid #2de128;
	width: 170px;
	background: rgba(34, 34, 34, 0.7);
	padding: 3px 5px;
	font-size: 1.2em;
	align-items: center;
}

.num_input {
	background: none;
	border: none;
	width: 2em;
	text-align: center;
	margin-right: 1em;
	color: #2de128;
	outline: none;
	font-size: 1.2em;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
	-webkit-appearance: none;
	margin: 0;
}

input[type="number"] {
	-moz-appearance: textfield;
}

.buttons {
	margin: 1em 0;
}

.btns_inp {
	display: flex;
	margin: 0.5em 0;
}

.plus_minus {
	margin: 0 0.5em;
	width: 2.2em;
	font-weight: bold;
	font-size: 1.2em;
}

.disabled {
	opacity: 0.3;
	color: #333;
}

.disabled:hover {
	background-color: initial;
	color: #333;
}
</style>

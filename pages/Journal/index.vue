<template>
	<div>
		<div id="wrapper">
			<h1>Journal</h1>
			<nuxt-link to="/">To Home</nuxt-link>
			<div class="journal_page">
				<label for="Date">DATE:</label>
				<input
					type="date"
					name="Date"
					v-model="newDate"
				>
				<label for="placeholder">PLACEHOLDER:</label>
				<textarea
					name="placeholder"
					id=""
					cols="30"
					rows="10"
					v-model="newText"
				></textarea>
				<button @click="saveEntry(newDate, newText)">Save entry</button>
				<p>{{journalEntries}}</p>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			journalEntries: [],
			newDate: '',
			newText: ''
		}
	},
	methods: {
		saveEntry(date, text) {
			let newEntry = {};
			newEntry.date = date;
			newEntry.text = text;
			this.journalEntries.push(newEntry);
		}
	}
}
</script>

<style scoped>
.journal_page {
	display: flex;
	flex-direction: column;
}
</style>
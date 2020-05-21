<template>
	<div>
		<div id="journal">
			<h3>Journal</h3>
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

				<button @click="saveEntry(newDate, newText)">
					<h4>Save entry</h4>
				</button>

				<button>
					<input
						id="fileInput"
						type="file"
						name="file"
						v-show="false"
					/>
					<label
						for="fileInput"
						class="file_input_label"
					>
						<h4>Submit user data</h4>
					</label>
				</button>

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
		},
	}
}
</script>

<style scoped>
.journal_page {
	display: flex;
	flex-direction: column;
}

.file_input_label {
	cursor: pointer;
}
</style>
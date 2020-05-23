<template>
	<div>
		<div id="journal">
			<h3>Journal</h3>
			<!-- ===== View entries ===== -->
			<div class="journal_view_entries">
				<h4>Your logs:</h4>
				<div
					v-for="el in journalEntries"
					:key="el.id"
					v-show="el.id === counter"
				>
					<p>Date: {{el.day}} {{el.month}} {{el.year}}</p>
					<pre class="text_display">{{el.text}}</pre>
					<button @click="decreaseCounter">Previous page</button>
					<button @click="increaseCounter">Next page</button>
				</div>
			</div>

			<!-- ===== New entry ===== -->
			<div class="journal_new_entry">
				<h4>New entry:</h4>
				<label for="Date">DATE:</label>
				<label for="placeholder">PLACEHOLDER:</label>
				<textarea
					name="placeholder"
					id=""
					cols="30"
					rows="10"
					v-model="newText"
					class="text_insert"
				></textarea>

				<button @click="saveEntry(newText, id)">
					Save entry
				</button>

				<vue-blob-json-csv
					tag-name="button"
					file-type="json"
					file-name="practice_journal"
					title="Download your data"
					:data="journalEntries"
				/>

				<button>
					<input
						id="fileInput"
						type="file"
						name="file"
						v-show="false"
						@change="loadFromFile"
					/>
					<label
						for="fileInput"
						class="file_input_label"
					>
						Submit user data
					</label>
				</button>

			</div>
		</div>
	</div>
</template>

<script>
import Vue from 'vue';
import VueBlobJsonCsv from 'vue-blob-json-csv';

Vue.use(VueBlobJsonCsv);

export default {
	data() {
		return {
			journalEntries: [],
			newText: '',
			id: 1,
			counter: 1,
			monthNames: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
		}
	},
	methods: {
		saveEntry(text, id) {
			let newEntry = {};
			let newDate = new Date();
			newEntry.day = newDate.getDate();
			newEntry.month = this.monthNames[newDate.getMonth()];
			newEntry.year = newDate.getFullYear();
			newEntry.text = text;
			newEntry.id = id;
			this.journalEntries.push(newEntry);

			this.newTest = '';
			this.id++;
		},
		loadFromFile(ev) {
			this.journalEntries = [];
			const file = ev.target.files[0];
			const reader = new FileReader();

			reader.onload = e => {
				const submittedFile = e.target.result;
				const parsed = JSON.parse(submittedFile);
				parsed.forEach(el => this.journalEntries.push(el))
			};
			reader.readAsText(file);
		},
		increaseCounter() {
			if (this.counter + 1 > this.journalEntries.length) {
				return;
			} else {
				this.counter++;
			}
		},
		decreaseCounter() {
			if (this.counter === 1) {
				return;
			} else {
				this.counter--;
			}
		},
	},
}
</script>

<style scoped>
.journal_new_entry {
	display: flex;
	flex-direction: column;
}

.file_input_label {
	cursor: pointer;
}

.text_insert {
	white-space: pre-wrap;
}

/* .text_display {
	white-space: initial;
} */
</style>
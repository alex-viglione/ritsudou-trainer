<template>
	<div>
		<div id="journal">
			<h3>Journal</h3>
			<!-- ===== View entries ===== -->
			<div class="journal_view_entries">
				<h4>Your logs:</h4>
				<transition-group name="slide">
					<div
						v-for="el in journalEntries"
						:key="el.id"
						v-show="el.id === counter"
					>
						<p id="date">{{el.day}} {{el.month}} {{el.year}}</p>
						<pre class="text_display">{{el.text}}</pre>
					</div>
				</transition-group>
				<div
					class="log_btns"
					v-if="journalEntries.length > 1"
				>
					<button @click="decreaseCounter">Previous page</button>
					<p>Page {{counter}} / {{journalEntries.length}}</p>
					<button @click="increaseCounter">Next page</button>
				</div>
			</div>

			<!-- ===== New entry ===== -->
			<div class="journal_new_entry">
				<h4>New entry:</h4>
				<textarea
					name="placeholder"
					id=""
					cols="30"
					rows="10"
					v-model="newText"
					class="text_insert"
				></textarea>

				<div class="jrn_btns">
					<button
						class="jrn_btn"
						@click="saveEntry(newText, id)"
					>
						Save entry
					</button>

					<vue-blob-json-csv
						tag-name="button"
						class="jrn_btn"
						file-type="json"
						file-name="practice_journal"
						title="Download your data"
						:data="journalEntries"
					/>

					<button
						id="file_inp_btn"
						class="jrn_btn"
					>
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
			this.counter = this.journalEntries.length;
		},
		loadFromFile(ev) {
			this.journalEntries = [];
			const file = ev.target.files[0];
			const reader = new FileReader();

			reader.onload = e => {
				const submittedFile = e.target.result;
				const parsed = JSON.parse(submittedFile);
				parsed.forEach(el => {
					this.journalEntries.push(el);
					this.id++;
					this.counter = this.journalEntries.length;
				})
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
	display: block;
	padding: 0.5em;
}

.text_insert {
	white-space: pre-wrap;
	margin: 0.5em 0;
	background-color: black;
	color: white;
	border: 1px solid #2de128;
	resize: none;
	background-color: rgba(34, 34, 34, 0.8);
	outline: none;
}

.text_display {
	white-space: pre-wrap;
	font-style: italic;
	border: 1px solid #2de128;
	background-color: rgba(255, 255, 255, 0.3);
	color: black;
	padding: 0.5em;
}

#file_inp_btn {
	padding: 0;
}

/* .text_display {
	white-space: initial;
} */

.journal_view_entries {
	margin-top: 0.5em;
	margin-bottom: 1em;
}

.jrn_btns {
	display: flex;
	flex-direction: column;
}

.jrn_btn {
	margin: 0.2em 0;
}

#date {
	font-weight: bold;
	margin-top: 0.2em;
	color: #2de128;
}

.log_btns {
	margin-top: 0.5em;
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.log_btns button {
	width: 130px;
}

.slide-enter-active {
	animation: slide-in 0.5s forwards;
	/* transition: opacity 1.5s; */
}

.slide-leave {
	display: none;
}

@keyframes slide-in {
	from {
		transform: translateX(50px);
	}

	to {
		transform: translateX(0);
	}
}
</style>
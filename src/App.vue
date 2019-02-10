<template>
	<div id="app">

		<div class="container">
			<h1 class="has-text-centered is-size-3">Notes</h1>
			<Notes :notes="notes" @remove="deleteNote" @toggleedit="toggleEditNote" />
		</div>

		<nav class="navbar is-fixed-bottom">
			<div class="form container">
				<div class="columns full">
					<div class="column is-8"><input placeholder="Type an awesome note" ref="input" class="input" v-model="draft" @keyup.enter="addNote" /></div>
					<div class="column is-2">
						<div class="select full">
							<select class="full" v-model="selectedColor">
								<option>blue</option>
								<option>yellow</option>
								<option>pink</option>
							</select>
						</div>
					</div>
					<div class="column is-2"><button :disabled="!canAdd" class="button full" @click="addNote">Add note</button></div>
				</div>
			</div>
		</nav>

	</div>
</template>

<script>
	import Notes from './components/Notes.vue'

	export default {
		name: 'app',
		components: {
			Notes
		},
		mounted() {
			this.$refs.input.focus();
		},
		data() {
			return {
				draft: '',
				notes: [],
				selectedColor: 'yellow',
			}
		},
		computed: {
			canAdd: function() {
				return this.draft.length;
			}
		},
		methods: {
			addNote() {
				if(!this.canAdd) return false;
				let id = this.notes.length+1;
				this.notes.push({
					id,
					description: this.draft,
					background: this.selectedColor,
					editing: false,
				});
				this.draft = '';
			},
			deleteNote(id) {
				let index = this.notes.findIndex(note => note.id == id);
				if(index>=0) this.notes.splice(index, 1);
			},
			toggleEditNote(id) {
				let index = this.notes.findIndex(note => note.id == id);
				this.notes[index].editing=!this.notes[index].editing;
			}
		}
	}
</script>

<style lang="scss">
html, body {
	height: 100%;
}
h1 {
	padding: 1em 0;
}
.full {
	width: 100%;
}
nav.navbar {
	padding-top: 1em;
	background-color: #eee;
}
</style>

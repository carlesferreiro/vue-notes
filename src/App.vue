<template>
	<div id="app">

		<div class="container">
			<h1 class="has-text-centered is-size-3">Notes importants</h1>
			<Notes :notes="notes" @remove="deleteNote" />
		</div>

		<nav class="navbar is-fixed-bottom">
			<div class="form container">
				<div class="columns full">
					<div class="column is-8"><input class="input" v-model="draft" @keyup.enter="addNote" /></div>
					<div class="column is-2">
						<div class="select">
							<select v-model="selectedColor">
								<option>blue</option>
								<option>yellow</option>
								<option>pink</option>
							</select>
						</div>
					</div>
					<div class="column is-2"><button class="button full" @click="addNote">Afegir</button></div>
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
		data() {
			return {
				draft: '',
				notes: [],
				selectedColor: 'yellow',
			}
		},
		methods: {
			addNote() {
				let id = this.notes.length+1;
				this.notes.push({
					id,
					description: this.draft,
					background: this.selectedColor,
				});
				this.draft = '';
			},
			deleteNote(id) {
				let index = this.notes.findIndex(note => note.id == id);
				if(index>=0) this.notes.splice(index, 1);
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

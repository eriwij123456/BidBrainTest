<template>
	<div class="bg-gradient-to-l from-gray-600 to-gray-400 fixed w-screen h-screen flex overflow-y-auto flex-col">
		<div class="min-w-0 mx-auto my-2">
			<input v-model="searchQuery" type="text" placeholder="Search..." class="block w-full px-4 py-3 rounded-md border-0 text-base text-gray-900 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-cyan-400 focus:ring-offset-gray-900">
		</div>
		<div class="mx-auto w-3/4 sm:w-2/3 px-4 py-4">
			<div class="grid grid-cols-2 sm:grid-cols-3 gap-4 sm:gap-6">
				<div @click="openMovie(bond)" class="flex-1 flex flex-col p-4 sm:p-8 bg-white rounded-md text-center hover:opacity-75 cursor-pointer" v-for="bond in filteredList" :key="bond">
					<img class="w-16 h-16 sm:w-32 sm:h-32 flex-shrink-0 mx-auto rounded-full mb-2" src="https://bit.ly/3EIwWVE" alt="">
					<p class="text-xs sm:text-sm font-bold">{{ bond.title }}</p>
				</div>
				<Moviecard v-if="dialog" @closeDialog="closeDialog()" :movie="selectedMovie"/>
			</div>
		</div>
	</div>
</template>

<script>

import Moviecard from './components/Moviecard.vue'
import movies from '../data/movies.json'
import _ from 'underscore'


export default {
  	name: 'App',
  	data() {
		return {	
			movies: movies,
			sortable: [],
			searchQuery: null,
			dialog: false,
			selectedMovie: null
		}
  	},

  	components: {
		Moviecard,
  	},

	props: {
	},

	computed: {
		filteredList(){
			if (this.searchQuery){
				return this.sortable.filter((bond)=>{
					return this.searchQuery.toLowerCase().split(' ').every(v => bond.title.toLowerCase().includes(v))
				})
			} else {
				return this.sortable;
			}
		}
  	},

	mounted () {
		this.sortable = _.values(movies)
		this.sortable = _.flatten(this.sortable, false)
		this.sortable = (this.sortable.sort(function (a, b) {
			return b.year - a.year;
		}))
  	},

	methods: {
		openMovie (bond) {
			console.log();
			this.selectedMovie = bond
			this.dialog = true
		},

		closeDialog () {
			this.dialog = false
		}
	},
}
</script>
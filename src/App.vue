<template>
	<div class="bg-gradient-to-l from-gray-600 to-gray-400 fixed w-screen h-screen flex overflow-y-auto flex-col">
		<div class="min-w-0 mx-auto mt-6 mb-4">
			<input v-model="searchQuery" type="text" placeholder="Search..." class="block w-full px-4 py-3 rounded-md border-0 text-base text-gray-900 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-cyan-400 focus:ring-offset-gray-900">
		</div>
		<div class="mx-auto w-full xl:w-2/3 px-4 py-4">
			<div class="grid grid-cols-2 sm:grid-cols-3 gap-4 sm:gap-6 lg:h-2/3 sm:w-2/3 mx-auto">
				<div @click="openMovie(bond)" v-for="bond in filteredList" :key="bond" class="hover:opacity-75 cursor-pointer">
					<p class="hidden lg:block text-sm font-bold text-center bg-gray-50 rounded-t-md py-2 text-lg">{{ bond.title }}</p>
					<div class="flex-1 flex flex-col p-4 lg:p-6 bg-gray-50 rounded-md lg:rounded-t-none text-center overflow-hidden h-full lg:h-auto">
						<img v-if="bond.image" class="hidden lg:block w-full h-full flex-shrink-0 mx-auto transform rotate-6" :src="bond.image">
						<div v-else class="animate-pulse flex justify-center h-full w-full">
							<div class="rounded-md bg-indigo-200 p-20 transform rotate-6"></div>
						</div>
						<img class="w-16 h-16 lg:hidden flex-shrink-0 mx-auto rounded-full" src="https://bit.ly/3EIwWVE">
						<p class="lg:hidden text-xs sm:text-sm font-bold my-2 items-end">{{ bond.title }}</p>
					</div>
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
					this.mergedStrings = bond.title + bond.actor + bond.director + bond.year.toString()
					return this.searchQuery.toLowerCase().split(' ').every(v => this.mergedStrings.toLowerCase().includes(v))
					// return this.searchQuery.toLowerCase().split(' ').every(v => bond.title.toLowerCase().includes(v) || bond.director.toLowerCase().includes(v) || bond.actor.toLowerCase().includes(v))
				})



			} else {
				return this.sortable;
			}
		}
  	},

	mounted () {
		this.sortable = _.flatten(_.values(movies), false)
		this.sortable.sort(function (a, b) {
			return b.year - a.year;
		})
  	},

	methods: {
		openMovie (bond) {
			this.selectedMovie = bond
			this.dialog = true
		},

		closeDialog () {
			this.dialog = false
		}
	},
}
</script>
<template>
	<div class="bg-gradient-to-l from-gray-600 to-gray-400 fixed w-screen h-screen flex justify-between overflow-y-auto">
		<div class="mx-auto my-auto px-4 py-4">
			<div class="grid grid-cols-2 sm:grid-cols-3 gap-4 sm:gap-6" v-for="movie in movies" :key="movie">
				<div  class="flex-1 flex flex-col p-4 sm:p-8 bg-white rounded-md text-center" v-for="bond in movie" :key="bond">
					<img class="w-16 h-16 sm:w-32 sm:h-32 flex-shrink-0 mx-auto rounded-full mb-2" src="https://bit.ly/3EIwWVE" alt="">
					<p class="text-xs sm:text-sm font-bold">{{ bond.title }}</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>

import movies from '../data/movies.json'


export default {
  	name: 'App',
  	data() {
		return {	
			movies: movies,
		}
  	},

  	components: {
		
  	},

	props: {
	},

	computed: {
  	},

	mounted () {
  	},

	methods: {
	},
}
</script>
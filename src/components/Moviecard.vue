<template>
<div class="fixed z-10 inset-0 overflow-y-scroll" aria-labelledby="modal-title" role="dialog" aria-modal="true">
	<div class="flex items-center justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
		<div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>
		<span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
		<div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-sm sm:w-full sm:p-6">
			<p class="absolute top-2 right-4 font-bold text-gray-600 cursor-pointer" @click="closeDialog()">X</p>
			<div>
				<img class="w-16 h-16 sm:w-32 sm:h-32 flex-shrink-0 mx-auto rounded-full mb-2" src="https://bit.ly/3EIwWVE" alt="">
				<div class="mt-3 text-center sm:mt-5">
					<h3 class="text-lg leading-6 font-medium text-gray-900" id="modal-title">
						{{movie.title}}
					</h3>
					<div class="mt-2">
						<p class="text-sm text-gray-500">
							Director: {{movie.director}}
						</p>
						<p class="text-sm text-gray-500">
							Bond: {{movie.actor}}
						</p>
						<p class="text-sm text-gray-500">
							Year: {{movie.year}}
						</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
</template>

<script>

import _ from 'underscore'

export default {
  	data() {
		return {
		}
  	},

	props: {
		movie: { 
			required: false 
		}
	},

  	components: {
		
  	},

	computed: {
  	},

	mounted () {
		console.log(this.movie);
  	},

	methods: {
		closeDialog() {
			this.$emit('closeDialog')
		}
	},
}
</script>

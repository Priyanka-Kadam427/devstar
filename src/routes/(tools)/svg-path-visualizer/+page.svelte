<script lang="ts">
	import { Button, Input, Textarea } from 'flowbite-svelte';
  
	let pathData = 'M10 10 H 90 V 90 H 10 Z'; // Default path data
	let pathEditor = pathData;
  
	function updatePath() {
	  pathData = pathEditor.trim();
	}
  
	function resetPath() {
	  pathEditor = 'M10 10 H 90 V 90 H 10 Z';  // Default to a simple rectangle
	  pathData = pathEditor;
	}
  </script>
  
  <section class="bg-white dark:bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:px-12">
	  <div class="card p-8 relative items-center mx-auto max-w-screen-xl overflow-hidden rounded-lg">
		<div class="gap-4 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden">
		  
		  <!-- Path Editor -->
		  <div class="rounded-lg overflow-hidden bg-gray-50 border border-gray-300">
			<Textarea
			  placeholder="Enter SVG path data"
			  rows="8"
			  bind:value={pathEditor}
			  class="resize-none block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
			/>
		  </div>
  
		  <!-- Path Visualizer -->
		  <div class="rounded-lg overflow-hidden bg-gray-50 border border-gray-300">
			<svg xmlns="http://www.w3.org/2000/svg" class="w-full h-48 border border-gray-300 rounded-md bg-white">
			  <path d={pathData} stroke="black" fill="transparent" stroke-width="1.5" />
			</svg>
		  </div>
  
		</div>
  
		<div class="items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-1 overflow-hidden">
		  <div class="mt-8 gap-4 items-center mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 overflow-hidden">
			<!-- Update Button -->
			<Button
			  color="blue"
			  on:click={updatePath}
			  class="w-full"
			>
			  Update Path
			</Button>
  
			<!-- Reset Button -->
			<Button
			  color="blue"
			  on:click={resetPath}
			  class="w-full"
			>
			  Reset Path
			</Button>
		  </div>  
		</div>
  
	  </div>
	</div>
  </section>
  
<script lang="ts">
	import { Button, Input, Textarea, Card, Label } from 'flowbite-svelte';
	
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
  
  <section class="bg-white dark:bg-gray-800">
	<div class="py-10 px-6 mx-auto max-w-screen-xl lg:px-16">
	  <Card class="max-w-md mx-auto">
		<h5 class="text-lg font-bold mb-2">SVG Path Visualizer</h5>
		<div class="grid grid-cols-1 gap-6">
		  <Label for="path-editor" value="Enter SVG path data" />
		  <Textarea
			id="path-editor"
			placeholder="Enter SVG path data"
			rows="10"
			bind:value={pathEditor}
			class="resize-none block p-3 w-full text-sm text-gray-700 bg-gray-100 rounded-lg border border-gray-200 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-300 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
		  />
		</div>
		<div class="grid grid-cols-1 gap-6 mt-6">
		  <Label for="path-visualizer" value="Path Visualizer" />
		  <div class="rounded-lg overflow-hidden bg-gray-100 border border-gray-200">
			<svg xmlns="http://www.w3.org/2000/svg" class="w-full h-60 border border-gray-200 rounded-md bg-white">
			  <path d={pathData} stroke="black" fill="transparent" stroke-width="2" />
			</svg>
		  </div>
		</div>
		<div class="flex justify-end gap-2 mt-6">
		  <Button
			color="blue"
			on:click={updatePath}
		  >
			Update Path
		  </Button>
		  <Button
			color="blue"
			on:click={resetPath}
		  >
			Reset Path
		  </Button>
		</div>
	  </Card>
	</div>
  </section>
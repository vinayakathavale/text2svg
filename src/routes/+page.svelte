<script>
	import { onMount } from 'svelte';
	let text = '';
	let svgContent = '';
  
	function generateSVG() {
	  const width = text.length * 50; // Adjust the factor as needed
	  svgContent = `<svg xmlns="http://www.w3.org/2000/svg" width="${width}" height="200">
		<text x="50%" y="50%" >${text}</text>
	  </svg>`;
	}
  
	function downloadSVG() {
	  const blob = new Blob([svgContent], { type: 'image/svg+xml;charset=utf-8' });
	  const url = URL.createObjectURL(blob);
	  const link = document.createElement('a');
	  link.href = url;
	  link.download = 'text.svg';
	  link.click();
	}
  
	onMount(() => {
	  generateSVG();
	});
</script>
  
<div>
	Convert text to SVG <br> <br>

	<input type="text" bind:value={text} on:input={generateSVG} />
	<button on:click={downloadSVG}>Download SVG</button>
	<br> <br>
	<div>
	  Rendered SVG:  <br>
	  	{@html svgContent}
	</div>
	<!-- Add a new preformatted text element to display the SVG content as text -->
	<div> 
		RAW SVG: 
		{svgContent}
	</div>
</div>
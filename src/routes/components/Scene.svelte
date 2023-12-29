<script lang="ts">
	import * as Threlte from '@threlte/core';
	import * as Three from 'three';
	import { GLTF, Grid, OrbitControls, interactivity } from '@threlte/extras';
	import { browser } from '$app/environment';
	import Sphere from './Sphere.svelte';
	import { Pane } from 'tweakpane';
	import Ghost from './ghost.svelte';

	const background = {
		position: {
			x: -6.4,
			y: 0.8,
			z: 2.6
		}
	};

	// if (browser) {
	// 	const pane = new Pane({
	// 		title: 'Scene'
	// 	});
	// 	const backgroundControls = pane.addFolder({
	// 		title: 'background',
      
	// 	});
	// 	backgroundControls.addBinding(background, 'position', {
	// 		multiline: true,
	// 		bufferSize: 3
	// 	});
	// 	backgroundControls.on('change', (ev) => {
	// 		background.position = ev.value as any;
	// 		console.log(background.position);
	// 	});
	// }

	let camera = {
		position: [10, 6, 10],
    makeDefault: true,
    zoom: 50,
	};

	
</script>


<Threlte.T.AmbientLight 
intensity={19} 
color={"#0e0e33"} />


<Sphere />
<Ghost color={"#FFFABF"}/>
<Threlte.T.OrthographicCamera
	{...camera}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
>
	<OrbitControls />
</Threlte.T.OrthographicCamera>


<GLTF
	url={'/models/forest_diorama.glb'}
	position={[background.position.x, background.position.y, background.position.z]}
	scale={0.03}
	rotation={[0, 90, 0]}
/>

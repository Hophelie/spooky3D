<!-- 
    GETTING STARTED -- https://threlte.xyz/docs/learn/getting-started/your-first-scene
    <script lang="ts">
	import * as Threlte from '@threlte/core';
	import * as Three from 'three';
	import { interactivity } from '@threlte/extras';
	import { spring } from 'svelte/motion';

	interactivity();
	const scale = spring(1);

	let rotation = 0;
	Threlte.useTask((delta) => {
		rotation += delta;
	});
</script>

<Threlte.T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 1, 0);
	}}
/>

<Threlte.T.DirectionalLight 
    position={[0, 10, 10]} 
    castShadow />

<Threlte.T.Mesh
	rotation.y={rotation}
	position.y={1}
	scale={$scale}
	on:pointerenter={() => scale.set(1.5)}
	on:pointerleave={() => scale.set(1)}
    castShadow
>
	<Threlte.T.BoxGeometry args={[2, 3, 2]} />
	<Threlte.T.MeshStandardMaterial color="skyblue" />

</Threlte.T.Mesh>

<Threlte.T.Mesh
  rotation.x={-Math.PI / 2}
  receiveShadow
>
  <Threlte.T.CircleGeometry args={[5, 40]} />
  <Threlte.T.MeshStandardMaterial color="white" />
</Threlte.T.Mesh> -->

<script lang="ts">
	import * as Threlte from '@threlte/core';
	import * as Three from 'three';
	import * as Utils from 'three/src/math/MathUtils';
	import { GLTF, Grid, OrbitControls, interactivity } from '@threlte/extras';
	import { browser } from '$app/environment';
	import { Pane } from 'tweakpane';

	const sphere = {
		position: {
			x:-6.70,
			y:3.20,
			z: -4
		}
	};
	let moonLight = {
		position: {
			x: sphere.position.x,
			y: sphere.position.y,
			z: sphere.position.z
		},
		intensity:3
	};
	// if (browser) {
	// 	const pane = new Pane({
	// 		title: 'Scene'
	// 	});
	// 	const moon = pane.addFolder({
	// 		title: 'Moon'
	// 	});
	// 	moon.addBinding(sphere, 'position', {
	// 		multiline: true,
	// 		bufferSize: 3
	// 	});
	// 	moon.on('change', (ev) => {
	// 		sphere.position = ev.value as any;
	// 	});
	// 	const moonLightControls = pane.addFolder({
	// 		title: 'MoonLight'
	// 	});
	// 	moonLightControls.addBinding(moonLight, 'position', {
	// 		multiline: true,
	// 		bufferSize: 3
	// 	});
	// 	moonLightControls.addBinding(moonLight, 'intensity')
	// 	moonLightControls.on('change', (ev) => {
	// 		console.log(ev.value instanceof Object);
	// 		if (ev.value instanceof Object ) {
	// 			moonLight.position = ev.value as any;
	// 			 }else{
	// 				moonLight.intensity = ev.value as any;
	// 		 }
			
	// 	});
	// }

</script>

<Threlte.T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	on:create={({ ref }) => {
		ref.lookAt(0, 0, 0);
	}}
>
	<OrbitControls />
</Threlte.T.PerspectiveCamera>

<Threlte.T.DirectionalLight
	position={[moonLight.position.x, moonLight.position.y, moonLight.position.z]}
	color={'#FFFABF'}
	intensity={moonLight.intensity}
	isDirectionalLight
	castShadow
/>


<Threlte.T.Mesh position={[sphere.position.x, sphere.position.y, sphere.position.z]}>
	<Threlte.T.SphereGeometry args={[1]} />
	<Threlte.T.MeshBasicMaterial color="#FFFABF" />
</Threlte.T.Mesh>

<!-- <Grid cellColor="#FE3D00" sectionColor="#FE3D00" />  -->

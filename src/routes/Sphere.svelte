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
			x: 0.40000000000000036,
			y: 4.199999999999999,
			z: -4.2
		}
	};

	if (browser) {
		const pane = new Pane({
			title: 'Scene'
		});
		const sphereControls = pane.addFolder({
			title: 'Sphere'
		});
		sphereControls.addBinding(sphere, 'position', {
			multiline: true,
			bufferSize: 3
		});
		sphereControls.on('change', (ev) => {
			sphere.position = ev.value as any;
			console.log(sphere.position);
		});
	}
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

<Threlte.T.DirectionalLight position={[3, 10, 7]} color={'#0D163D'} intensity={60} />

<Threlte.T.Mesh position={[sphere.position.x, sphere.position.y, sphere.position.z]}>
	<Threlte.T.SphereGeometry args={[1]} />
	<Threlte.T.MeshStandardMaterial color="skyblue" />
</Threlte.T.Mesh>

<!-- <Grid cellColor="#FE3D00" sectionColor="#FE3D00" />  -->

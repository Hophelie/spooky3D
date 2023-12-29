<script lang="ts">
	import * as Threlte from '@threlte/core';
	import * as Three from 'three';
	import { GLTF, Grid, OrbitControls, interactivity } from '@threlte/extras';
	import { browser } from '$app/environment';
    import  Sphere  from './Sphere.svelte';
    import { Pane } from 'tweakpane';

	const background = {
		position: {
            x: -6.40,
            y: 0.80,
            z: 2.6
        }
	};

	if (browser) {
		const pane = new Pane({
			title: 'background'
		});
		const backgroundControls = pane.addFolder({
			title: 'background'
		});
        backgroundControls.addBinding(background, 'position', {
            multiline: true,
            bufferSize: 3,
        });
        backgroundControls.on('change', (ev) => {
            background.position = ev.value as any;
            console.log(background.position);
        });
	}
	

	if (browser) {
		// const pane = new Pane({
		// 	title: 'Scene'
		// });
		// const sphereControls = pane.addFolder({
		// 	title: 'Sphere'
		// });
        // sphereControls.addBinding(sphere, 'position', {
        //     multiline: true,
        //     bufferSize: 3,
        // });
        // sphereControls.on('change', (ev) => {
        //     sphere.position = ev.value as any;
        //     console.log(sphere.position);
        // });
	}

    
    let camera   = {
        position:[0, 0,10]
       
    } 
    let pointLight = {
    position: [0, 10, 10],
    color: 'hsl(0, 100%, 100%)',
    }   
    let ghost = {
        position:[0, 2.85, 0],
        scale:0.4,
        rotation:[0, 0, 0]
    }

</script>
<Threlte.T.AmbientLight color="#000000" intensity={3} />

<Sphere />
<Threlte.T.OrthographicCamera
makeDefault
zoom={50}
position={[10, 6, 10]}
on:create={({ ref }) => {
    ref.lookAt(0, 0, 0);
}}
>
<OrbitControls />
</Threlte.T.OrthographicCamera>




<GLTF
  url={'/models/ghost.glb'}
  {...ghost}
/>
<GLTF
  url={'/models/forest_diorama.glb'}
    position={[background.position.x, background.position.y, background.position.z]}
    scale={0.03}
    rotation={[0, 90, 0]}
/>



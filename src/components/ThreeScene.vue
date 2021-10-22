<script setup>
import { onMounted } from '@vue/runtime-core';
import {ref} from 'vue'
import * as THREE from 'three'
import OrbitControls from 'three-orbitcontrols'

defineProps({
  
})

let camera = ref(null);
let scene = ref(null);
let renderer = ref(null);
let geometry= ref(null);
let material= ref(null); 
let mesh= ref(null);

camera = new THREE.PerspectiveCamera( 70, window.innerWidth / window.innerHeight, 0.01, 10 );
camera.position.z = 1;

scene = new THREE.Scene();

geometry = new THREE.BoxGeometry( 0.2, 0.2, 0.2 );
material = new THREE.MeshNormalMaterial();

mesh = new THREE.Mesh( geometry, material );
scene.add( mesh );

renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setSize( window.innerWidth, window.innerHeight ); 


let controls = new OrbitControls(camera, renderer.domElement);


function animate() {
  // mesh.rotation.x += 0.001;
  mesh.rotation.y += 0.01;
	requestAnimationFrame( animate );
	renderer.render( scene, camera );
}


onMounted(()=>{
  animate();
  document.getElementById('ThreeScenceMain').appendChild(renderer.domElement);
})
</script>

<template>
  <div id="ThreeScenceMain"></div>
</template>

<style scoped>
#ThreeScenceMain{
  width: 100%;
  height: 100%;
}
</style>

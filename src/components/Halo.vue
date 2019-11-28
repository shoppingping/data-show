<!-- 问题：添加不进去地球图片 -->
<template>

  <div id="canvas" class="earth" ref="chartdiv">
  </div>
  
</template>


<script>

import * as THREE from "three";

export default {

  data: function () {
    return {
      renderer: new THREE.WebGLRenderer({antialias: true,alpha: true}),
      camera: new THREE.PerspectiveCamera(35, window.innerWidth / window.innerHeight, 1, 1000),
      scene: new THREE.Scene(),
      group: null,
      halo: new THREE.Object3D(),
      particle: new THREE.Object3D(),
      luminor: new THREE.Object3D(),
      lights: [],
    }
  },

  mounted: function () {
    this.init();
    this.animate();
  },

  methods: {

    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight *2;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },

    init() {
      this.initRenderer();
      this.initCamera();
      this.initGlobal();
      this.initHalo();
      this.initPartical();
      this.initLight();

      window.addEventListener('resize', this.onWindowResize, false);

    },

    initRenderer(){
      this.renderer.setPixelRatio((window.devicePixelRatio) ? window.devicePixelRatio : 1);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.autoClear = false;
      this.renderer.setClearColor(0x000000, 1.0);
      document.getElementById('canvas').appendChild(this.renderer.domElement);
    },

    initCamera(){
      this.camera.position.z = 400;
      this.scene.add(this.camera);
    },

    initGlobal(){

      this.group = new THREE.Group();
      // this.group.scale.set(1.2,1.2,1.2);
      this.group.position.set(0,-200,0);
      this.scene.add(this.group);

      let globeTextureLoader = new THREE.TextureLoader();
      globeTextureLoader.load('./assets/img/world.svg',  (texture) => {
        let globeGgeometry = new THREE.SphereGeometry(240, 100, 100);
        let globeMaterial = new THREE.MeshStandardMaterial({map: texture});
        let globeMesh = new THREE.Mesh(globeGgeometry, globeMaterial);
        this.group.add(globeMesh);
        // this.group.rotation.x = THREE.Math.degToRad(35);
        // this.group.rotation.y = THREE.Math.degToRad(170);
      });
    },

    initHalo(){

      var geom3 = new THREE.SphereGeometry(240, 120, 120);
      var mat3 = new THREE.ShaderMaterial({
        uniforms: {},
        // vertexShader: document.getElementById('vertexShader').textContent,
        vertexShader: 'varying vec3 vNormal; void main() { vNormal = normalize( normalMatrix * normal ); gl_Position = projectionMatrix * modelViewMatrix * vec4( position, 1.0 ); }',
        // fragmentShader: document.getElementById('fragmentShader').textContent,
        fragmentShader: 'varying vec3 vNormal; void main() { float intensity = pow( 0.7 - dot( vNormal, vec3( 0.0, 0.0, 0.5 ) ), 4.0 ); gl_FragColor = vec4( 1.3, 1.0, 1.0, 1.0 ) * intensity; }',
        side: THREE.BackSide,
        blending: THREE.AdditiveBlending,
        transparent: true
      });

      var sun = new THREE.Mesh(geom3, mat3);
      sun.position.set(0,-300,0);
      sun.scale.set(1.6,1.6,1.6);
      this.halo.add(sun);
      
      var sun2 = new THREE.Mesh(geom3, mat3);
      sun2.position.set(10,-285,1)
      sun2.scale.set(1.2,1.2,1.2);
      this.halo.add(sun2);
      
      this.scene.add(this.halo);
    },

    initPartical(){
      var geometry = new THREE.TetrahedronGeometry(1, 1);
      var material = new THREE.MeshPhongMaterial({
        color: 0xFFD700,
        // shading: THREE.FlatShading,
      });

     for (var i = 0; i < 500; i++) {
        var mesh = new THREE.Mesh(geometry, material);
        mesh.position.set(Math.random() - 0.5, Math.random() - 0.5, Math.random() - 0.5).normalize();
        mesh.position.multiplyScalar( 200 + (Math.random() * 500));
        mesh.rotation.set(Math.random() * 2, Math.random() * 2, Math.random() * 2);
        this.particle.add(mesh);
      }
      
      this.scene.add(this.particle);
    },


    initLight(){

      // let ambientLight = new THREE.AmbientLight(0x000000);
      // this.scene.add(ambientLight);
      
      let hemiLight = new THREE.HemisphereLight(0x000000, 0x1111111, 20);
      hemiLight.position.set(-1, -1, 2);
      this.luminor.add(hemiLight);
      this.scene.add(this.luminor);
     
      // this.lights[1] = new THREE.DirectionalLight(0x000000, 7);
      // this.lights[1].position.set(-1, 0, 0.5);
      // this.lights[2] = new THREE.DirectionalLight(0x000000, 7);
      // this.lights[2].position.set(1, 0, 0.5);
      // this.scene.add(this.lights[1]);
      // this.scene.add(this.lights[2]);






      // 位于场景正上方的光源，颜色从天空颜色渐变为地面颜色。
      let light = new THREE.HemisphereLight(0xffffbb, 0x080820, 1);
      this.scene.add(light);

      // 环境光
      // let light2 = new THREE.AmbientLight(0xFFFFFF);
      // light2.position.set(100, 100, 200);
      // this.scene.add(light2);

      // 平行光
      // 位置不同，方向光作用于物体的面也不同，看到的物体各个面的颜色也不一样
      // let light3 = new THREE.DirectionalLight(0xffffbb, 1);
      // light3.position.set(-1, 1, 1);
      // this.scene.add(light3);
    },


    animate() {
      // var timer = 0.0001 * Date.now();
      requestAnimationFrame(this.animate);

      // this.particle.rotation.x += 0.0000;
      this.particle.rotation.y -= 0.0040;
      this.group.rotation.y += 0.002;
       
      this.renderer.clear();
      this.renderer.render(this.scene, this.camera)
    },
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.earth {
  // position: relative;
  // width: 160%;
  // height: 100%;
  // bottom: 0;
  // height: 2300px;
  // top: 200px;
  // left: -30%;
}


</style>

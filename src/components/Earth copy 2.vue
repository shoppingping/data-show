<template>

  <div id="canvas">
  </div>
  
</template>


<script>

import * as THREE from "three";

export default {

  data: function () {
    return {
      // width: document.getElementById('canvas').clientWidth,
      // height: document.getElementById('canvas').clientHeight,
      width: 200,
      height: 100,
      // stats: null,
      camera: new THREE.PerspectiveCamera(30, this.width / this.height, 1, 10000),
      renderer: new THREE.WebGLRenderer({
            antialias: true,
            alpha: true,
            canvas: this.renderer
        }),
      particle: new THREE.Object3D(),
      scene: new THREE.Scene(),
      light: {
        luminor: new THREE.Object3D(),
      },
      earthMesh: null,
      cloudsMesh: null,
      halo: new THREE.Object3D(),
      controls: null,
      circle: new THREE.Object3D(),
      luminor: new THREE.Object3D(),
    }
  },

  mounted: function () {
    this.init();
    // this.animate();
  },

  methods: {

    // 帧蘋
    // initStats() {
    //   this.stats = new Stats();
    //   document.getElementById('canvas').appendChild(this.stats.dom);
    // },

    // 渲染器
    initThree() {
        // width = 2000;
        // height = 2000;
        this.renderer.setSize(this.width, this.height);
        document.getElementById('canvas').appendChild(this.renderer.domElement);
        this.renderer.setClearColor(0x000000, 1.0);
    },

    // 相机
    initCamera() {
        // 透视相机 视角越大，看到的场景越大，那么中间的物体相对于整个场景来说，就越小了
        this.camera.position.x = -500;
        this.camera.position.y = 500;
        this.camera.position.z = -500;
        this.camera.lookAt({ x: 0.6, y: 0, z: 0 });
    },

    // // 场景
    // var scene;
    // function initScene() {
    //     scene = new THREE.Scene();
    // }

    // 光源

    initLight() {

        // A light source positioned directly above the scene, with color fading from the sky color to the ground color. 
        // 位于场景正上方的光源，颜色从天空颜色渐变为地面颜色。
        //  var light = new THREE.HemisphereLight(0xffffbb, 0x080820, 1);
        // scene.add(light);

        // 环境光
        // light = new THREE.AmbientLight(0xFFFFFF);
        // light.position.set(100, 100, 200);
        // scene.add(light);

        // 平行光
        // 位置不同，方向光作用于物体的面也不同，看到的物体各个面的颜色也不一样
        // light = new THREE.DirectionalLight(0xffffbb, 1);
        // light.position.set(-1, 1, 1);
        // scene.add(light);






        // 环境光
        // var ambientLight = new THREE.AmbientLight(0x000000);
        // scene.add(ambientLight);

        // 上方光
        this.light.luminor = new THREE.Object3D();
        // var hemiLight = new THREE.HemisphereLight(0x000000, 0x1111111, 30);
        let hemiLight = new THREE.HemisphereLight(0xffffbb, 0x080820, 1);
        // hemiLight.position.set(-1, -1, 2);
        hemiLight.position.set(-1, 1, 2);
        this.light.luminor.add(hemiLight);

        this.scene.add(this.light.luminor)


        // 平行光
        // lights[1] = new THREE.DirectionalLight(0x000000, 7);
        // lights[1].position.set(-1, 0, 0.5);
        // lights[2] = new THREE.DirectionalLight(0x000000, 7);
        // lights[2].position.set(1, 0, 0.5);
        // scene.add(lights[1]);
        // scene.add(lights[2]);
    },

    // 地球
    initEarth() {
        var earthGeo = new THREE.SphereGeometry(500, 100, 100);
        var earthMater = new THREE.MeshPhongMaterial({
            map: new THREE.TextureLoader().load('https://raw.githubusercontent.com/jiangyuzhen/three-earth/master/assets/earth.jpg'),
            // map: new THREE.TextureLoader().load('../assets/bg/world09.svg'),
            side: THREE.DoubleSide
        });
        this.earthMesh = new THREE.Mesh(earthGeo, earthMater);
        this.earthMesh.scale.set(1.4,1.4,1.4);
        this.earthMesh.position.y = -790;
        this.earthMesh.rotation.z = 0.5
        this.scene.add(this.earthMesh);
    },

    // 云

    initClouds() {
        var cloudsGeo = new THREE.SphereGeometry(512, 100, 100);
        var cloudsMater = new THREE.MeshPhongMaterial({
            alphaMap: new THREE.TextureLoader().load('https://raw.githubusercontent.com/jiangyuzhen/three-earth/master/assets/clouds.jpg'),
            transparent: true,
            opacity: 0.9
        });
        this.cloudsMesh = new THREE.Mesh(cloudsGeo, cloudsMater);
        this.cloudsMesh.position.y = -490;
        // mesh.rotation.set()
        this.cloudsMesh.rotation.x = 0.9
        this.scene.add(this.cloudsMesh);
    },



    initHalo() {
        // 添加太阳

        // 背景光
        var geom3 = new THREE.SphereGeometry(512, 100, 100);
        var mat3 = new THREE.ShaderMaterial({
          uniforms: {},
          vertexShader: 'varying vec3 vNormal; void main() { vNormal = normalize( normalMatrix * normal ); gl_Position = projectionMatrix * modelViewMatrix * vec4( position, 1.0 ); }',
          fragmentShader: 'varying vec3 vNormal; void main() { float intensity = pow( 0.7 - dot( vNormal, vec3( 0.0, 0.0, 0.5 ) ), 9.0 ); gl_FragColor = vec4( 1.3, 1.0, 1.0, 1.0 ) * intensity; }',
          side: THREE.BackSide,
          blending: THREE.AdditiveBlending,
          transparent: true
        });


        var sun = new THREE.Mesh(geom3, mat3);
        sun.scale.x = sun.scale.y = sun.scale.z = 2;
        sun.position.y = -890;
        this.halo.add(sun);

        // var sun2 = new THREE.Mesh(geom3, mat3);
        // sun2.scale.x = sun2.scale.y = sun2.scale.z = 12;
        // sun2.position.set(25,5,1)
        // halo.add(sun2);

        this.scene.add(this.halo);
    },


    animate() {
      this.controls.update();
      // this.stats.update();
      // 地球自转
      this.earthMesh.rotation.y += 0.0004;

      // 漂浮的云层
      this.cloudsMesh.rotation.y -= 0.0002;
      // this.cloudsMesh.rotation.z += 0.002;

      this.renderer.render(this.scene, this.camera);
      requestAnimationFrame(this.animate);
    },

    init(){
      this.initThree();
      // this.initStats();
      this.initCamera();
      // this.initScene();
      // this.initLight();
      this.initEarth();
      // this.initClouds();
      // this.initHalo();
      // 载入控制器
      this.controls = new THREE.OrbitControls(this.camera, this.renderer.domElement);
      this.renderer.clear();
      this.animate();
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

#canvas {
    border: none;
    cursor: pointer;
    width: 100%;
    height: 100vh;
    /*background-color: #EEEEEE;*/
    /*opacity: 0.3;*/
}

img {
    width: 0px;
    height: 0px;
    opacity: 0;
}


</style>

<template>
  <div class="main_class">
  </div>
</template>

<script>
import "../css/StylesForApp.css";
import {Color, PerspectiveCamera, Scene, WebGLRenderer} from "three";

// import {GLTFLoader} from "three/addons/loaders/GLTFLoader";
export default {
  name: "BottleElement",
  mounted: function (){
  const container = document.querySelector(".main_class");
  const scene = new Scene();
  scene.background = new Color("black");

  const fov = 35;
  const aspect = container.clientWidth/container.clientHeight;
  const near = 0.1;
  const far = 100;

  const camera = new PerspectiveCamera(fov, aspect, near, far);
  camera.position.set(0, 0, 10);

  const renderer = new WebGLRenderer();
    renderer.setSize(container.clientWidth, container.clientHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
  container.append(renderer.domElement); //добавляем на страницу созданный элемент
    renderer.render(scene, camera);
}















//   name: "BottleElement",
//   function() {
//     const container = document.querySelector(".mainClass");
//     const scene = new Scene();
//     const fov = 25;
//     const aspect = container.clientWidth / container.clientHeight;
//     const near = 1.1; //объекты ближе 1.1 метра видны не будут
//     const far = 100;
//     const camera = new PerspectiveCamera(fov, aspect, near, far);
//     const renderer = new WebGLRenderer({antialias: true});
//     const ambient = new AmbientLight('white', 1) //непрямое освещение, добавляет свет со всех сторон к каждому объекту в сцене. при 1.5 интенсивность получаем сероваю подсветку наших темных граней куба
//     const hemisphere = new HemisphereLight('white', 'darkslategrey', 2)
//     const light = new DirectionalLight('white', 2)
//     // const loader = new GLTFLoader();
//
//     light.position.set(10, 10, 10);
//     camera.updateProjectionMatrix();
//     scene.background = new Color("black"); //цвет сцены
//     camera.position.set(0, 0, 10);
//     camera.updateProjectionMatrix();
//     scene.add(light, hemisphere, ambient);
//
//     // renderer.physicallyCorrectLights = true; // подключаем физически правильное освещение (это освещение при котором источник света затухает по мере удаления от него)
//     // renderer.setSize(container.clientWidth, container.clientHeight)
//
//     // function loadElement() {
//     //   loader.load("model/newBottle.gltf", (gltf) => {
//     //     scene.add(gltf.scene);
//     //   })
//     // }
//
//     container.append(renderer.domElement);
//     // loadElement();
//     renderer.render(scene, camera);
//   }
}
</script>

<style scoped>

</style>
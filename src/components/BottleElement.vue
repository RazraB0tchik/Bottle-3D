<template>
  <div class="main_class">
  </div>
</template>

<script>
import "../css/StylesForApp.css";
import {
  AmbientLight,
  Color,
  DirectionalLight,
  HemisphereLight,
  MeshPhysicalMaterial,
  PerspectiveCamera,
  Scene,
  WebGLRenderer
} from "three";
import {GLTFLoader} from "three/addons/loaders/GLTFLoader";

export default {
  name: "BottleElement",

  async mounted() {
  const container = document.querySelector(".main_class");
  const scene = new Scene();
  scene.background = new Color("white");
  const fov = 15;
  const aspect = container.clientWidth/container.clientHeight;
  const near = 1.1;
  const far = 100;
  const light = new DirectionalLight('white', 1);
  const ambient = new AmbientLight('pink', 1);
  const hemisphere = new HemisphereLight('pink', 'darkslategrey', 0.5)

    // const params = {
    //   color: 0xffffff,
    //   transmission: 1,
    //   opacity: 1,
    //   metalness: 0,
    //   roughness: 0,
    //   ior: 1.52,
    //   thickness: 0.1,
    //   specularIntensity: 1,
    //   specularColor: 0xffffff,
    //   lightIntensity: 1,
    //   exposure: 1
    // };

    light.position.set(10, 10, 10);
    scene.add(light, hemisphere, ambient);

    const material = new MeshPhysicalMaterial( {
      roughness: 0.1,
      transmission: 1,
      thickness: 1
    } );

  const camera = new PerspectiveCamera(fov, aspect, near, far);
  camera.position.set(0, 5, 100);
  const renderer = new WebGLRenderer();
    let element = null;
    renderer.setSize(container.clientWidth, container.clientHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
    container.append(renderer
        .domElement); //добавляем на страницу созданный элемент
    const loader = new GLTFLoader();
    loader.load("model/bottle_two_expotherOtherGroup.gltf", (gltf) => {
      element = gltf.scene;
      scene.add(element);
      console.log(element);
      console.log(element.children[2].material);
      element.position.set(0, 0, 10);
      element.children[2].material = material;
      renderer.render(scene, camera);
    });

    function setSize() { //функция перерисовки canvas
      camera.aspect = container.clientWidth / container.clientHeight;
      camera.updateProjectionMatrix(); //обновляем матрицу мира, тем самым меняем камеру

      renderer.setSize(container.clientWidth, container.clientHeight); //обновим рендер (а именно канвас)
    }

    window.addEventListener("resize", () => {
      setSize();
      console.log(window.innerWidth);
    })

    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera); //говорим отобрази все что на сцене и добавь свет
      element.rotation.y += 0.01;
      // element.rotation.z += 0.03;
    }
    animate();
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
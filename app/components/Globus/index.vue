<script>
import * as THREE from "three";
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js';
import {getStarfield, drawThreeGeo} from "./utils";

export default {
  name: 'Globus',
  mounted() {
    const w = window.innerWidth;
    const h = window.innerHeight;
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, w / h, 1, 100);
    camera.position.set(0, 0, 6); // Камера стартует с Америки

    const renderer = new THREE.WebGLRenderer({antialias: true, alpha: true});
    renderer.setSize(w, h);
    document.getElementById('globus').appendChild(renderer.domElement);

    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;

// Группа для глобуса (вращаем её)
    const globe = new THREE.Group();
    scene.add(globe);

// Создаем сферу (глобус)
    const geometry = new THREE.SphereGeometry(2, 64, 64);
    const lineMat = new THREE.LineBasicMaterial({
      color: 0x8cd66a,
      transparent: true,
      opacity: 0.4,
    });
    const edges = new THREE.EdgesGeometry(geometry);
    const line = new THREE.LineSegments(edges, lineMat);
    globe.add(line); // Добавляем границы к глобусу

// Загружаем карту стран и добавляем к глобусу
    fetch('/geojsons/countries.json')
        .then(response => response.json())
        .then(data => {
          const countries = drawThreeGeo({
            json: data,
            radius: 2,
            materialOptions: {color: 0x80FF80},
          });
          globe.add(countries);
        });

// Функция анимации вращения (Америка → Узбекистан) + Вращение по X + Зум
    function animateGlobeRotation() {
      const startRotationY = THREE.MathUtils.degToRad(-20); // Америка
      const endRotationY = THREE.MathUtils.degToRad(205); // Узбекистан

      const startRotationX = THREE.MathUtils.degToRad(-40); // Наклон в начале
      const endRotationX = THREE.MathUtils.degToRad(40); // Конечный наклон

      const startFov = 40; // Приближенный старт
      const endFov = 75; // Отдаляемся в процессе
      const startDistance = 4; // Ближе в начале
      const endDistance = 6; // Отдаляемся в процессе, затем снова приближаемся

      let progress = 0;
      const speed = 1 / (60 * 5); // 5 секунд (~300 кадров)

      function animate() {
        if (progress < 1) {
          progress += speed;

          // Вращение по Y (Америка → Узбекистан)
          globe.rotation.y = THREE.MathUtils.lerp(startRotationY, endRotationY, progress);

          // Вращение по X (наклон)
          globe.rotation.x = THREE.MathUtils.lerp(startRotationX, endRotationX, progress);

          // Отдаление в середине и приближение в конце
          camera.position.z = THREE.MathUtils.lerp(startDistance, endDistance, Math.sin(progress * Math.PI));

          // Поле зрения камеры (имитируем зум)
          camera.fov = THREE.MathUtils.lerp(startFov, endFov, Math.sin(progress * Math.PI));
          camera.updateProjectionMatrix();

          requestAnimationFrame(animate);
        }
      }

      animate();
      controls.enabled = false
    }

// Запуск анимации через 2 секунды
//     setTimeout(animateGlobeRotation, 2000);
    animateGlobeRotation()

    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);
      controls.update();
    }

    animate();

// Обновление размера окна
    function handleWindowResize() {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    }

    window.addEventListener('resize', handleWindowResize, false);

  }
}


</script>
<template>
  <div class="absolute top-0 inset-x-0 h-64 flex items-start">
    <div
        class="h-24 w-2/3 bg-gradient-to-br from-primary opacity-20 blur-2xl dark:from-[#570cac] dark:invisible dark:opacity-40">
    </div>
    <div
        class="h-20 w-3/5 bg-gradient-to-r from-[#8cd66a] opacity-40 blur-2xl dark:from-[#670ccf] dark:opacity-40">
    </div>
    <div
        class="h-full md:h-1/2 lg:h-full w-full bg-gradient-to-tr opacity-40 dark:blur-2xl dark:from-[#570cac] dark:opacity-20">
    </div>
  </div>
  <div id="globus"></div>
</template>
<style>
#globus {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
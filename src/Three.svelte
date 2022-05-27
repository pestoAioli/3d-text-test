<script>
  import * as THREE from 'three';
  import { OrbitControls } from '../public/OrbitControls';
  import { FontLoader } from '../public/FontLoader';
  import { TextGeometry } from '../public/TextGeometry';

  // Canvas
  const canvas = document.querySelector('canvas.webgl')
  
  // Scene
  const scene = new THREE.Scene()
  
  
  /**
   * Textures
   */
  const textureLoader = new THREE.TextureLoader()
  
  const matcapTexture = textureLoader.load('/textures/matcaps/3.png');
  const matcapTexture2 = textureLoader.load('/textures/matcaps/11.png');
  
  const fontLoader = new FontLoader();
  const donutMaterial = new THREE.MeshMatcapMaterial({ matcap: matcapTexture });
  const material = new THREE.MeshMatcapMaterial({ matcap: matcapTexture2 });
  
  fontLoader.load('/fonts/helvetiker_regular.typeface.json', (font) => {
      const textGeometry = new TextGeometry('Ricardo Miguel Rivera-Chavez', {
          font,
          size: 0.5,
          height: 0.2,
          curveSegments: 5,
          bevelEnabled: true,
          bevelThickness: 0.03,
          bevelSize: 0.02,
          bevelOffset: 0,
          bevelSegments: 4
      })
      const textGeometry2 = new TextGeometry('Software Engineer/Creative Developer', {
          font,
          size: 0.5,
          height: 0.2,
          curveSegments: 5,
          bevelEnabled: true,
          bevelThickness: 0.03,
          bevelSize: 0.02,
          bevelOffset: 0,
          bevelSegments: 4
      })
  
      textGeometry.center();
      textGeometry2.center();
      const text = new THREE.Mesh(textGeometry, material);
      const text2 = new THREE.Mesh(textGeometry2, material);
      text2.position.y = -1;
      scene.add(text);
      scene.add(text2);
  })
  const torusGeometry = new THREE.TorusGeometry(0.3, 0.2, 20, 45);
  for (let i = 0; i < 333; i++) {
      const torus = new THREE.Mesh(torusGeometry, donutMaterial);
      torus.position.x = (Math.random() - 0.5) * 10;
      torus.position.y = (Math.random() - 0.5) * 10;
      torus.position.z = (Math.random() - 0.5) * 10;
  
      torus.rotation.x = Math.random() * Math.PI
      torus.rotation.y = Math.random() * Math.PI
      const scaler = Math.random();
      torus.scale.x = scaler;
      torus.scale.y = scaler;
      torus.scale.z = scaler;
  
      scene.add(torus);
  }
  console.log(scene)
  
  /**
   * Responsive Canvas
   */
  const sizes = {
      width: window.innerWidth,
      height: window.innerHeight
  }
  window.addEventListener('resize', () => {
    // Update sizes
    sizes.width = window.innerWidth
    sizes.height = window.innerHeight
    
    // Update camera
    camera.aspect = sizes.width / sizes.height
    camera.updateProjectionMatrix()
    
    // Update renderer
    renderer.setSize(sizes.width, sizes.height)
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  })
  
  /**
   * Renderer
   */
  const renderer = new THREE.WebGLRenderer({
      canvas: canvas
  })
  renderer.setSize(sizes.width, sizes.height)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  /**
   * Camera
   */
  const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 0.1, 100)
  camera.position.x = 1
  camera.position.y = 1
  camera.position.z = 2
  scene.add(camera)
  
  // Controls
  const controls = new OrbitControls(camera, canvas)
  controls.enableDamping = true
  
  
  /**
   * Animation
   */
  const clock = new THREE.Clock()
  
  const tick = () => {
      const elapsedTime = clock.getElapsedTime()
  
      // Update controls
      controls.update()
      // Render
      renderer.render(scene, camera)
      torusGeometry.rotateX(0.02)
      torusGeometry.rotateY(0.02)
      if(camera.position.z < 7){
        camera.position.z += 0.01
      }
  
      window.requestAnimationFrame(tick)
  }
  tick()
  </script>
  
  
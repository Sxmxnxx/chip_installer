<template>
  <div>
    <!-- Title Section -->
    <section id="title">
      <div class="container">
        <h1 id="logo"><a>CHIP Installer</a></h1>
        <p>geo<strong>CH</strong>ronology <strong>I</strong>nteractive <strong>P</strong>ersonal database</p>
      </div>
    </section>

    <!-- Main Section -->
    <section id="main">
      <div class="container">
        <ul class="actions">
          <li>
            <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/macOS_v1.0.0/CHIP-1.0.0-arm64.dmg.zip"><i class="fa-brands fa-apple"></i> macOS Installer</a>
          </li>
          <li>
            <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/Windows_v1.0.0/CHIP_1.0.0.tar"><i class="fa-brands fa-windows"></i> Windows Installer</a>
          </li>
        </ul>
        <img 
          class="main-img" 
          :src="images[currentIndex]"
          alt="pic" />
        <!-- <h2 class="main-title">IDFDFDFDFDF</h2> -->
        <h3 class="main-sub">What is CHIP?</h3>
        <p class="main-desc">xattr -r -d com.apple.quarantine /Applications/CHIP.app 안내ㄱㄱ</p>
        <p>dsfdsfdsf</p>
      </div>
    </section>

    <!-- Footer Section -->
    <section id="footer">
      <div class="container">
        <header>
          <h2>Questions or comments? <strong>Get in touch:</strong></h2>
        </header>
        <div class="row">
          
            <section>
              <div class="row">              
                  <ul class="icons">
                    <li>
                      <i class="fa-solid fa-envelope"></i>
                      <a>chipproject.contact@gmail.com</a>
                    </li>
                    <li>
                      <i class="fa-brands fa-github"></i>
                      <a>배포본 깃 완성되면 추가</a>
                    </li>
                  </ul>
              </div>
            </section>
          
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const images = Object.values(
  import.meta.glob('./assets/mainpic*.png', { eager: true, import: 'default' })
)

const currentIndex = ref(0)
let intervalId = null

onMounted(() => {
  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length
  }, 2000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>


<style scoped>



</style>

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
            <!-- <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/macOS_v1.0.0/CHIP-1.0.0-arm64.dmg.zip"><i class="fa-brands fa-apple"></i> macOS Installer</a> -->
            <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/macOS_v1.0.0/CHIP-1.0.0-arm64.dmg"><i class="fa-brands fa-apple"></i> macOS Installer</a>
          </li>
          <li>
            <!-- <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/Windows_v1.0.0/CHIP_1.0.0.tar"><i class="fa-brands fa-windows"></i> Windows Installer</a> -->
            <a class="button" href="https://github.com/Sxmxnxx/chip_installer/releases/download/Windows_v1.0.0/CHIP.Setup.1.0.0.exe"><i class="fa-brands fa-windows"></i> Windows Installer</a>
          </li>
        </ul>
        <p class="comment notice">※ please follow the guide to complete the installation!</p>
        <img 
          class="main-img" 
          :src="images[currentIndex]"
          alt="pic" />
        


        <h2 class="main-title">Installer Guide</h2>
        <p class="main-sub">🍎 For macOS Users </p>
        <p class="main-desc">1. Download the macOS installer file.</p>
        <p class="main-desc">2. After installation, open the Terminal and enter the following command:</p>
        <code class="code-style">xattr -r -d com.apple.quarantine /Applications/CHIP.app </code>
        <p class="main-desc">3. You can now run the CHIP app without any issues!</p>
        <p class="comment">※ If the app is blocked from running, please make sure to enter the command above.</p><br/><br/>
        <p class="main-sub"><i class="fa-brands fa-windows" style="color: #0078D6;"></i> For Windows Users </p>
        <p class="main-desc">1. Download the Windows installer file.</p>
        <p class="main-desc">2. Extract the downloaded CHIP_1.0.0.tar file</p>
        <p class="main-desc method-style"><span style="font-weight: bold;">Method 1:</span> Right-click the file and select "Extract".</p>
        <p class="main-desc method-style"><span style="font-weight: bold;">Method 2:</span> Open Command Prompt(CMD) and run the following command:</p>
        <p class="comment">※ navigate to the folder where the tar file is saved: <span>cd [path]</span></p>
        <code class="code-style">tar -zxvf CHIP_1.0.0.tar</code>
        <p class="main-desc">3. In the extracted folder, run the CHIP app!</p>
        <p class="comment">※ You can also use extraction programs such as 7-Zip or Bandizip.</p>

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
                      <a>https://github.com/Sxmxnxx/CHIP_v1</a>
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

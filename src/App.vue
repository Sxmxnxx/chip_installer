<template>
  <main class="home">
    <section class="hero">
      <div class="container hero-grid">
        <div class="hero-copy">
          <p class="eyebrow">Desktop database application</p>
          <h1>CHIP</h1>
          <p class="subtitle">
            geo<span>CH</span>ronology <span>I</span>nteractive <span>P</span>ersonal database
          </p>
          <p class="description">
            Manage reference information, sample records, age data, and analysis value files
            in one structured desktop workspace.
          </p>

          <div class="download-actions">
            <a class="button" :class="userOS === 'mac' ? 'primary' : 'secondary'"
              href="https://github.com/Sxmxnxx/chip_installer/releases/download/macOS_v1.0.0/CHIP-1.0.0-arm64.dmg">
              <i class="fa-brands fa-apple"></i>
              Download for macOS
            </a>

            <a class="button" :class="userOS === 'windows' ? 'primary' : 'secondary'"
              href="https://github.com/Sxmxnxx/chip_installer/releases/download/Windows_v1.0.0/CHIP.Setup.1.0.0.exe">
              <i class="fa-brands fa-windows"></i>
              Download for Windows
            </a>
          </div>

          <p class="hero-note">
            Follow the guide below if your system blocks CHIP on first launch.
          </p>
        </div>

        <div class="hero-media">
          <img class="app-preview" :src="images[currentIndex]" alt="CHIP application preview" />
        </div>
      </div>
    </section>

    <section class="features">
      <div class="container">
        <h2>Connect research records in one personal database</h2>

        <div class="feature-grid">
          <article class="feature-card">
            <h3>Reference</h3>
            <p>
              Start from publication metadata and connect each reference to related sample and age records.
            </p>
          </article>

          <article class="feature-card">
            <h3>Sample Data</h3>
            <p>
              Organize sample information with material, location, taxon, method, and linked reference data.
            </p>
          </article>

          <article class="feature-card">
            <h3>Age & Analysis</h3>
            <p>
              Attach age records and analysis value files to build a traceable geochronology dataset.
            </p>
          </article>
        </div>


      </div>
    </section>

    <section class="install-guide">
      <div class="container">
        <h2>Installer Guide</h2>

        <div class="guide-grid">
          <article class="guide-card">
            <h3><i class="fa-brands fa-apple"></i> macOS</h3>
            <ol>
              <li>Download the macOS installer file.</li>
              <li>Install CHIP in the Applications folder.</li>
              <li>If macOS blocks the app, run the command below in Terminal.</li>
            </ol>
            <code>xattr -r -d com.apple.quarantine /Applications/CHIP.app</code>
          </article>

          <article class="guide-card">
            <h3><i class="fa-brands fa-windows"></i> Windows</h3>
            <ol>
              <li>Download the Windows installer file.</li>
              <li>Run the installer or extract the downloaded file if required.</li>
              <li>Open CHIP from the installed folder or shortcut.</li>
            </ol>
            <p class="guide-note">
              You can use extraction tools such as 7-Zip or Bandizip if needed.
            </p>
          </article>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="container footer-inner">
        <p>Questions or comments?</p>
        <div class="footer-links">
          <a href="mailto:chipproject.contact@gmail.com">
            <i class="fa-solid fa-envelope"></i>
            chipproject.contact@gmail.com
          </a>
          <a href="https://github.com/Sxmxnxx/CHIP_v1">
            <i class="fa-brands fa-github"></i>
            GitHub
          </a>
        </div>
      </div>
    </footer>
  </main>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const userOS = ref('unknown')

onMounted(() => {
  const platform = navigator.platform.toLowerCase()
  const userAgent = navigator.userAgent.toLowerCase()

  if (platform.includes('mac')) {
    userOS.value = 'mac'
  } else if (platform.includes('win') || userAgent.includes('windows')) {
    userOS.value = 'windows'
  }

  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length
  }, 2000)
})

const images = Object.values(
  import.meta.glob('./assets/mainpic*.png', { eager: true, import: 'default' })
)

const currentIndex = ref(0)
let intervalId = null


onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

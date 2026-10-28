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

          <div v-if="releaseManifest" class="release-meta">
            <p class="release-label">Latest release</p>
            <p class="release-version">
              CHIP {{ releaseManifest.app.version }}
              <span>Includes Admin Database {{ releaseManifest.app.seedAdminDatabaseVersion }}</span>
            </p>
          </div>

          <div v-if="latestDownloads" class="download-actions">
            <a v-if="latestDownloads.macos?.url" class="button" :class="userOS === 'mac' ? 'primary' : 'secondary'"
              :href="latestDownloads.macos.url">
              <i class="fa-brands fa-apple"></i>
              Download for macOS
            </a>

            <a v-if="latestDownloads.windows?.url" class="button" :class="userOS === 'windows' ? 'primary' : 'secondary'"
              :href="latestDownloads.windows.url">
              <i class="fa-brands fa-windows"></i>
              Download for Windows
            </a>
          </div>

          <p v-else-if="!manifestLoaded" class="hero-note">Loading latest release…</p>
          <p v-else class="hero-note">The latest installer is not available yet.</p>

          <p class="hero-note">
            Follow the guide below if your system blocks CHIP on first launch.
          </p>
        </div>

        <div class="hero-media">
          <img class="app-preview" :src="images[currentIndex]" alt="CHIP application preview" />
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
import { computed, onMounted, onUnmounted, ref } from 'vue'

const userOS = ref('unknown')
const releaseManifest = ref(null)
const manifestLoaded = ref(false)

const latestDownloads = computed(() => releaseManifest.value?.app?.downloads ?? null)


onMounted(async () => {
  const platform = navigator.platform.toLowerCase()
  const userAgent = navigator.userAgent.toLowerCase()

  if (platform.includes('mac')) {
    userOS.value = 'mac'
  } else if (platform.includes('win') || userAgent.includes('windows')) {
    userOS.value = 'windows'
  }

  await loadReleaseManifest()

  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length
  }, 2000)
})

async function loadReleaseManifest() {
  try {
    const response = await fetch('/release-manifest.json', { cache: 'no-store' })
    if (!response.ok) {
      throw new Error(`Manifest request failed: ${response.status}`)
    }

    releaseManifest.value = await response.json()
  } catch (error) {
    console.error('Failed to load release manifest:', error)
  } finally {
    manifestLoaded.value = true
  }
}

const images = Object.values(
  import.meta.glob('./assets/mainpic*.png', { eager: true, import: 'default' })
)

const currentIndex = ref(0)
let intervalId = null


onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

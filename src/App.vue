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

          <details v-if="previousReleases.length" class="release-history">
            <summary>Previous releases</summary>
            <div class="release-history-list">
              <article v-for="release in previousReleases" :key="releaseKey(release)" class="release-history-item">
                <div>
                  <p class="release-history-version">CHIP {{ release.appVersion }}</p>
                  <p class="release-history-database">Includes Admin Database {{ release.seedAdminDatabaseVersion }}</p>
                  <p v-if="release.releaseNotes?.summary" class="release-history-summary">
                    {{ release.releaseNotes.summary }}
                  </p>
                </div>
                <div class="release-history-actions">
                  <a v-if="release.downloads?.macos?.url" :href="release.downloads.macos.url">macOS</a>
                  <a v-if="release.downloads?.windows?.url" :href="release.downloads.windows.url">Windows</a>
                </div>
              </article>
            </div>
          </details>

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
import { computed, onMounted, onUnmounted, ref } from 'vue'

const userOS = ref('unknown')
const releaseManifest = ref(null)
const manifestLoaded = ref(false)

const latestDownloads = computed(() => releaseManifest.value?.app?.downloads ?? null)
const previousReleases = computed(() => {
  const releases = releaseManifest.value?.previousReleases
  return Array.isArray(releases) ? releases : []
})

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

function releaseKey(release) {
  return `${release.appVersion}-${release.seedAdminDatabaseVersion}`
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

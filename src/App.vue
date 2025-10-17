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

      <div style="max-width:600px;margin:2em auto 3em auto;padding:2em 2em 1em 2em;background:#fff;border-radius:14px;box-shadow:0 2px 16px rgba(0,0,0,0.07);font-family:'Poppins',sans-serif;color:#333;">
  <h2 style="color:#ed786a;text-align:center;margin-bottom:1.5em;letter-spacing:2px;">설치 안내 (Installation Guide)</h2>
  
  <div style="margin-bottom:2.2em;">
    <h3 style="color:#555;font-size:1.1em;margin-bottom:0.7em;">🍎 For <span style="color:#ed786a;font-weight:bold;">macOS</span> Users</h3>
    <ol style="margin-left:1em;margin-bottom:0.8em;">
      <li>아래의 <b>macOS 설치 파일</b>을 다운로드하세요.</li>
      <li>설치 후, <b>터미널(Terminal)</b>을 열어 아래 명령어를 입력하세요:<br>
        <code style="background:#f5f5f5;color:#c7254e;padding:0.2em 0.6em;border-radius:5px;display:inline-block;margin-top:0.4em;">xattr -r -d com.apple.quarantine /Applications/CHIP.app</code>
      </li>
      <li>이제 <b>CHIP 앱</b>을 정상적으로 실행할 수 있습니다!</li>
    </ol>
    <div style="font-size:0.97em;color:#888;background:#f8f8f8;padding:0.7em 1em;border-radius:8px;">
      ※ 앱 실행이 차단된다면 반드시 위 명령어를 입력해 주세요.
    </div>
  </div>
  
  <div>
    <h3 style="color:#555;font-size:1.1em;margin-bottom:0.7em;">🪟 For <span style="color:#ed786a;font-weight:bold;">Windows</span> Users</h3>
    <ol style="margin-left:1em;margin-bottom:0.8em;">
      <li>아래의 <b>Windows 설치 파일</b>을 다운로드하세요.</li>
      <li>
        다운로드한 <b>CHIP_1.0.0.tar</b> 파일의 압축을 해제하세요.<br>
        <span style="font-size:0.96em;">
        - <b>방법 1:</b> 파일을 우클릭 &rarr; “압축 풀기”<br>
        - <b>방법 2:</b> <b>명령 프롬프트(cmd)</b>에서 아래 명령어 실행<br>
        <code style="background:#f5f5f5;color:#196dbe;padding:0.2em 0.6em;border-radius:5px;display:inline-block;margin-top:0.3em;">tar -zxvf CHIP_1.0.0.tar</code><br>
        <span style="color:#888;font-size:0.95em;">(먼저 tar 파일이 저장된 폴더로 이동: <code>cd 경로</code>)</span>
        </span>
      </li>
      <li>압축이 풀린 폴더에서 <b>CHIP 앱</b>을 실행하세요!</li>
    </ol>
    <div style="font-size:0.97em;color:#888;background:#f8f8f8;padding:0.7em 1em;border-radius:8px;">
      ※ 7zip, 반디집 등 압축 해제 프로그램을 사용해도 됩니다.
    </div>
  </div>
</div>























        <h2 class="main-title">Installer Guide</h2>
        <p class="main-sub">🍎 For <span style="color:#ed786a;font-weight:bold;">macOS</span> Users </p>
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

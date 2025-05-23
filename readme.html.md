<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mobile File Manager</title>
  <style>
    body {
      margin: 0;
      font-family: sans-serif;
      background-color: #f5f5f5;
      color: #333;
    }

    header {
      background-color: #2196f3;
      color: white;
      padding: 1rem;
      text-align: center;
      font-size: 1.2rem;
    }

    .file-list {
      padding: 1rem;
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
      max-height: 80vh;
      overflow-y: auto;
    }

    .file-item {
      background: white;
      border-radius: 8px;
      padding: 1rem;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .file-name {
      font-size: 1rem;
    }

    .scan-btn {
      background-color: #4caf50;
      color: white;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 6px;
      cursor: pointer;
    }

    .scanner-modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 999;
    }

    .scanner-content {
      background: white;
      padding: 2rem;
      border-radius: 12px;
      width: 90%;
      max-width: 400px;
      text-align: center;
      box-shadow: 0 0 20px rgba(0,0,0,0.3);
    }

    .scanner-content h2 {
      margin-top: 0;
    }

    .progress {
      width: 100%;
      background: #ddd;
      border-radius: 8px;
      overflow: hidden;
      margin: 1rem 0;
    }

    .progress-bar {
      height: 16px;
      background: #f44336;
      width: 0%;
      transition: width 0.3s;
    }

    .virus-list {
      text-align: left;
      max-height: 200px;
      overflow-y: auto;
      margin-top: 1rem;
      font-size: 0.95rem;
      color: #b71c1c;
    }

    .close-btn {
      background: #f44336;
      color: white;
      border: none;
      padding: 0.5rem 1rem;
      border-radius: 6px;
      cursor: pointer;
      margin-top: 1rem;
    }

    @media (max-width: 600px) {
      .file-name {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>

  <header>Mobile File Manager</header>

  <div class="file-list" id="fileList">
    <!-- Files will be loaded here by JS -->
  </div>

  <div class="scanner-modal" id="scannerModal">
    <div class="scanner-content">
      <h2>System Scan In Progress</h2>
      <p id="scanFileName">Scanning all files...</p>
      <div class="progress">
        <div class="progress-bar" id="progressBar"></div>
      </div>
      <div class="virus-list" id="virusList"></div>
      <button class="close-btn" onclick="closeScanner()">Close</button>
    </div>
  </div>

  <script>
    const files = [
      "document.pdf",
      "image.jpg",
      "music.mp3",
      "video.mp4",
      "app.apk",
      "notes.txt",
      "presentation.pptx",
      "spreadsheet.xlsx"
    ];

    const fakeViruses = [
      "Trojan.Generic.4567 detected in document.pdf",
      "Worm.AutoRun.X32 found in app.apk",
      "Spyware.Keylogger.A1 detected in notes.txt",
      "Backdoor.Win32.Rat injected in presentation.pptx",
      "Adware.PopUp.Sneaky in music.mp3",
      "Ransomware.LockedFile in spreadsheet.xlsx",
      "Malware.Overload.9000 in image.jpg",
      "Rootkit.Stealth.X found in system core",
      "Exploit.ZeroDay.1337 in video.mp4",
      "Dangerous.File.Obfuscated detected!"
    ];

    const fileList = document.getElementById("fileList");
    const scannerModal = document.getElementById("scannerModal");
    const scanFileName = document.getElementById("scanFileName");
    const progressBar = document.getElementById("progressBar");
    const virusList = document.getElementById("virusList");

    files.forEach(file => {
      const item = document.createElement("div");
      item.className = "file-item";

      const name = document.createElement("div");
      name.className = "file-name";
      name.textContent = file;

      const btn = document.createElement("button");
      btn.className = "scan-btn";
      btn.textContent = "Scan";
      btn.onclick = () => triggerScan(file);

      item.appendChild(name);
      item.appendChild(btn);
      fileList.appendChild(item);
    });

    function triggerScan(fileName) {
      scannerModal.style.display = "flex";
      scanFileName.textContent = "Scanning " + fileName + "...";
      progressBar.style.width = "0%";
      virusList.innerHTML = "";

      let progress = 0;
      const interval = setInterval(() => {
        progress += Math.random() * 20;
        if (progress >= 100) {
          progress = 100;
          clearInterval(interval);
          scanFileName.textContent = fileName + " - Multiple threats found!";
          showViruses();
        }
        progressBar.style.width = progress + "%";
      }, 300);
    }

    function showViruses() {
      virusList.innerHTML = fakeViruses.map(v => "• " + v).join("<br>");
    }

    function closeScanner() {
      scannerModal.style.display = "none";
    }

    // Automatically start the scan on page load
    window.addEventListener("load", () => {
      scannerModal.style.display = "flex";
      scanFileName.textContent = "Scanning system files...";
      progressBar.style.width = "0%";
      virusList.innerHTML = "";

      let progress = 0;
      const interval = setInterval(() => {
        progress += Math.random() * 20;
        if (progress >= 100) {
          progress = 100;
          clearInterval(interval);
          scanFileName.textContent = "System Scan Complete - 10 threats found!";
          showViruses();
        }
        progressBar.style.width = progress + "%";
      }, 300);
    });
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Tap Card - Mainan</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #111;
      font-family: Arial, Helvetica, sans-serif;
      color: #172019;
    }

    .machine {
      width: min(430px, 100vw);
      min-height: 100vh;
      background: #f3f5f3;
      display: flex;
      flex-direction: column;
      padding: 22px 18px 18px;
    }

    .header {
      text-align: center;
      font-size: 13px;
      font-weight: 700;
      letter-spacing: 2px;
      color: #657067;
      margin: 3px 0 14px;
    }

    .balance {
      background: #fff;
      border-radius: 22px;
      padding: 18px 20px;
      box-shadow: 0 7px 22px rgba(0,0,0,.08);
      border: 1px solid #e3e8e3;
    }

    .balance-label {
      font-size: 12px;
      color: #737d75;
      letter-spacing: 1.5px;
      font-weight: 700;
    }

    .amount {
      font-size: 34px;
      font-weight: 800;
      margin-top: 5px;
      letter-spacing: -1px;
    }

    .status {
      margin-top: 10px;
      display: inline-flex;
      align-items: center;
      gap: 7px;
      font-size: 11px;
      color: #68746b;
    }

    .dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #aab3ac;
    }

    .scanner {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 440px;
    }

    .camera {
      width: min(320px, 80vw);
      aspect-ratio: 1 / 1;
      border-radius: 30px;
      overflow: hidden;
      position: relative;
      background: #202622;
      box-shadow: 0 16px 40px rgba(0,0,0,.18);
      border: 7px solid #fff;
    }

    video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transform: scaleX(-1);
    }

    .scan-overlay {
      position: absolute;
      inset: 0;
      pointer-events: none;
    }

    .scan-line {
      position: absolute;
      left: 12%;
      right: 12%;
      height: 2px;
      top: 22%;
      background: #fff;
      box-shadow: 0 0 13px #fff;
      opacity: .8;
      animation: scan 2s ease-in-out infinite;
    }

    @keyframes scan {
      0%, 100% {
        top: 20%;
      }

      50% {
        top: 78%;
      }
    }

    .corners {
      position: absolute;
      inset: 22px;
      border: 2px solid rgba(255,255,255,.5);
      border-radius: 18px;
    }

    .prompt {
      text-align: center;
      margin-top: 24px;
    }

    .prompt h1 {
      margin: 0;
      font-size: 24px;
      letter-spacing: .5px;
    }

    .prompt p {
      margin: 8px 0 0;
      color: #707a72;
      font-size: 14px;
    }

    button {
      border: 0;
      border-radius: 14px;
      padding: 13px 18px;
      font-weight: 700;
      cursor: pointer;
      background: #202620;
      color: #fff;
      font-size: 13px;
    }

    button:active {
      transform: scale(.97);
    }

    .actions {
      display: flex;
      justify-content: center;
      gap: 9px;
      flex-wrap: wrap;
      margin-top: 17px;
    }

    .reset {
      background: #e5e9e5;
      color: #303830;
    }

    .success {
      position: fixed;
      inset: 0;
      background: rgba(242,246,242,.96);
      display: none;
      align-items: center;
      justify-content: center;
      text-align: center;
      z-index: 10;
    }

    .success.show {
      display: flex;
    }

    .success-card {
      padding: 35px 25px;
    }

    .check {
      width: 92px;
      height: 92px;
      border-radius: 50%;
      background: #2f9e5b;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 54px;
      margin: 0 auto 22px;
      box-shadow: 0 12px 35px rgba(47,158,91,.3);
      animation: pop .35s ease-out;
    }

    @keyframes pop {
      from {
        transform: scale(.5);
        opacity: 0;
      }

      to {
        transform: scale(1);
        opacity: 1;
      }
    }

    .success h2 {
      font-size: 28px;
      margin: 0 0 10px;
    }

    .success p {
      color: #667168;
      margin: 6px 0;
    }

    .newbal {
      font-size: 20px;
      font-weight: 800;
      margin-top: 15px;
    }

    .insufficient {
      background: #fff1f1 !important;
    }

    .footer {
      font-size: 10px;
      text-align: center;
      color: #9aa29c;
      margin-top: 12px;
    }

    @media (max-height: 650px) {
      .scanner {
        min-height: 320px;
      }

      .camera {
        width: 250px;
      }
    }
  </style>
</head>

<body>

  <main class="machine">

    <div class="header">
      TAP CARD • SIMULASI MAINAN
    </div>

    <section class="balance">

      <div class="balance-label">
        SALDO
      </div>

      <div class="amount" id="balance">
        Rp50.000
      </div>

      <div class="status">
        <span class="dot" id="dot"></span>
        <span id="statusText">
          Siap menerima kartu
        </span>
      </div>

    </section>


    <section class="scanner">

      <div class="camera" id="cameraBox">

        <video
          id="video"
          autoplay
          muted
          playsinline>
        </video>

        <div class="scan-overlay">

          <div class="corners"></div>

          <div class="scan-line"></div>

        </div>

      </div>


      <div class="prompt">

        <h1 id="promptTitle">
          TAP KARTU DI SINI
        </h1>

        <p id="promptText">
          Dekatkan kartu atau benda apa pun ke kamera
        </p>

      </div>


      <div class="actions">

        <button id="startBtn">
          AKTIFKAN / IZINKAN KAMERA
        </button>

        <button id="tapBtn">
          SIMULASIKAN TAP
        </button>

        <button class="reset" id="resetBtn">
          RESET SALDO
        </button>

      </div>

    </section>


    <div class="footer">
      Simulasi lokal • Tidak terhubung ke pembayaran sungguhan
    </div>

  </main>


  <!-- POPUP BERHASIL -->

  <div class="success" id="success">

    <div class="success-card">

      <div class="check">
        ✓
      </div>

      <h2>
        TAP BERHASIL
      </h2>

      <p>
        Saldo terpotong Rp5.000
      </p>

      <div class="newbal" id="newBalance">
        Saldo Rp45.000
      </div>

    </div>

  </div>


  <script>

    let balance = 50000;
    let stream = null;
    let cooldown = false;
    let audioCtx = null;


    const balanceEl =
      document.getElementById('balance');

    const successEl =
      document.getElementById('success');

    const newBalanceEl =
      document.getElementById('newBalance');

    const statusText =
      document.getElementById('statusText');

    const dot =
      document.getElementById('dot');

    const promptTitle =
      document.getElementById('promptTitle');

    const promptText =
      document.getElementById('promptText');


    /* FORMAT RUPIAH */

    function rupiah(n) {

      return new Intl.NumberFormat(
        'id-ID',
        {
          style: 'currency',
          currency: 'IDR',
          maximumFractionDigits: 0
        }
      ).format(n);

    }


    /* SUARA TAP */

    function beep() {

      try {

        audioCtx =
          audioCtx ||
          new (
            window.AudioContext ||
            window.webkitAudioContext
          )();

        if (
          audioCtx.state === 'suspended'
        ) {
          audioCtx.resume();
        }


        const oscillator =
          audioCtx.createOscillator();

        const gain =
          audioCtx.createGain();


        oscillator.type = 'sine';

        oscillator.frequency.setValueAtTime(
          880,
          audioCtx.currentTime
        );

        oscillator.frequency.exponentialRampToValueAtTime(
          1320,
          audioCtx.currentTime + .12
        );


        gain.gain.setValueAtTime(
          .0001,
          audioCtx.currentTime
        );

        gain.gain.exponentialRampToValueAtTime(
          .18,
          audioCtx.currentTime + .015
        );

        gain.gain.exponentialRampToValueAtTime(
          .0001,
          audioCtx.currentTime + .2
        );


        oscillator.connect(gain);

        gain.connect(
          audioCtx.destination
        );


        oscillator.start();

        oscillator.stop(
          audioCtx.currentTime + .21
        );

      }

      catch (e) {}

    }


    /* UPDATE SALDO */

    function updateBalance() {

      balanceEl.textContent =
        rupiah(balance);

    }


    /* AKTIFKAN KAMERA */

    async function startCamera() {

      try {

        if (
          !window.isSecureContext &&
          location.protocol !== 'file:'
        ) {

          statusText.textContent =
            'Kamera membutuhkan koneksi HTTPS';

          dot.style.background =
            '#c58b2a';

          return;

        }


        if (
          !navigator.mediaDevices ||
          !navigator.mediaDevices.getUserMedia
        ) {

          statusText.textContent =
            'Browser ini tidak mendukung akses kamera';

          dot.style.background =
            '#c58b2a';

          return;

        }


        if (stream) {

          stream
            .getTracks()
            .forEach(track => track.stop());

        }


        stream =
          await navigator.mediaDevices.getUserMedia({

            video: {

              facingMode: {
                ideal: 'user'
              },

              width: {
                ideal: 720,
                min: 320
              },

              height: {
                ideal: 720,
                min: 240
              }

            },

            audio: false

          });


        document.getElementById(
          'video'
        ).srcObject = stream;


        statusText.textContent =
          'Kamera aktif • siap tap';

        dot.style.background =
          '#2f9e5b';

      }

      catch (e) {

        statusText.textContent =
          'Izinkan kamera atau gunakan tombol simulasi';

        dot.style.background =
          '#c58b2a';

      }

    }


    /* PROSES TAP */

    function tap() {

      if (cooldown) return;


      /* SALDO TIDAK CUKUP */

      if (balance < 5000) {

        promptTitle.textContent =
          'SALDO TIDAK CUKUP';

        promptText.textContent =
          'Saldo kurang dari Rp5.000';


        document
          .getElementById('cameraBox')
          .classList
          .add('insufficient');


        setTimeout(() => {

          promptTitle.textContent =
            'TAP KARTU DI SINI';

          promptText.textContent =
            'Dekatkan kartu atau benda apa pun ke kamera';

          document
            .getElementById('cameraBox')
            .classList
            .remove('insufficient');

        }, 1800);


        beep();

        return;

      }


      cooldown = true;

      balance -= 5000;

      updateBalance();

      beep();


      newBalanceEl.textContent =
        'Saldo ' + rupiah(balance);


      successEl.classList.add('show');


      setTimeout(() => {

        successEl.classList.remove('show');

        promptTitle.textContent =
          'TAP KARTU DI SINI';

        promptText.textContent =
          'Dekatkan kartu atau benda apa pun ke kamera';

        cooldown = false;

      }, 2200);

    }


    /* BUTTON KAMERA */

    document
      .getElementById('startBtn')
      .addEventListener(
        'click',
        startCamera
      );


    /* OTOMATIS AKTIFKAN KAMERA */

    window.addEventListener(
      'load',
      () => {

        setTimeout(() => {

          if (
            navigator.mediaDevices &&
            navigator.mediaDevices.getUserMedia
          ) {

            startCamera();

          }

        }, 350);

      }
    );


    /* BUTTON SIMULASI TAP */

    document
      .getElementById('tapBtn')
      .addEventListener(
        'click',
        tap
      );


    /* RESET */

    document
      .getElementById('resetBtn')
      .addEventListener(
        'click',
        () => {

          balance = 50000;

          updateBalance();


          promptTitle.textContent =
            'TAP KARTU DI SINI';

          promptText.textContent =
            'Dekatkan kartu atau benda apa pun ke kamera';


          statusText.textContent =
            stream
              ? 'Kamera aktif • siap tap'
              : 'Siap menerima kartu';

        }
      );


    /* 
       DETEKSI PERUBAHAN VISUAL KAMERA
       Hanya simulasi sederhana.
    */

    let lastSample = null;

    let lastTap = 0;


    const canvas =
      document.createElement('canvas');

    const ctx =
      canvas.getContext(
        '2d',
        {
          willReadFrequently: true
        }
      );


    setInterval(() => {

      const video =
        document.getElementById('video');


      if (
        !stream ||
        video.readyState < 2 ||
        cooldown
      ) {

        return;

      }


      canvas.width = 48;
      canvas.height = 48;


      ctx.drawImage(
        video,
        25,
        25,
        Math.max(
          1,
          video.videoWidth - 50
        ),
        Math.max(
          1,
          video.videoHeight - 50
        ),
        0,
        0,
        48,
        48
      );


      const data =
        ctx.getImageData(
          0,
          0,
          48,
          48
        ).data;


      let total = 0;


      for (
        let i = 0;
        i < data.length;
        i += 12
      ) {

        total +=
          Math.abs(data[i] - 128) +
          Math.abs(data[i + 1] - 128) +
          Math.abs(data[i + 2] - 128);

      }


      const sample =
        Math.round(
          total / (data.length / 12)
        );


      if (
        lastSample !== null &&
        Math.abs(
          sample - lastSample
        ) > 12 &&
        Date.now() - lastTap > 3500
      ) {

        lastTap = Date.now();

        tap();

      }


      lastSample = sample;

    }, 300);

  </script>

</body>
</html>

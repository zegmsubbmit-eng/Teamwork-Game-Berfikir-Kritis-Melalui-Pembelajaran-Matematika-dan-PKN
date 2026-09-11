<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
  <meta name="theme-color" content="#1e2a4a" />
  <title>Lintasan Matematika &amp; PKN · P1 vs P2</title>
  <style>
    :root {
      --navy: #1e2a4a;
      --paper: #f4efe4;
      --card: #fffdf8;
      --line: #d7cbb6;
      --ink: #222;
      --mute: #5b5348;
      --red: #9b1c1c;
      --p1: #2c4a7c;
      --p2: #2f5d3a;
      --tan: #efe6d6;
    }
    * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
    html, body {
      margin: 0;
      height: 100%;
      background: var(--paper);
      color: var(--ink);
      font: 16px/1.45 Georgia, "Times New Roman", serif;
      overflow: hidden;
    }
    button { font: inherit; cursor: pointer; }
    .screen { display: none; height: 100dvh; }
    .screen.on { display: flex; flex-direction: column; }

    .awal {
      max-width: 720px;
      margin: 0 auto;
      padding: 20px 16px 32px;
      overflow: auto;
    }
    .badge {
      font-family: Arial, Helvetica, sans-serif;
      font-size: 11px;
      letter-spacing: .14em;
      text-transform: uppercase;
      color: var(--navy);
    }
    h1 { color: var(--navy); font-size: 28px; line-height: 1.2; margin: 8px 0 10px; }
    .box {
      background: var(--card);
      border: 1px solid var(--line);
      padding: 14px 16px;
      margin: 12px 0 0;
    }
    .mulai {
      width: 100%;
      margin-top: 18px;
      background: var(--navy);
      color: #fff;
      border: 0;
      padding: 16px;
      font-family: Arial, Helvetica, sans-serif;
      font-size: 16px;
    }
    .nama-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 12px; }
    .nama-row label { display: block; font-family: Arial, Helvetica, sans-serif; font-size: 12px; margin-bottom: 4px; }
    .nama-row input {
      width: 100%;
      padding: 10px;
      border: 1px solid var(--line);
      background: var(--card);
      font: 16px Arial, Helvetica, sans-serif;
    }
    .p1c { color: var(--p1); }
    .p2c { color: var(--p2); }

    .play-top {
      flex: 0 0 auto;
      background: var(--card);
      border-bottom: 3px solid var(--navy);
      padding: 8px 12px 10px;
    }
    .meta {
      display: flex;
      justify-content: space-between;
      gap: 8px;
      font-family: Arial, Helvetica, sans-serif;
      font-size: 12px;
      color: var(--mute);
    }
    .soal {
      margin: 6px 0 0;
      color: var(--navy);
      font-size: clamp(16px, 3.4vw, 22px);
    }
    .timer {
      font-family: Arial, Helvetica, sans-serif;
      font-weight: bold;
      color: var(--red);
    }

    .arena {
      flex: 1;
      display: grid;
      grid-template-columns: 1fr 1fr;
      min-height: 0;
    }
    .panel {
      padding: 10px;
      display: flex;
      flex-direction: column;
      min-height: 0;
      overflow: hidden;
    }
    .panel.p1 { background: #e8eef6; border-right: 2px solid var(--navy); }
    .panel.p2 { background: #e7f0e8; }
    .who {
      font-family: Arial, Helvetica, sans-serif;
      font-size: 13px;
      letter-spacing: .08em;
      text-transform: uppercase;
      margin-bottom: 6px;
    }
    .panel.p1 .who { color: var(--p1); }
    .panel.p2 .who { color: var(--p2); }
    .track {
      display: grid;
      grid-template-columns: repeat(10, 1fr);
      gap: 3px;
      margin-bottom: 8px;
    }
    .tile {
      height: 14px;
      border: 1px solid var(--line);
      background: var(--card);
    }
    .panel.p1 .tile.on { background: var(--p1); border-color: var(--p1); }
    .panel.p2 .tile.on { background: var(--p2); border-color: var(--p2); }
    .ops {
      flex: 1;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      min-height: 0;
    }
    .ops button {
      border: 2px solid var(--line);
      background: var(--card);
      padding: 8px;
      text-align: left;
      font-family: Arial, Helvetica, sans-serif;
      font-size: clamp(13px, 2.4vw, 16px);
      line-height: 1.3;
    }
    .ops button:disabled { opacity: .85; cursor: default; }
    .ops button.pick { outline: 3px solid currentColor; }
    .panel.p1 .ops button.pick { color: var(--p1); border-color: var(--p1); }
    .panel.p2 .ops button.pick { color: var(--p2); border-color: var(--p2); }
    .ops button.benar { background: #d7ead8; border-color: var(--p2); }
    .ops button.salah { background: #f3d6d6; border-color: var(--red); }
    .status {
      margin-top: 8px;
      min-height: 1.3em;
      font-family: Arial, Helvetica, sans-serif;
      font-size: 13px;
    }

    .hasil { padding: 24px 16px; overflow: auto; text-align: center; }
    .skorbesar { font-size: 42px; margin: 8px 0; color: var(--navy); }
    @media (max-width: 720px) and (orientation: portrait) {
      .arena { grid-template-columns: 1fr; grid-template-rows: 1fr 1fr; }
      .panel.p1 { border-right: 0; border-bottom: 2px solid var(--navy); }
      .ops { grid-template-columns: 1fr 1fr; }
      h1 { font-size: 22px; }
    }
  </style>
</head>
<body>
  <section class="screen on" id="layarAwal">
    <div class="awal">
      <p class="badge">Game terpisah · bukan bagian website infografis</p>
      <h1>Lintasan Matematika &amp; PKN</h1>
      <p>Dua pemain, satu layar. Soal diambil dari materi situs Kelompok 1 kelas 8E: menjodohkan Matematika dengan Pancasila, plus data angket 9 September 2026.</p>
      <div class="box">
        <strong>Cara main</strong>
        <p>Ada 10 pos di lintasan. Soal muncul di atas. Pemain 1 dan Pemain 2 menjawab di sisi masing-masing. Jawaban benar = maju 1 pos. Waktu 20 detik. Setelah 10 soal, yang posnya lebih jauh menang.</p>
      </div>
      <div class="nama-row">
        <div>
          <label class="p1c" for="n1">Pemain 1</label>
          <input id="n1" maxlength="16" value="Pemain 1" />
        </div>
        <div>
          <label class="p2c" for="n2">Pemain 2</label>
          <input id="n2" maxlength="16" value="Pemain 2" />
        </div>
      </div>
      <button class="mulai" id="btnMulai" type="button">Mulai lintasan</button>
    </div>
  </section>

  <section class="screen" id="layarMain">
    <div class="play-top">
      <div class="meta">
        <span id="nomorSoal">Pos 1 / 10</span>
        <span class="timer" id="timer">20</span>
      </div>
      <p class="soal" id="teksSoal"></p>
    </div>
    <div class="arena">
      <div class="panel p1">
        <div class="who" id="label1">Pemain 1 · 0</div>
        <div class="track" id="track1"></div>
        <div class="ops" id="ops1"></div>
        <div class="status" id="st1"></div>
      </div>
      <div class="panel p2">
        <div class="who" id="label2">Pemain 2 · 0</div>
        <div class="track" id="track2"></div>
        <div class="ops" id="ops2"></div>
        <div class="status" id="st2"></div>
      </div>
    </div>
  </section>

  <section class="screen" id="layarHasil">
    <div class="hasil">
      <p class="badge">Garis finis</p>
      <h1 id="judulHasil">Hasil</h1>
      <p class="skorbesar" id="skorHasil"></p>
      <p id="ketHasil"></p>
      <button class="mulai" id="btnUlang" type="button">Main lagi</button>
    </div>
  </section>

  <script>
    const SOAL = [
      {
        t: "Pos 1 · Aljabar. Sederhanakan 3x + 2x + 5.",
        o: ["5x + 5", "6x", "3x + 7", "5x + 10"],
        k: 0
      },
      {
        t: "Pos 2 · Pasangan PKN untuk aljabar. Aturan yang bisa dihitung cocok dengan nilai apa?",
        o: ["Tata tertib harus jelas supaya adil (sila ke-5)", "Yang suaranya paling keras yang menang", "Aturan tidak perlu dijelaskan", "Boleh tebak-tebakan saja"],
        k: 0
      },
      {
        t: "Pos 3 · Peluang. Dari 10 kartu nama, 3 bertuliskan “setuju”. Peluang kartu “setuju” terambil?",
        o: ["3/10", "10/3", "1/3", "3"],
        k: 0
      },
      {
        t: "Pos 4 · 3/10 belum boleh disebut “hampir seluruh kelas setuju”. Sikap PKN yang tepat?",
        o: ["Musyawarah (sila ke-4) memakai data, bukan desas-desus", "Langsung umunkan hasil ke seluruh sekolah", "Abaikan angka, ikut teman saja", "Buang sampel supaya kelihatan besar"],
        k: 0
      },
      {
        t: "Pos 5 · Bilangan bulat. Hasil (+7) + (−7) dan pasangan PKN-nya?",
        o: ["0 · hak dan kewajiban harus seimbang", "14 · hak boleh tanpa kewajiban", "7 · kewajiban saja yang dihitung", "−14 · kas kelas selalu minus"],
        k: 0
      },
      {
        t: "Pos 6 · Persamaan. 6 kelompok membagi 24 tugas piket sama rata. Tiap kelompok mendapat…",
        o: ["4 tugas, karena 6x = 24", "6 tugas", "24 tugas", "5 tugas"],
        k: 0
      },
      {
        t: "Pos 7 · Perbandingan senilai. 2 guru mendampingi 3 kelompok. Untuk 6 kelompok diperlukan…",
        o: ["4 guru", "2 guru", "6 guru", "3 guru"],
        k: 0
      },
      {
        t: "Pos 8 · Angket kelas 8E, 9 September 2026 (32 siswa). Hambatan dengan jumlah orang terbanyak?",
        o: ["Kesulitan memahami / mengerjakan tugas (7)", "Mengantuk (6)", "Kelelahan / capek (5)", "Terdistraksi HP (4)"],
        k: 0
      },
      {
        t: "Pos 9 · Data angket. Mengapa jumlah jawaban bisa lebih dari 32?",
        o: ["Satu siswa boleh menuliskan lebih dari satu hambatan", "Ada kelas lain yang dihitung", "Setiap orang dihitung 32 kali", "Diagramnya otomatis menambah angka"],
        k: 0
      },
      {
        t: "Pos 10 · Bangun datar + PKN. Pojok baca 3 m × 2 m luasnya, dan maknanya?",
        o: ["6 m² · fasilitas sekolah milik bersama", "5 m² · barang boleh ditaruh semaunya", "32 m² · tidak perlu diukur", "3 m² · milik satu orang saja"],
        k: 0
      }
    ];

    const n1 = document.getElementById("n1");
    const n2 = document.getElementById("n2");

    let i = 0;
    let skor = [0, 0];
    let pilih = [null, null];
    let terkunci = [false, false];
    let sisa = 20;
    let jam = null;
    let nama = ["Pemain 1", "Pemain 2"];

    function acakOpsi(soal) {
      const pasang = soal.o.map((teks, idx) => ({ teks, benar: idx === soal.k }));
      for (let a = pasang.length - 1; a > 0; a--) {
        const b = Math.floor(Math.random() * (a + 1));
        const tmp = pasang[a];
        pasang[a] = pasang[b];
        pasang[b] = tmp;
      }
      return pasang;
    }

    function buatTrack(id) {
      const el = document.getElementById(id);
      el.innerHTML = "";
      for (let n = 0; n < 10; n++) {
        const d = document.createElement("div");
        d.className = "tile";
        el.appendChild(d);
      }
    }

    function isiTrack() {
      [1, 2].forEach((p) => {
        const tiles = document.getElementById("track" + p).children;
        for (let n = 0; n < 10; n++) tiles[n].classList.toggle("on", n < skor[p - 1]);
        document.getElementById("label" + p).textContent = nama[p - 1] + " · " + skor[p - 1];
      });
    }

    function tampil(id) {
      document.querySelectorAll(".screen").forEach((s) => s.classList.remove("on"));
      document.getElementById(id).classList.add("on");
    }

    function muatSoal() {
      const s = SOAL[i];
      const opsi = acakOpsi(s);
      pilih = [null, null];
      terkunci = [false, false];
      sisa = 20;
      document.getElementById("nomorSoal").textContent = "Pos " + (i + 1) + " / 10";
      document.getElementById("teksSoal").textContent = s.t;
      document.getElementById("timer").textContent = sisa;
      document.getElementById("st1").textContent = "Pilih jawaban";
      document.getElementById("st2").textContent = "Pilih jawaban";
      [1, 2].forEach((p) => {
        const box = document.getElementById("ops" + p);
        box.innerHTML = "";
        opsi.forEach((item, idx) => {
          const b = document.createElement("button");
          b.type = "button";
          b.textContent = item.teks;
          b.dataset.benar = item.benar ? "1" : "0";
          b.addEventListener("click", () => jawab(p - 1, idx, box));
          box.appendChild(b);
        });
      });
      isiTrack();
      clearInterval(jam);
      jam = setInterval(() => {
        sisa -= 1;
        document.getElementById("timer").textContent = Math.max(0, sisa);
        if (sisa <= 0) {
          terkunci = [true, true];
          selesaiSoal();
        }
      }, 1000);
    }

    function jawab(pemain, idx, box) {
      if (terkunci[pemain]) return;
      pilih[pemain] = idx;
      [...box.children].forEach((b, n) => b.classList.toggle("pick", n === idx));
      document.getElementById("st" + (pemain + 1)).textContent = "Jawaban dikunci";
      terkunci[pemain] = true;
      if (terkunci[0] && terkunci[1]) selesaiSoal();
    }

    function selesaiSoal() {
      clearInterval(jam);
      [1, 2].forEach((p) => {
        const box = document.getElementById("ops" + p);
        const tombol = [...box.children];
        tombol.forEach((b) => {
          b.disabled = true;
          if (b.dataset.benar === "1") b.classList.add("benar");
        });
        const pick = pilih[p - 1];
        let ok = false;
        if (pick !== null) {
          ok = tombol[pick].dataset.benar === "1";
          if (!ok) tombol[pick].classList.add("salah");
        }
        if (ok) {
          skor[p - 1] += 1;
          document.getElementById("st" + p).textContent = "Benar, maju 1 pos!";
        } else {
          document.getElementById("st" + p).textContent = pick === null ? "Waktu habis" : "Belum tepat, tetap di pos";
        }
      });
      isiTrack();
      setTimeout(() => {
        i += 1;
        if (i >= SOAL.length) finis();
        else muatSoal();
      }, 1600);
    }

    function finis() {
      tampil("layarHasil");
      document.getElementById("skorHasil").textContent = skor[0] + " — " + skor[1];
      let judul = "Seri!";
      let ket = nama[0] + " dan " + nama[1] + " sama-sama di pos " + skor[0] + ".";
      if (skor[0] > skor[1]) {
        judul = nama[0] + " sampai lebih dulu";
        ket = "Lintasan dimenangkan " + nama[0] + " dengan " + skor[0] + " pos benar.";
      } else if (skor[1] > skor[0]) {
        judul = nama[1] + " sampai lebih dulu";
        ket = "Lintasan dimenangkan " + nama[1] + " dengan " + skor[1] + " pos benar.";
      }
      document.getElementById("judulHasil").textContent = judul;
      document.getElementById("ketHasil").textContent = ket + " Soal ini menyambung ke infografis dan data angket di situs kelompok.";
    }

    document.getElementById("btnMulai").addEventListener("click", () => {
      nama[0] = (n1.value || "Pemain 1").trim().slice(0, 16);
      nama[1] = (n2.value || "Pemain 2").trim().slice(0, 16);
      i = 0;
      skor = [0, 0];
      buatTrack("track1");
      buatTrack("track2");
      tampil("layarMain");
      muatSoal();
    });

    document.getElementById("btnUlang").addEventListener("click", () => {
      tampil("layarAwal");
    });
  </script>
</body>
</html>

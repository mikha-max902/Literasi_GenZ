
# Literasi_GenZ
Web interaktif untuk meningkatkan literasi membaca Generasi Z
literasi_genz/
│
├── index.html
├── style.css
└── script.js
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Literasi Gen Z - Interaktif</title>
  <link rel="stylesheet" href="style.css">
</head>
<body data-theme="light">

<button class="dark-mode-toggle" onclick="toggleTheme()">Dark/Light Mode</button>

<header>
  <h1>Literasi Gen Z</h1>
  <p>Uji Literasimu, Seru & Interaktif!</p>
</header>

<nav>
  <a href="#bacaan">Bacaan Acak</a>
  <a href="#pertanyaan">Pertanyaan Interaktif</a>
  <a href="#statistik">Statistik</a>
  <a href="#about">Tentang</a>
</nav>

<div class="container" id="bacaan">
  <h2>Bacaan Acak</h2>
  <p id="textBacaan">Klik tombol untuk menampilkan bacaan acak.</p>
  <button onclick="acakBacaan()">Bacaan Berikutnya</button>
</div>

<div class="container" id="pertanyaan">
  <h2>Pertanyaan Interaktif</h2>
  <p id="textPertanyaan">Klik tombol untuk menampilkan pertanyaan acak.</p>
  <div class="choices" id="choices"></div>
  <p id="feedback"></p>
</div>

<div class="container" id="statistik">
  <h2>Skor & Statistik</h2>
  <p id="skor">Skor: 0</p>
  <p id="total">Pertanyaan dijawab: 0</p>
</div>

<div class="container" id="about">
  <h2>Tentang</h2>
  <p>Web ini dibuat untuk meningkatkan literasi membaca Gen Z secara interaktif, menampilkan bacaan dan pertanyaan acak, serta memberikan skor berdasarkan jawaban yang benar.</p>
</div>

<footer>
  &copy; 2025 Literasi Gen Z
</footer>

<script src="script.js"></script>
</body>
</html>
:root {
  --bg-color: #f0f4f8;
  --text-color: #333;
  --primary-color: #4f46e5;
  --secondary-color: #6366f1;
}

[data-theme="dark"] {
  --bg-color: #1f2937;
  --text-color: #f3f4f6;
  --primary-color: #818cf8;
  --secondary-color: #4f46e5;
}

body {
  font-family: Arial, sans-serif;
  margin: 0; padding: 0;
  background-color: var(--bg-color);
  color: var(--text-color);
  transition: all 0.3s;
}

header {
  background-color: var(--primary-color);
  color: white;
  padding: 1rem;
  text-align: center;
}

nav {
  display: flex;
  justify-content: center;
  gap: 1rem;
  background-color: var(--secondary-color);
  padding: 0.5rem 0;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.container {
  max-width: 800px;
  margin: 2rem auto;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  transition: all 0.3s;
}

button {
  background-color: var(--primary-color);
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 1rem;
  transition: 0.2s;
}

button:hover {
  background-color: var(--secondary-color);
}

.choices {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.choice-btn {
  padding: 0.5rem;
  border-radius: 5px;
  border: 1px solid var(--primary-color);
  background-color: white;
  cursor: pointer;
  transition: 0.2s;
}

.choice-btn:hover {
  background-color: var(--primary-color);
  color: white;
}

footer {
  text-align: center;
  padding: 1rem;
  background-color: #e0e7ff;
  margin-top: 2rem;
}

.dark-mode-toggle {
  position: fixed;
  top: 1rem;
  right: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: var(--primary-color);
  color: white;
}
const bacaan = [
  "Generasi Z cenderung suka membaca konten singkat di media sosial.",
  "Scroll culture memengaruhi cara Gen Z memahami teks panjang.",
  "Literasi digital perlu ditingkatkan agar membaca lebih kritis."
];

const pertanyaan = [
  {
    q: "Apa yang dimaksud dengan scroll culture?",
    choices: ["Budaya membaca teks panjang", "Budaya menggulir layar cepat", "Budaya menulis artikel", "Budaya menonton film"],
    answer: 1
  },
  {
    q: "Sebutkan salah satu dampak scroll culture pada Gen Z!",
    choices: ["Pemahaman mendalam", "Rendahnya fokus membaca", "Meningkatkan literasi kritis", "Mengurangi waktu online"],
    answer: 1
  },
  {
    q: "Bagaimana cara meningkatkan literasi digital Gen Z?",
    choices: ["Membaca konten panjang rutin", "Scrolling tanpa batas", "Menghapus buku", "Mengurangi belajar online"],
    answer: 0
  }
];

let skor = 0;
let totalJawab = 0;
let currentIndex = null;

function acakBacaan() {
  const index = Math.floor(Math.random() * bacaan.length);
  document.getElementById('textBacaan').innerText = bacaan[index];
}

function acakPertanyaan() {
  currentIndex = Math.floor(Math.random() * pertanyaan.length);
  const q = pertanyaan[currentIndex];
  document.getElementById('textPertanyaan').innerText = q.q;
  const choicesDiv = document.getElementById('choices');
  choicesDiv.innerHTML = '';
  q.choices.forEach((choice, index) => {
    const btn = document.createElement('button');
    btn.innerText = choice;
    btn.className = 'choice-btn';
    btn.onclick = () => cekJawaban(index);
    choicesDiv.appendChild(btn);
  });
  document.getElementById('feedback').innerText = '';
}

function cekJawaban(selected) {
  const q = pertanyaan[currentIndex];
  totalJawab++;
  if (selected === q.answer) {
    skor++;
    document.getElementById('feedback').innerText = 'Jawaban Benar!';
  } else {
    document.getElementById('feedback').innerText = 'Jawaban Salah!';
  }
  updateSkor();
}

function updateSkor() {
  document.getElementById('skor').innerText = `Skor: ${skor}`;
  document.getElementById('total').innerText = `Pertanyaan dijawab: ${totalJawab}`;
}

function toggleTheme() {
  const body = document.body;
  const currentTheme = body.getAttribute('data-theme');
  body.setAttribute('data-theme', currentTheme === 'light' ? 'dark' : 'light');
}

// Inisialisasi
acakBacaan();
acakPertanyaan();

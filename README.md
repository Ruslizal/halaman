# halaman
followers
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>RUSLIZAL</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @keyframes kedip {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }
    .animate-kedip {
      animation: kedip 1s infinite;
    }
  </style>
</head>
<body class="bg-gray-900 text-white min-h-screen relative overflow-hidden">

  <!-- Lampu Warna-Warni -->
  <div class="fixed inset-0 -z-10 overflow-hidden">
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-gradient-to-r from-pink-500 via-purple-500 to-blue-500 opacity-20 rounded-full blur-3xl animate-pulse"></div>
  </div>

  <!-- Judul -->
  <header class="text-center py-10">
    <h1 class="text-4xl font-bold text-blue-400 animate-kedip">RUSLIZAL</h1>
    <p class="text-gray-400 mt-2">Cek harga & pesan followers dengan mudah</p>
  </header>

  <!-- Formulir -->
  <main class="max-w-xl mx-auto bg-gray-800 shadow-2xl rounded-2xl p-6 space-y-5">

    <!-- Platform -->
    <div>
      <label class="block mb-1 font-medium">Pilih Platform</label>
      <select id="platform" onchange="updateServiceOptions()" class="w-full p-3 rounded-lg bg-gray-900 border border-gray-700">
        <option value="">-- Pilih Platform --</option>
        <option value="instagram">Instagram</option>
        <option value="tiktok">TikTok</option>
        <option value="youtube">YouTube</option>
        <option value="facebook">Facebook</option>
      </select>
    </div>

    <!-- Layanan -->
    <div>
      <label class="block mb-1 font-medium">Pilih Layanan</label>
      <select id="layanan" onchange="updateWA()" class="w-full p-3 rounded-lg bg-gray-900 border border-gray-700">
        <option value="">-- Pilih Layanan --</option>
      </select>
    </div>

    <!-- Username -->
    <div>
      <label class="block mb-1 font-medium">Username Akun</label>
      <input type="text" id="username" placeholder="@namauser" oninput="updateWA()" class="w-full p-3 rounded-lg bg-gray-900 border border-gray-700" />
    </div>

    <!-- Jumlah -->
    <div>
      <label class="block mb-1 font-medium">Jumlah</label>
      <input type="number" id="jumlah" oninput="updateWA()" class="w-full p-3 rounded-lg bg-gray-900 border border-gray-700" />
    </div>

    <!-- Total Harga -->
    <div>
      <label class="block mb-1 font-medium">Total Harga</label>
      <div id="totalHarga" class="text-xl font-bold text-yellow-400">Rp 0</div>
    </div>

    <!-- Tombol WhatsApp -->
    <a id="linkWA" target="_blank" class="block w-full text-center py-3 bg-gray-700 text-white font-bold rounded-lg opacity-50 pointer-events-none transition">
      Kirim ke WhatsApp
    </a>
  </main>

  <footer class="text-center text-sm text-gray-500 mt-10">
    &copy; 2025 RUSLIZAL
  </footer>

  <!-- Script -->
  <script>
    const layananData = {
      instagram: {
        followers: 4500,
        like: 1000,
        views: 100,
        favorit: 2000
      },
      tiktok: {
        followers: 5000,
        like: 1000,
        views: 100
      },
      youtube: {
        subscribers: 2000,
        like: 1000,
        views: 1500
      },
      facebook: {
        likes: 800,
        followers: 1000,
        shares: 1100
      }
    };

    const layananLabels = {
      followers: "Followers",
      like: "Like",
      views: "Views",
      favorit: "Favorit",
      subscribers: "Subscribers",
      likes: "Likes",
      shares: "Shares"
    };

    function updateServiceOptions() {
      const platform = document.getElementById("platform").value;
      const layananSelect = document.getElementById("layanan");
      layananSelect.innerHTML = `<option value="">-- Pilih Layanan --</option>`;

      if (platform && layananData[platform]) {
        for (let layanan in layananData[platform]) {
          const option = document.createElement("option");
          option.value = layanan;
          option.textContent = layananLabels[layanan];
          layananSelect.appendChild(option);
        }
      }

      updateWA();
    }

    function updateWA() {
      const username = document.getElementById("username").value.trim();
      const jumlah = parseInt(document.getElementById("jumlah").value.trim());
      const platform = document.getElementById("platform").value;
      const layanan = document.getElementById("layanan").value;

      const waButton = document.getElementById("linkWA");

      let harga = 0;
      if (platform && layanan && jumlah) {
        const hargaPer100 = layananData[platform]?.[layanan] || 0;
        harga = Math.ceil((jumlah / 100) * hargaPer100);
        document.getElementById("totalHarga").textContent = `Rp ${harga.toLocaleString()}`;
      } else {
        document.getElementById("totalHarga").textContent = `Rp 0`;
      }

      const valid = username !== "" && jumlah > 0 && platform !== "" && layanan !== "";

      if (valid) {
        const pesan = 
`Halo Admin, saya ingin memesan:

Username: ${username}
Platform: ${capitalize(platform)}
Layanan: ${layananLabels[layanan]}
Jumlah: ${jumlah}
Total Harga: Rp ${harga.toLocaleString()}`;

        const encoded = encodeURIComponent(pesan);
        const waNumber = "6282129111408";
        waButton.href = `https://wa.me/${waNumber}?text=${encoded}`;
        waButton.classList.remove("opacity-50", "pointer-events-none", "bg-gray-700");
        waButton.classList.add("bg-green-600", "hover:bg-green-700");
      } else {
        waButton.href = "#";
        waButton.classList.add("opacity-50", "pointer-events-none", "bg-gray-700");
        waButton.classList.remove("bg-green-600", "hover:bg-green-700");
      }
    }

    function capitalize(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }

    window.onload = updateServiceOptions;
  </script>
</body>
</html>

# games
Game Interaktif
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Media Pembelajaran IPAS Kelas 6: Macam-macam Benua</title>
    <!-- Memuat Tailwind CSS untuk styling responsif dan modern -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Menggunakan font Inter */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6; /* Abu-abu muda */
        }
        /* Style untuk kartu benua */
        .continent-card {
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            background-color: white;
            border-radius: 1rem; /* Sudut membulat */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* Bayangan lembut */
        }
        .continent-card:hover {
            transform: translateY(-5px); /* Efek angkat saat di-hover */
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        /* Style untuk modal/popup */
        .modal {
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
        }
        .modal-content {
            max-width: 90%;
            max-height: 90vh;
            overflow-y: auto;
            border-radius: 1rem;
        }
        /* Style untuk gambar media card agar terpotong rapi */
        .media-card-img {
            height: 100px; /* Tinggi tetap untuk mobile */
        }
        @media (min-width: 640px) {
            .media-card-img {
                height: 120px; /* Tinggi sedikit lebih besar di desktop */
            }
        }
    </style>
</head>
<body class="p-4 sm:p-8">

    <!-- Header Aplikasi -->
    <header class="text-center mb-8">
        <h1 class="text-3xl sm:text-4xl font-extrabold text-blue-800">Media Pembelajaran Interaktif Benua</h1>
        <p class="mt-2 text-lg text-gray-600">IPAS Kelas 6: Karakteristik, Batas, dan Hal Penting Benua di Dunia</p>
    </header>

    <!-- Konten Utama: Daftar Benua -->
    <main id="continent-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 max-w-7xl mx-auto">
        <!-- Kartu Benua akan dimasukkan oleh JavaScript -->
    </main>

    <!-- Modal (Popup) untuk Detail Benua -->
    <div id="continent-modal" class="modal fixed inset-0 hidden items-center justify-center p-4">
        <div class="modal-content bg-white p-6 sm:p-8 shadow-2xl w-full lg:w-3/5">
            <div class="flex justify-between items-center border-b pb-3 mb-4">
                <h2 id="modal-title" class="text-2xl sm:text-3xl font-bold text-blue-700">Detail Benua</h2>
                <button id="close-modal-btn" class="text-gray-500 hover:text-gray-800 text-3xl font-light leading-none">
                    &times;
                </button>
            </div>
            
            <!-- Konten Detail -->
            <div id="modal-content-body" class="space-y-6 text-gray-700">
                
                <!-- Peta Benua -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-blue-500 pl-2">Peta & Gambaran Umum</h3>
                    <img id="modal-map-image" class="w-full h-auto rounded-lg mt-2 shadow-md object-cover" src="" alt="Peta Benua" onerror="this.onerror=null;this.src='https://placehold.co/600x300/CCCCCC/333333?text=Peta+Tidak+Tersedia';">
                </section>
                
                <!-- Karakteristik -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-yellow-500 pl-2">Karakteristik Utama</h3>
                    <p id="modal-karakteristik" class="mt-2 text-base"></p>
                </section>

                <!-- Batas Benua -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-yellow-500 pl-2">Batas-batas Wilayah</h3>
                    <ul id="modal-batas" class="list-disc list-inside mt-2 space-y-1 text-base pl-4"></ul>
                </section>

                <!-- Fauna Endemik Khas -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-green-500 pl-2">Fauna Endemik Khas</h3>
                    <div id="modal-fauna" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 mt-2">
                        <!-- Konten Fauna dimuat oleh JS -->
                    </div>
                </section>
                
                <!-- Flora Khas & Hasil Bumi -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-orange-500 pl-2">Flora Khas & Hasil Bumi</h3>
                    <div id="modal-flora" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 mt-2">
                         <!-- Konten Flora dimuat oleh JS -->
                    </div>
                </section>
                
                <!-- Suku Asli/Penduduk Pribumi -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-red-500 pl-2">Suku Asli & Penduduk Pribumi</h3>
                    <div id="modal-indigenous" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 mt-2">
                         <!-- Konten Suku Asli dimuat oleh JS -->
                    </div>
                </section>
                
                <!-- Hal Penting/Fakta Menarik -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-900 border-l-4 border-purple-500 pl-2">Hal Penting & Fakta Menarik</h3>
                    <ul id="modal-fakta" class="list-disc list-inside mt-2 space-y-1 text-base pl-4"></ul>
                </section>
                
            </div>

            <!-- Catatan Footer -->
            <footer class="mt-6 pt-4 border-t text-sm text-gray-500">
                <p>Pelajari lebih lanjut tentang keajaiban setiap benua!</p>
            </footer>
        </div>
    </div>

    <script>
        // Data Benua - DITINGKATKAN dengan data gambar placeholder untuk Peta, Fauna, Flora, dan Suku Asli
        const continentsData = [
            {
                name: "Asia",
                icon: "🌏",
                color: "bg-red-500",
                mapImage: "https://placehold.co/600x300/F87171/ffffff?text=PETA+ASIA",
                karakteristik: "Benua terluas di dunia (± 44 juta km²). Merupakan tempat lahirnya agama-agama besar. Terletak di Timur dan Utara Bumi.",
                batas: [
                    "Utara: Samudra Arktik", "Timur: Samudra Pasifik, Selat Bering",
                    "Selatan: Samudra Hindia", "Barat: Benua Eropa (Pegunungan Ural), Laut Merah, Laut Tengah"
                ],
                fakta: ["Memiliki gunung tertinggi di dunia: Gunung Everest.", "Populasi terpadat di dunia.", "Terbagi menjadi Asia Timur, Asia Tenggara, Asia Selatan, Asia Barat, dan Asia Tengah."],
                indigenous: [
                    { name: "Suku Ainu", image: "https://placehold.co/150x100/DC2626/ffffff?text=Suku+Ainu", description: "Jepang" },
                    { name: "Suku Tamil", image: "https://placehold.co/150x100/DC2626/ffffff?text=Suku+Tamil", description: "India/Sri Lanka" }
                ],
                fauna: [
                    { name: "Harimau Siberia", image: "https://placehold.co/150x100/10B981/ffffff?text=Harimau+Siberia", description: "Asia Utara" },
                    { name: "Panda Raksasa", image: "https://placehold.co/150x100/10B981/ffffff?text=Panda", description: "Tiongkok" }
                ],
                flora: [
                    { name: "Bambu", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Bambu", description: "Tanaman serbaguna" },
                    { name: "Padi", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Padi", description: "Makanan pokok" }
                ]
            },
            {
                name: "Amerika",
                icon: "🗽",
                color: "bg-blue-500",
                mapImage: "https://placehold.co/600x300/3B82F6/ffffff?text=PETA+AMERIKA",
                karakteristik: "Benua memanjang dari Kutub Utara hingga Kutub Selatan. Sering disebut sebagai 'Dunia Baru'. Dibagi menjadi Amerika Utara, Tengah, dan Selatan.",
                batas: [
                    "Utara: Samudra Arktik", "Timur: Samudra Atlantik",
                    "Selatan: Samudra Pasifik, Samudra Atlantik", "Barat: Samudra Pasifik"
                ],
                fakta: ["Memiliki sungai terpanjang di dunia (Sungai Amazon) dan air terjun tertinggi (Air Terjun Angel).", "Dikenal dengan Keragaman Suku Indian (penduduk asli).", "Di Amerika Utara terdapat Danau Superior, danau air tawar terluas di dunia."],
                indigenous: [
                    { name: "Suku Indian", image: "https://placehold.co/150x100/2563EB/ffffff?text=Suku+Indian", description: "Amerika Utara" },
                    { name: "Suku Maya", image: "https://placehold.co/150x100/2563EB/ffffff?text=Suku+Maya", description: "Amerika Tengah" }
                ],
                fauna: [
                    { name: "Llama", image: "https://placehold.co/150x100/10B981/ffffff?text=Llama", description: "Amerika Selatan" },
                    { name: "Grizzly Bear", image: "https://placehold.co/150x100/10B981/ffffff?text=Grizzly+Bear", description: "Amerika Utara" }
                ],
                flora: [
                    { name: "Jagung", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Jagung", description: "Berasal dari Meksiko" },
                    { name: "Pohon Sequoia", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Sequoia", description: "Pohon tertinggi" }
                ]
            },
            {
                name: "Afrika",
                icon: "🦁",
                color: "bg-green-500",
                mapImage: "https://placehold.co/600x300/10B981/ffffff?text=PETA+AFRIKA",
                karakteristik: "Sering disebut 'Benua Hitam' karena mayoritas penduduknya berkulit gelap. Benua yang dilewati garis khatulistiwa dan memiliki banyak gurun (termasuk Gurun Sahara).",
                batas: [
                    "Utara: Laut Tengah, Benua Eropa", "Timur: Samudra Hindia, Laut Merah",
                    "Selatan: Samudra Atlantik, Samudra Hindia", "Barat: Samudra Atlantik"
                ],
                fakta: ["Memiliki gurun terluas di dunia: Gurun Sahara.", "Memiliki sungai terpanjang di dunia: Sungai Nil.", "Hampir seluruh wilayahnya beriklim tropis."],
                indigenous: [
                    { name: "Suku Masai", image: "https://placehold.co/150x100/059669/ffffff?text=Suku+Masai", description: "Kenya/Tanzania" },
                    { name: "Suku Zulu", image: "https://placehold.co/150x100/059669/ffffff?text=Suku+Zulu", description: "Afrika Selatan" }
                ],
                fauna: [
                    { name: "Singa", image: "https://placehold.co/150x100/10B981/ffffff?text=Singa", description: "Raja hutan" },
                    { name: "Jerapah", image: "https://placehold.co/150x100/10B981/ffffff?text=Jerapah", description: "Hewan tertinggi" }
                ],
                flora: [
                    { name: "Pohon Baobab", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Baobab", description: "Pohon botol" },
                    { name: "Kopi", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Kopi", description: "Hasil utama Ethiopia" }
                ]
            },
            {
                name: "Eropa",
                icon: "🗼",
                color: "bg-indigo-500",
                mapImage: "https://placehold.co/600x300/6366F1/ffffff?text=PETA+EROPA",
                karakteristik: "Benua terkecil kedua setelah Australia. Memiliki sejarah peradaban maju dan sering disebut 'Benua Biru' karena mata biru penduduknya.",
                batas: [
                    "Utara: Samudra Arktik", "Timur: Benua Asia (Pegunungan Ural), Laut Kaspia",
                    "Selatan: Laut Tengah, Laut Hitam", "Barat: Samudra Atlantik"
                ],
                fakta: ["Merupakan cikal bakal perkembangan ilmu pengetahuan dan industri modern.", "Terbagi menjadi Eropa Utara, Timur, Barat, dan Selatan.", "Benua yang paling banyak dihuni oleh negara-negara maju."],
                indigenous: [
                    { name: "Suku Sami", image: "https://placehold.co/150x100/4F46E5/ffffff?text=Suku+Sami", description: "Skandinavia Utara" },
                    { name: "Suku Basque", image: "https://placehold.co/150x100/4F46E5/ffffff?text=Suku+Basque", description: "Spanyol/Prancis" }
                ],
                fauna: [
                    { name: "Rusa Merah", image: "https://placehold.co/150x100/10B981/ffffff?text=Rusa+Merah", description: "Hutan Eropa" },
                    { name: "Elang Emas", image: "https://placehold.co/150x100/10B981/ffffff?text=Elang+Emas", description: "Pegunungan Alpen" }
                ],
                flora: [
                    { name: "Bunga Tulip", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Tulip", description: "Belanda" },
                    { name: "Anggur", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Anggur", description: "Hasil utama" }
                ]
            },
            {
                name: "Australia",
                icon: "🦘",
                color: "bg-yellow-500",
                mapImage: "https://placehold.co/600x300/F59E0B/ffffff?text=PETA+AUSTRALIA",
                karakteristik: "Benua paling kecil dan paling datar. Sering disebut Benua Oceania karena meliputi banyak pulau di sekitarnya.",
                batas: [
                    "Utara: Laut Arafuru, Laut Timor, Selat Torres", "Timur: Samudra Pasifik",
                    "Selatan: Samudra Hindia", "Barat: Samudra Hindia"
                ],
                fakta: ["Hanya terdiri dari satu negara utama (Australia).", "Kangaroo dan Koala adalah fauna endemik yang terkenal.", "The Great Barrier Reef, terumbu karang terbesar di dunia, berada di lepas pantai timurnya."],
                indigenous: [
                    { name: "Suku Aborigin", image: "https://placehold.co/150x100/D97706/ffffff?text=Suku+Aborigin", description: "Australia" },
                    { name: "Suku Maori", image: "https://placehold.co/150x100/D97706/ffffff?text=Suku+Maori", description: "Selandia Baru" }
                ],
                fauna: [
                    { name: "Kangaroo", image: "https://placehold.co/150x100/10B981/ffffff?text=Kangaroo", description: "Hewan berkantung" },
                    { name: "Koala", image: "https://placehold.co/150x100/10B981/ffffff?text=Koala", description: "Hewan lucu" }
                ],
                flora: [
                    { name: "Eucalyptus", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Eucalyptus", description: "Pohon Khas" },
                    { name: "Gandum", image: "https://placehold.co/150x100/F59E0B/ffffff?text=Gandum", description: "Hasil utama" }
                ]
            }
        ];

        const gridContainer = document.getElementById('continent-grid');
        const modal = document.getElementById('continent-modal');
        const closeModalBtn = document.getElementById('close-modal-btn');

        /**
         * Fungsi pembantu untuk membuat kartu media (gambar + teks)
         * @param {object} item - Objek berisi nama, gambar (url), dan deskripsi
         */
        function createMediaCard(item) {
            return `
                <div class="bg-gray-50 rounded-lg shadow-sm overflow-hidden border border-gray-200">
                    <img src="${item.image}" alt="${item.name}" 
                         class="w-full media-card-img object-cover" 
                         onerror="this.onerror=null;this.src='https://placehold.co/150x100/AAAAAA/333333?text=Gambar+Rusak';"
                    >
                    <div class="p-2 text-center">
                        <p class="font-semibold text-sm text-gray-800 leading-tight">${item.name}</p>
                        <p class="text-xs text-gray-500 mt-1">${item.description}</p>
                    </div>
                </div>
            `;
        }

        /**
         * Fungsi untuk merender kartu benua di grid.
         */
        function renderContinentCards() {
            gridContainer.innerHTML = ''; // Kosongkan container
            
            continentsData.forEach(continent => {
                const card = document.createElement('div');
                card.classList.add('continent-card', 'p-6', continent.color, 'bg-opacity-20', 'shadow-lg', 'transform', 'hover:scale-[1.02]');
                card.setAttribute('data-continent-name', continent.name);

                card.innerHTML = `
                    <div class="text-4xl mb-4">${continent.icon}</div>
                    <h3 class="text-2xl font-bold text-gray-800 mb-2">${continent.name}</h3>
                    <p class="text-gray-600 text-sm">${continent.karakteristik.substring(0, 70)}...</p>
                    <button class="mt-4 text-sm font-semibold text-${continent.color.replace('bg-', '')}-700 hover:underline">
                        Lihat Detail →
                    </button>
                `;

                // Menambahkan event listener untuk menampilkan modal
                card.addEventListener('click', () => showContinentDetail(continent.name));
                gridContainer.appendChild(card);
            });
        }

        /**
         * Fungsi untuk menampilkan modal detail benua.
         * @param {string} name - Nama benua yang akan ditampilkan.
         */
        function showContinentDetail(name) {
            const continent = continentsData.find(c => c.name === name);

            if (!continent) return;

            document.getElementById('modal-title').textContent = `Detail Benua ${continent.name} ${continent.icon}`;
            
            // 1. Peta Benua
            document.getElementById('modal-map-image').src = continent.mapImage;
            
            // 2. Karakteristik
            document.getElementById('modal-karakteristik').textContent = continent.karakteristik;
            
            // 3. Batas
            const batasList = document.getElementById('modal-batas');
            batasList.innerHTML = continent.batas.map(item => `<li class="text-base">${item}</li>`).join('');

            // 4. Fauna Khas
            document.getElementById('modal-fauna').innerHTML = continent.fauna.map(createMediaCard).join('');

            // 5. Flora Khas
            document.getElementById('modal-flora').innerHTML = continent.flora.map(createMediaCard).join('');
            
            // 6. Suku Asli
            document.getElementById('modal-indigenous').innerHTML = continent.indigenous.map(createMediaCard).join('');
            
            // 7. Fakta Penting
            const faktaList = document.getElementById('modal-fakta');
            faktaList.innerHTML = continent.fakta.map(item => `<li class="text-base">${item}</li>`).join('');

            // Tampilkan modal
            modal.classList.remove('hidden');
            modal.classList.add('flex');
        }

        /**
         * Fungsi untuk menyembunyikan modal.
         */
        function hideModal() {
            modal.classList.add('hidden');
            modal.classList.remove('flex');
        }

        // Event listener untuk tombol tutup modal
        closeModalBtn.addEventListener('click', hideModal);

        // Event listener untuk menutup modal saat klik di luar area modal
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                hideModal();
            }
        });

        // Event listener untuk menutup modal saat tombol ESC ditekan
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && !modal.classList.contains('hidden')) {
                hideModal();
            }
        });

        // Inisialisasi: Render kartu saat halaman dimuat
        window.onload = renderContinentCards;
    </script>
</body>
</html>

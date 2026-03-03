```python
import os
import re
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
from tqdm import tqdm
from html_to_markdown import convert, ConversionOptions

# ==============================
# Configuration
# ==============================

# EN: Project name identifier used for naming the final markdown file
# ID: Nama proyek yang digunakan untuk penamaan file markdown akhir
NAME = "livewire-4x"

# EN: Base URL of the documentation website
# ID: URL utama dari website dokumentasi
BASE_URL = "https://livewire.laravel.com"

# EN: Starting page URL for crawling
# ID: URL halaman awal untuk proses crawling
START_URL = "https://livewire.laravel.com/docs/4.x/quickstart"

# EN: Base directory where all files will be stored
# ID: Direktori dasar tempat semua file akan disimpan
BASE_DIR = "docs/livewire-4x"

# EN: Directory to store downloaded HTML files
# ID: Direktori untuk menyimpan file HTML hasil download
OUTPUT_DIR = f"{BASE_DIR}/htmls"

# EN: Final combined markdown output file path
# ID: Path file markdown gabungan akhir
OUTPUT_MD = os.path.join(BASE_DIR, f"{NAME}.md")

# EN: Directory to store individual markdown files
# ID: Direktori untuk menyimpan file markdown satu per satu
OUTPUT_MD_DIR = os.path.join(BASE_DIR, "markdowns")

print("Configuration:")
print(f"BASE_URL   : {BASE_URL}")
print(f"START_URL  : {START_URL}")
print(f"BASE_DIR   : {BASE_DIR}")
print(f"OUTPUT_DIR : {OUTPUT_DIR}")
print("-" * 70)

# EN: Create output directory if it does not exist
# ID: Membuat folder output jika belum ada
os.makedirs(OUTPUT_DIR, exist_ok=True)

# EN: Create markdown directory if it does not exist
# ID: Membuat folder markdown jika belum ada
os.makedirs(OUTPUT_MD_DIR, exist_ok=True)

print(f"Output folder is ready: {os.path.abspath(OUTPUT_DIR)}")
print("-" * 70)

print("Markdown")
print(f"Source folder : {os.path.abspath(OUTPUT_DIR)}")
print(f"Output file   : {os.path.abspath(OUTPUT_MD)}")
print(f"Output folder   : {os.path.abspath(OUTPUT_MD_DIR)}")
print("-" * 70)

# EN: Custom headers to mimic a real browser request
# ID: Header request agar terlihat seperti browser asli
headers = {
    "User-Agent": "Mozilla/5.0"
}

# ==============================
# Step 1: Fetch start page
# ==============================

print("Fetching start page...")

# EN: Send HTTP GET request to start page
# ID: Mengirim request GET ke halaman awal
response = requests.get(START_URL, headers=headers)
response.raise_for_status()

print("Start page successfully fetched")

# EN: Parse HTML using BeautifulSoup
# ID: Parsing HTML menggunakan BeautifulSoup
soup = BeautifulSoup(response.text, "html.parser")

# ==============================
# Step 2: Take all links from the sidebar menu
# ==============================

print("Scanning sidebar menu...")

# EN: Find the <ul> element that contains documentation links
# ID: Mencari elemen <ul> yang berisi link dokumentasi
menu_ul = soup.find(
    "ul",
    class_="list-none space-y-5 divide-y divide-slate-700 px-3"
)

if menu_ul is None:
    raise Exception("Documentation menu not found!")

# EN: Extract all anchor tags that contain href attribute
# ID: Mengambil semua tag anchor yang memiliki atribut href
links = menu_ul.find_all("a", href=True)

# EN: Use set to avoid duplicate URLs
# ID: Menggunakan set untuk menghindari URL duplikat
seen_urls = set()

# EN: List to store final menu items (name and URL)
# ID: List untuk menyimpan nama menu dan URL final
final_items = []

for link in links:
    href = link["href"].strip()

    # EN: Only process internal documentation links
    # ID: Hanya memproses link dokumentasi internal
    if not href.startswith("/docs/4.x"):
        continue

    # EN: Convert relative URL to absolute URL
    # ID: Mengubah URL relatif menjadi URL absolut
    full_url = urljoin(BASE_URL, href)

    # EN: Skip duplicate URLs
    # ID: Lewati jika URL sudah pernah diproses
    if full_url in seen_urls:
        continue
    seen_urls.add(full_url)

    # EN: Extract menu text as file name
    # ID: Mengambil teks menu sebagai nama file
    menu_name = link.get_text(strip=True)

    # EN: Remove invalid characters for file names
    # ID: Menghapus karakter yang tidak valid untuk nama file
    safe_name = re.sub(r'[\\/*?:"<>|]', "", menu_name)

    final_items.append((safe_name, full_url))

print(f"Total menus found: {len(final_items)}")

# ==============================
# Step 3: Crawl each documentation page
# ==============================

print("Starting crawling process...")

for idx, (safe_name, url) in enumerate(tqdm(final_items), start=1):
    try:
        # EN: Send request to documentation page
        # ID: Mengirim request ke halaman dokumentasi
        r = requests.get(url, headers=headers)
        r.raise_for_status()

        # EN: Create 4-digit prefix for ordering
        # ID: Membuat prefix 4 digit untuk urutan file
        prefix = f"{idx:04d}"

        # EN: Construct HTML file name
        # ID: Membuat nama file HTML
        filename = f"{prefix}_{safe_name}.html"
        file_path = os.path.join(OUTPUT_DIR, filename)

        # EN: Save raw HTML to file
        # ID: Menyimpan HTML mentah ke file
        with open(file_path, "w", encoding="utf-8") as f:
            f.write(r.text)

    except Exception as e:
        print(f"Failed to download {url}: {e}")

print("Crawling finished.")

# ==============================
# Step 4: Convert HTML to individual Markdown files and single Markdown file
# ==============================

# EN: Get all HTML files and sort them by filename
# ID: Mengambil semua file HTML dan mengurutkannya berdasarkan nama file
html_files = sorted([
    f for f in os.listdir(OUTPUT_DIR)
    if f.endswith(".html")
])

print(f"Total HTML files found: {len(html_files)}")
print("-" * 70)

# EN: Configure markdown conversion options
# ID: Mengatur opsi konversi markdown
options = ConversionOptions(
    heading_style="atx",
    wrap=False
)

# EN: List to collect all markdown content for combined file
# ID: List untuk mengumpulkan semua markdown untuk file gabungan
all_markdown_content = []

for filename in tqdm(html_files):
    file_path = os.path.join(OUTPUT_DIR, filename)

    # EN: Read HTML file content
    # ID: Membaca isi file HTML
    with open(file_path, "r", encoding="utf-8") as f:
        html_content = f.read()

    soup = BeautifulSoup(html_content, "html.parser")

    # EN: Extract main documentation content div
    # ID: Mengambil div utama yang berisi konten dokumentasi
    content_div = soup.find(
        "div",
        class_="pt-12 docsearch-content overflow-hidden flex-1 mx-auto max-w-prose w-full"
    )

    if content_div is None:
        print(f"Content not found in: {filename}")
        continue

    # =====================================================
    # EN: Remove image-related tags if found
    # ID: Menghapus tag terkait gambar jika ditemukan
    # =====================================================

    image_tags = ["img", "svg", "picture", "source"]

    for tag in image_tags:
        found = content_div.find_all(tag)
        if found:
            for element in found:
                element.decompose()

    # EN: Convert cleaned HTML content to markdown
    # ID: Mengonversi HTML yang sudah dibersihkan menjadi markdown
    markdown = convert(str(content_div), options)

    # EN: Generate markdown filename using same prefix
    # ID: Membuat nama file markdown dengan prefix yang sama
    md_filename = filename.replace(".html", ".md")
    md_file_path = os.path.join(OUTPUT_MD_DIR, md_filename)

    # EN: Save individual markdown file
    # ID: Menyimpan file markdown satu per satu
    with open(md_file_path, "w", encoding="utf-8") as f:
        f.write(markdown)

    # EN: Add section header for combined markdown file
    # ID: Menambahkan header section untuk file markdown gabungan
    title = md_filename.replace(".md", "")
    section_header = f"\n\n# {title}\n\n"

    all_markdown_content.append(section_header + markdown)

# EN: Combine all markdown sections into one document
# ID: Menggabungkan semua bagian markdown menjadi satu dokumen
final_markdown = "\n\n".join(all_markdown_content)

# EN: Save final combined markdown file
# ID: Menyimpan file markdown gabungan akhir
with open(OUTPUT_MD, "w", encoding="utf-8") as f:
    f.write(final_markdown)

print("-" * 70)
print("Conversion completed.")
print(f"Individual markdown files saved in: {OUTPUT_MD_DIR}")
print(f"Combined markdown file created: {OUTPUT_MD}")
```

Saya sebelumnya telah berhasil melakukan crawling dokumentasi Livewire v4 menggunakan Python di Jupyter Lab seperti contoh di atas. Sekarang saya ingin melakukan crawling dokumentasi FluxUI v2 dari halaman berikut:

[https://fluxui.dev/docs/installation](https://fluxui.dev/docs/installation)

Tolong bantu saya membuat script dengan ketentuan berikut:

1. Saya menggunakan Jupyter Lab, sehingga kode harus langsung bisa dijalankan dalam bentuk sel Python.

2. Struktur langkah harus mengikuti pola yang sudah saya gunakan sebelumnya, yaitu:

   * Configuration
   * Step 1: Fetch start page
   * Step 2: Ambil semua link dari menu sidebar
   * Step 3: Crawl setiap halaman dokumentasi
   * Step 4: Convert HTML menjadi file Markdown terpisah dan satu file Markdown gabungan

3. Setiap bagian kode wajib memiliki komentar penjelasan dalam dua bahasa:

   * EN untuk penjelasan dalam bahasa Inggris
   * ID untuk penjelasan dalam bahasa Indonesia

4. Menu dokumentasi biasanya berada di dalam elemen berikut:
   ```html
   <ui-sidebar class="[grid-area:sidebar] z-1 flex flex-col gap-4 [:where(&amp;)]:w-64 p-4 data-flux-sidebar-collapsed-desktop:w-14 data-flux-sidebar-collapsed-desktop:px-2 data-flux-sidebar-collapsed-desktop:cursor-e-resize rtl:data-flux-sidebar-collapsed-desktop:cursor-w-resize max-lg:data-flux-sidebar-cloak:hidden data-flux-sidebar-on-mobile:data-flux-sidebar-collapsed-mobile:-translate-x-full data-flux-sidebar-on-mobile:data-flux-sidebar-collapsed-mobile:rtl:translate-x-full z-20! data-flux-sidebar-on-mobile:start-0! data-flux-sidebar-on-mobile:fixed! data-flux-sidebar-on-mobile:top-0! data-flux-sidebar-on-mobile:min-h-dvh! data-flux-sidebar-on-mobile:max-h-dvh! max-h-dvh overflow-y-auto overscroll-contain max-lg:bg-white dark:bg-zinc-900 lg:w-54 lg:mr-16 max-lg:p-8 lg:pl-0 max-lg:w-64 py-12 gap-7 pr-20 max-lg:border-r border-transparent dark:border-white/10 print:hidden text-sm" x-init="$el.classList.add(&#039;transition-transform&#039;)" x-persist="sidebar" wire:scroll="" collapsible="mobile" sticky x-data data-flux-sidebar-cloak data-flux-sidebar>
   ```

5. Contoh salah satu item menu adalah:
   ```html
   <a class="flex gap-2 items-center pl-4 py-[5px] first:pt-0 last:pb-0 border-l-2 border-zinc-100 dark:border-zinc-700" href="/components/badge" wire:navigate="" wire:current="font-medium text-zinc-800 dark:text-white border-zinc-800 dark:border-white!">Badge</a>
   ```

6. Konten utama dokumentasi biasanya berada di dalam elemen berikut:
   ```html
   <div class="[grid-area:main] p-6 lg:p-8 [[data-flux-container]_&amp;]:px-0  lg:py-12" listen-for-intersection-of-titles="listen-for-intersection-of-titles" data-flux-main>
   ```

7. Saat mengonversi HTML menjadi Markdown:

   * Periksa terlebih dahulu apakah terdapat tag gambar.
   * Jika terdapat tag seperti img, svg, picture, atau source, hapus terlebih dahulu sebelum proses konversi.
   * Tujuannya agar ukuran file Markdown akhir tidak terlalu besar.

8. Hasil akhir harus berupa:

   * Semua halaman dokumentasi tersimpan sebagai file HTML terpisah.
   * Seluruh HTML tersebut digabung menjadi satu file Markdown akhir.
   * Urutan file mengikuti prefix numerik seperti 0001, 0002, dan seterusnya.

Buatkan script lengkap dan detail sesuai spesifikasi di atas.

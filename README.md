
# Pengolahan Citra Muhammad Raehand Fathahillah

1. Teori Tentang Word Segmentation
    
Word segmentation adalah proses memisahkan teks tanpa spasi menjadi unit-unit kata yang terpisah. Pada bahasa-bahasa seperti Bahasa Inggris, kata-kata biasanya dipisahkan oleh spasi, sehingga pemisahan kata menjadi tugas yang relatif mudah. Namun, dalam beberapa bahasa seperti Bahasa Tionghoa, Bahasa Jepang, atau Bahasa Thai, teks tidak memiliki pemisah kata yang jelas.

Berikut ini beberapa teori dan metode yang digunakan dalam word segmentation:

A. Statistik dan Probabilitas: Metode berbasis statistik menggunakan analisis probabilitas untuk memprediksi batas kata. Dalam hal ini, diperhatikan frekuensi kemunculan kata dan kombinasi kata dalam sebuah teks. Metode seperti Maximum Likelihood dan Hidden Markov Model (HMM) sering digunakan untuk menghitung probabilitas kata dan mendapatkan urutan kata yang paling mungkin.

B. Berbasis Kamus: Metode ini menggunakan kamus yang memuat daftar kata-kata yang valid untuk sebuah bahasa. Kamus tersebut dapat berisi kata-kata baku, kata-kata yang sering digunakan, atau kata-kata yang diambil dari teks-teks yang ada. Metode ini mencocokkan teks dengan entri kamus untuk mengidentifikasi batas kata.

C. Berbasis Aturan: Pendekatan ini menggunakan aturan gramatikal dan morfologis untuk mengidentifikasi batas kata. Aturan-aturan tersebut mencakup pola pembentukan kata, pengenalan akar kata, dan afiksasi dalam bahasa tertentu. Misalnya, dalam Bahasa Inggris, awalan seperti "un-" atau sufiks seperti "-ing" dapat membantu mengidentifikasi kata-kata yang terpisah.

D. Pembelajaran Mesin: Dengan kemajuan dalam bidang pemrosesan bahasa alami dan pembelajaran mesin, metode berbasis pembelajaran mesin telah menjadi populer. Model seperti jaringan saraf berbasis rekurensi (RNN) atau transformer dapat dilatih untuk mempelajari pola dan konteks dalam teks yang tidak terpisahkan untuk memprediksi batas kata.

E. Pendekatan Hibrida: Pendekatan ini menggabungkan beberapa metode di atas untuk mencapai hasil yang lebih akurat. Misalnya, penggunaan kamus untuk mencocokkan kata-kata yang umum dan kemudian menggunakan model berbasis pembelajaran mesin untuk mengidentifikasi kata-kata yang tidak ada dalam kamus.

Penting untuk dicatat bahwa word segmentation tidak selalu memiliki solusi yang unik dan dapat bervariasi tergantung pada bahasa dan konteksnya. Metode yang efektif untuk satu bahasa mungkin tidak bekerja dengan baik untuk bahasa lain. Oleh karena itu, penelitian dan pengembangan terus dilakukan untuk meningkatkan keakuratan dan kinerja metode word segmentation.

2. Menjelaskan Tahap-Tahapan Cara Penyelesaiannyaa

Pertama saya Import library yang saya butuhkan untuk menjalankan tahapan-tahapan selanjutnya antara lain library nyaa adalah :
-opencv adalah library yang populer untuk penglihatan komputer dan pemrosesan citra. Library ini menyediakan berbagai fungsi dan algoritma untuk memanipulasi, menganalisis, dan memproses citra dan video. OpenCV dapat digunakan dengan bahasa pemrograman seperti Python, C++, dan Java.
-selanjutnya adalah Numpy (Numerical Python) adalah library Python yang populer untuk komputasi numerik. NumPy menyediakan struktur data yang efisien dan performa tinggi untuk memanipulasi dan mengolah array multidimensi.
-setelah itu saya juga menggunakan library matplotlib sebagai library Python yang populer untuk visualisasi data. 
-Dan yang terkahir adalah saya mengambil beberapa sub modul yaitu:
Submodul io dari library scikit-image (from skimage import io) menyediakan fungsi untuk membaca dan menulis gambar dalam berbagai format file.

Submodul color (from skimage import color) menyediakan fungsi-fungsi untuk mengubah ruang warna gambar.

Submodul measure (from skimage import measure) berfokus pada analisis dan pengukuran objek dalam gambar.

Selanjutnya kita masuk kepada Resize dan Read Image atau Gambar mengapa hal ini diperlukan karena Read image (membaca gambar) dan resize (mengubah ukuran) diperlukan sebelum word segmentation untuk mempersiapkan gambar yang akan diproses. Membaca gambar memungkinkan kita mendapatkan data piksel dari gambar yang akan dianalisis. Sedangkan resize digunakan untuk menyesuaikan ukuran gambar agar sesuai dengan kebutuhan word segmentation.

Pertama yang saya lakukan adalah melakukan codingan membaca gambar saya terlebih dahulu setelah itu saya ingin mengetahui height,width dan channels dari gambar saya gunakan agar tidaak salah dalam proses resize image nya nanti,setelah saya mengetahui ketiga tersebut maka saya lakukan ke step selanjutnya yaitu resize image dengan height lebih besar dari 1000 karena height pada gambar saya adalah 1600 dan width yang saya gunakan adalah = 900.

Selanjutnya saya melakukan Image Processing dengan menggunakan fungsi thresholding yang bertujuan untuk mengubah citra menjadi citra biner, di mana setiap piksel diubah menjadi nilai biner (hitam atau putih) berdasarkan ambang batas tertentu. dan Image Processinng ini digunakan yang bertujuan untuk melakukan preprocessing gambar, segmentasi teks, deteksi dan pemisahan kata, penghapusan noise, dan koreksi teks. Hal ini membantu meningkatkan kualitas gambar, memisahkan kata-kata, menghilangkan noise, dan memperbaiki teks sebelum dilakukan analisis lebih lanjut pada kata-kata yang terisolasi.

Setelah itu saya melakukan Line Segmentation yang bertujuan untuk memisahkan baris-baris teks dalam sebuah dokumen atau gambar teks. Ini membantu dalam mengurangi interferensi antara garis-garis teks, mempertahankan konteks visual yang jelas, dan menyesuaikan variasi ukuran dan orientasi dalam pemrosesan kata-kata, Pada Line Segmentation saya gunakan fungsi dilation yang berfungsi sebagai pengubah garis teks yang tipis atau kurang terhubung menjadi garis teks yang lebih tebal atau terhubung.

Fungsi dilation bekerja dengan menggeser elemen struktural (kernel) di sepanjang piksel dalam citra dan mengganti piksel target dengan nilai maksimum di sekitarnya. Dengan melakukan operasi ini, area garis teks diperluas sehingga dapat menghubungkan atau memperbesar gap antara garis-garis teks yang terpisah.

Penerapan dilation dalam line segmentation membantu dalam memperbaiki kesalahan pemisahan antara baris teks yang terpisah atau memperbaiki kegagalan dalam mendeteksi garis teks yang tipis atau putus, tak lupa juga saya melakukan image.copy untuk mengcopy hasil dari line segmentation yang sudah saya kerjakan.

Setelah semua komponen siap dan sudah saya megetahui apa saja yang saya perlukan untuk mengerjakan word segmentation maka tahap selanjutnya adalah word Segmentation dengan mengunnakan variable baru yaitu dillated 2
dan sedikit saya jelaskan tentang codingan yang saya buat yaitu;
image_copy_3 = image.copy(): Baris ini membuat salinan gambar asli (image) yang akan digunakan untuk visualisasi dan menggambar persegi panjang di sekitar kata-kata tersegmentasi.

words_list = []: Variabel words_list adalah daftar kosong yang akan digunakan untuk menyimpan koordinat persegi panjang yang mengelilingi setiap kata yang tersegmentasi.

for line in sorted_contours_lines:
x, y, w, h = cv2.boundingRect(line)
roi_line = dilated2[y: y+w, x:x+w]: Loop ini mengiterasi melalui kontur garis yang telah diurutkan (sorted_contours_lines). Untuk setiap kontur garis, cv2.boundingRect digunakan untuk mendapatkan koordinat persegi panjang yang membungkus garis tersebut. Kemudian, dilakukan pengambilan ROI (Region of Interest) dari gambar dilated2 menggunakan koordinat persegi panjang tersebut.

(cnt, heirarchy) = cv2.findContours(roi_line.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE): Fungsi cv2.findContours digunakan untuk mendeteksi kontur-kontur dalam ROI yang telah diambil sebelumnya (roi_line). Metode cv2.RETR_EXTERNAL digunakan untuk mengambil hanya kontur eksternal, sementara cv2.CHAIN_APPROX_NONE digunakan untuk menyimpan semua titik kontur tanpa menghilangkan apapun.

sorted_contour_words = sorted(cnt, key=lambda cntr : cv2.boundingRect(cntr)): Kontur-kontur yang telah dideteksi dalam ROI diurutkan berdasarkan koordinat persegi panjang mereka menggunakan fungsi sorted.

for word in sorted_contour_words:
x2, y2, w2, h2 = cv2.boundingRect(word)
words_list.append([x+x2, y+y2, x+x2+w2, y+y2+h2])
cv2.rectangle(image_copy_3, (x+x2, y+y2), (x+x2+w2, y+y2+h2), (255,255,100),2): Loop ini mengiterasi melalui kontur-kontur kata yang telah diurutkan (sorted_contour_words). Untuk setiap kontur kata, cv2.boundingRect digunakan untuk mendapatkan koordinat persegi panjang yang membungkus kata tersebut. Koordinat persegi panjang ini ditambahkan ke dalam words_list untuk menyimpan informasi tentang setiap kata yang tersegmentasi. Selain itu, cv2.rectangle digunakan untuk menggambar persegi panjang di sekitar setiap kata pada image_copy_3 dengan warna kuning.

plt.imshow(image_copy_3): Baris ini menampilkan gambar image_copy_3 yang telah diperbarui dengan persegi panjang yang mengelilingi kata-kata tersegmentasi.

Kode ini melakukan proses segmentasi kata dengan memperoleh kontur garis dan kata-kata dalam gambar, menentukan persegi panjang yang mengelilingi setiap kata,dan menyimpan koordinat-kordinat tersebut dalam words_list. Selain itu, persegi panjang juga digambar di sekitar setiap kata pada gambar image_copy_3 menggunakan cv2.rectangle.

Pada akhirnya, gambar image_copy_3 ditampilkan menggunakan plt.imshow, sehingga Anda dapat melihat visualisasi hasil word segmentation dengan persegi panjang yang mengelilingi setiap kata.

Kode ini merupakan implementasi dasar dari word segmentation menggunakan kontur dan persegi panjang sebagai metode untuk memisahkan kata-kata dalam gambar. Setelah kata-kata tersegmentasi, Anda dapat melanjutkan dengan melakukan pemrosesan teks lebih lanjut, seperti pengenalan karakter atau analisis teks.

3. Jurnal Yang Digunakan 
    https://journals.iium.edu.my/ejournal/index.php/iiumej/article/view/1408/759


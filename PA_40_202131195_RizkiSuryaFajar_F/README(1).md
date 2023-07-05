
# Contour

Contur (atau disebut juga "contour" dalam bahasa Inggris) mengacu pada garis yang mengelilingi area yang memiliki intensitas piksel yang serupa atau pola yang seragam. Kontur adalah representasi visual dari bentuk atau objek yang ada dalam gambar.

Ketika kita melakukan operasi segmentasi pada gambar, kontur sering digunakan untuk mengidentifikasi dan memisahkan objek dari latar belakang atau objek lain dalam gambar. Setiap kontur diidentifikasi sebagai urutan titik-titik piksel yang membentuk garis tertutup. Garis kontur ini mengikuti batas atau tepi dari objek dalam gambar.

Beberapa fungsi atau algoritma dalam pustaka pengolahan gambar, seperti OpenCV, dapat digunakan untuk menemukan kontur dalam gambar. Fungsi cv2.findContours() adalah salah satu contohnya. Fungsi ini mengidentifikasi kontur-kontur yang ada dalam gambar dengan menghitung batas-batas yang memisahkan area dengan intensitas piksel yang berbeda.

Setelah mengidentifikasi kontur, kita dapat menggunakannya untuk berbagai tujuan, seperti pengenalan objek, pengukuran ukuran atau bentuk objek, deteksi perubahan atau gerakan, dan banyak lagi. Kontur juga sering digunakan sebagai input untuk operasi lanjutan, seperti pengenalan wajah, pelacakan objek, atau segmentasi lebih lanjut.

Dalam implementasi kode Anda, Anda menggunakan fungsi cv2.findContours() untuk menemukan kontur dalam gambar setelah menerapkan operasi Canny Edge Detection. Kontur yang ditemukan kemudian digambar pada gambar salinan menggunakan fungsi cv2.drawContours().


#Tahapan

  1.  Mempersiapkan gambar: Mulailah dengan memuat gambar yang akan digunakan untuk membuat gambar kontur. Anda dapat menggunakan pustaka seperti OpenCV untuk membaca dan memuat gambar ke dalam struktur data yang sesuai.

  2.  Pra-pemrosesan (Opsional): Beberapa gambar mungkin memerlukan pra-pemrosesan sebelum dapat menemukan kontur dengan baik. Tahap pra-pemrosesan dapat mencakup penyesuaian kontras, pencahayaan, penghalusan gambar, atau operasi morfologi seperti erosi dan dilasi. Pra-pemrosesan dapat membantu meningkatkan kualitas kontur yang akan ditemukan.

  3.  Mengubah gambar menjadi citra biner: Untuk menemukan kontur, gambar perlu diubah menjadi citra biner. Ini bisa dilakukan dengan menggunakan teknik segmentasi, seperti thresholding, yang mengubah piksel gambar menjadi hitam atau putih berdasarkan ambang batas tertentu. Teknik lain seperti Canny Edge Detection juga dapat digunakan untuk menghasilkan tepi yang akurat sebagai dasar kontur.

 4.   Mencari kontur: Setelah gambar diubah menjadi citra biner, langkah berikutnya adalah menemukan kontur dalam citra tersebut. Dalam OpenCV, Anda dapat menggunakan fungsi cv2.findContours() untuk menemukan kontur dalam citra biner. Fungsi ini mengembalikan daftar kontur yang ditemukan.

5.  Menampilkan atau menggambar kontur: Setelah kontur ditemukan, Anda dapat memilih untuk menampilkan atau menggambar kontur pada gambar asli atau gambar lainnya. Dalam OpenCV, Anda dapat menggunakan fungsi cv2.drawContours() untuk menggambar kontur pada gambar dengan memberikan parameter gambar sasaran, daftar kontur, indeks kontur yang ingin digambar, warna, dan ketebalan garis.


#source code

    import cv2: Baris ini mengimpor pustaka OpenCV, yang merupakan pustaka populer untuk tugas pengolahan citra dan video. Pustaka ini menyediakan fungsi dan alat untuk pengolahan gambar dan video, deteksi dan pelacakan objek, dan lain-lain.

    import numpy as np: Baris ini mengimpor pustaka NumPy dan memberikan alias "np". NumPy adalah pustaka yang kuat untuk komputasi numerik di Python. Pustaka ini mendukung array multidimensi besar dan koleksi fungsi matematika untuk melakukan operasi pada array tersebut.

    import matplotlib.pyplot as plt: Baris ini mengimpor modul pyplot dari pustaka Matplotlib, yang merupakan pustaka untuk membuat visualisasi dan plot di Python. Pustaka ini menyediakan antarmuka mirip MATLAB untuk membuat visualisasi dan plot.

#memasukkan gambar asli

    image = cv2.imread('build.jpeg'): Baris ini membaca gambar dengan nama file 'build.jpeg' menggunakan fungsi cv2.imread(). Gambar tersebut disimpan dalam variabel image. Fungsi cv2.imread() digunakan untuk membaca gambar dari file ke dalam bentuk array yang dapat digunakan untuk pemrosesan lebih lanjut.

    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB): Baris ini mengubah skema warna gambar dari BGR (Blue-Green-Red) ke RGB (Red-Green-Blue). Fungsi cv2.cvtColor() digunakan untuk mengubah skema warna gambar.

    edged = cv2.Canny(image_rgb, 30, 200): Baris ini menggunakan metode Canny edge detection untuk menemukan tepi dalam gambar. Metode Canny edge detection menghasilkan gambar biner dengan menandai tepi yang terdeteksi. Parameter pertama adalah gambar sumber yang telah diubah ke skema warna RGB. Parameter kedua dan ketiga adalah batas bawah dan atas untuk proses deteksi tepi.

    contours, _ = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE): Baris ini mencari kontur atau garis tepi yang ada dalam gambar biner edged. Fungsi cv2.findContours() mengembalikan daftar kontur yang terdeteksi. Parameter pertama adalah gambar biner yang diubah menjadi salinan. Parameter kedua adalah metode retrieval (pengambilan) kontur, dan cv2.RETR_EXTERNAL digunakan untuk mendapatkan hanya kontur eksternal terluar. Parameter ketiga adalah metode aproksimasi kontur, dan cv2.CHAIN_APPROX_SIMPLE digunakan untuk mengaproksimasi kontur dengan menggunakan titik-titik ujung saja.

    image_copy = image.copy(): Baris ini membuat salinan gambar asli untuk digunakan dalam visualisasi hasil.


#memasukkan Contour


    image_copy = image.copy(): Baris ini membuat salinan gambar asli untuk digunakan dalam visualisasi hasil. Salinan gambar disimpan dalam variabel image_copy.

    cv2.drawContours(image_copy, contours, -1, (0, 0, 255), 3): Baris ini menggambar kontur pada salinan gambar image_copy. Fungsi cv2.drawContours() digunakan untuk menggambar kontur pada gambar. Parameter pertama adalah gambar sasaran, yaitu image_copy. Parameter kedua adalah daftar kontur yang ingin digambar, yaitu contours yang diperoleh sebelumnya. Parameter ketiga adalah indeks kontur yang ingin digambar. Dalam hal ini, nilai -1 digunakan untuk menggambar semua kontur. Parameter keempat adalah warna kontur yang ingin digambar, di sini (0, 0, 255) adalah warna merah (B, G, R). Parameter kelima adalah ketebalan garis kontur dalam piksel, di sini 3 digunakan.

    
#memasukkan blank

    binary = np.zeros_like(image_rgb): Baris ini membuat array nol dengan ukuran yang sama seperti gambar image_rgb. Array ini akan digunakan sebagai gambar biner kosong.

    cv2.drawContours(binary, contours, -1, (255, 255, 255), thickness=cv2.FILLED): Baris ini menggambar kontur pada gambar biner binary dengan mengisi area di dalam kontur. Fungsi cv2.drawContours() digunakan untuk menggambar kontur pada gambar. Parameter pertama adalah gambar sasaran, yaitu binary. Parameter kedua adalah daftar kontur yang ingin digambar, yaitu contours yang diperoleh sebelumnya. Parameter ketiga adalah indeks kontur yang ingin digambar. Dalam hal ini, nilai -1 digunakan untuk menggambar semua kontur. Parameter keempat adalah warna yang ingin digunakan untuk mengisi area kontur, di sini (255, 255, 255) adalah warna putih (B, G, R). Parameter thickness digunakan untuk menentukan ketebalan garis kontur atau metode pengisian area kontur. Di sini, cv2.FILLED digunakan untuk mengisi seluruh area kontur.


#output

    fig, axes = plt.subplots(1, 3, figsize=(10, 10)): Baris ini membuat sebuah objek gambar (fig) dan sejumlah sumbu (axes). Sumbu-sumbu ini akan digunakan untuk menampilkan gambar-gambar.
        Parameter pertama 1 menentukan bahwa kita ingin satu baris sumbu.
        Parameter kedua 3 menentukan bahwa kita ingin tiga sumbu dalam satu baris.
        Parameter figsize=(10, 10) menentukan ukuran gambar yang ingin ditampilkan, yaitu 10x10 inci.

    ax = axes.ravel(): Baris ini mengubah array sumbu yang dihasilkan sebelumnya menjadi array satu dimensi. Ini memudahkan untuk mengakses setiap sumbu secara individu.

    ax[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)): Baris ini menampilkan gambar asli di sumbu pertama (ax[0]). Fungsi imshow() digunakan untuk menampilkan gambar, dan cv2.cvtColor() digunakan untuk mengubah skema warna dari BGR ke RGB agar sesuai dengan tampilan yang diharapkan oleh Matplotlib.

    ax[0].set_title("Original Image"): Baris ini menambahkan judul "Original Image" pada sumbu pertama (ax[0]).

    ax[1].imshow(cv2.cvtColor(image_copy, cv2.COLOR_BGR2RGB)): Baris ini menampilkan gambar dengan kontur yang telah digambar di sumbu kedua (ax[1]). Gambar yang ditampilkan adalah image_copy, yang merupakan salinan gambar asli dengan kontur yang digambar sebelumnya.

    ax[1].set_title("Drawn Contours"): Baris ini menambahkan judul "Drawn Contours" pada sumbu kedua (ax[1]).

    ax[2].imshow(binary, cmap='binary'): Baris ini menampilkan gambar biner kosong dengan kontur yang diisi di sumbu ketiga (ax[2]). Gambar yang ditampilkan adalah binary, yang merupakan gambar biner dengan kontur yang diisi dengan warna putih.

    ax[2].set_title("Blank Image"): Baris ini menambahkan judul "Blank Image" pada sumbu ketiga (ax[2]).

    plt.tight_layout(): Baris ini mengatur tata letak agar tampilan gambar terlihat lebih rapi dengan jarak yang tepat antara sumbu-sumbu.

    plt.show(): Baris ini menampilkan gambar-gambar yang sudah diatur sebelumnya menggunakan Matplotlib.

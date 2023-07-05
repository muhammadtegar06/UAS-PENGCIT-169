
# Project Title

# Membaca gambar dari file 'jalan2.jpg' menggunakan OpenCV
image = cv2.imread('IMAGES/jalan2.jpg')

# Mengubah skema warna gambar dari BGR ke RGB
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Mencetak dimensi gambar
print(image.shape)

# Mengambil tinggi dan lebar gambar
height = image.shape[0]
width = image.shape[1]

# Definisi titik-titik daerah minat (region of interest)
region_of_interest_vertices = [
    (0, height),
    (width/2, height/2),
    (width, height)
]

# Mengubah gambar menjadi skala abu-abu
gray_image = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)

# Menerapkan deteksi tepi pada gambar
canny_image = cv2.Canny(gray_image, 100, 200)

# Memotong gambar menggunakan daerah minat
cropped_image = region_of_interest(canny_image, np.array([region_of_interest_vertices], np.int32))

# Melakukan transformasi Hough pada gambar yang dipotong
lines = cv2.HoughLinesP(cropped_image,
                        rho=6,
                        theta=np.pi/180,
                        threshold=160,
                        lines=np.array([]),
                        minLineLength=40,
                        maxLineGap=25)

# Menggambar garis-garis pada gambar asli
image_with_lines = drow_the_lines(image, lines)

# Menampilkan gambar dengan garis-garis
plt.imshow(image_with_lines)
plt.show()


## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)


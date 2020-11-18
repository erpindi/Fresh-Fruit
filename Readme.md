## Fresh_Fruit
Aplikasi ini adalah aplikasi penjualan buah dengan bucket dengan menggunakan konsep MVC yang ditekankan agar mahasiswa paham konsep MVC

## Scope and Functionalities
1. User dapat menekan tombol Add
2. User dapat menampilkan gambar buah
3. User akan melihat warning 

## How Does it Works?
1. Apa fungsi BucketEventListener?

Fungsi dari BucketEventListener ialah tempat untuk menghandle event ketika action dijalankan berhasil (onSucceed) dan gagal (onFailed) 

2. Logika Pembahasan

Diawali pada MainWindow.xaml.cs, dengan membuat sebuah instance dari masing - masing class.

``` javascript
 public MainWindow()
        {
            InitializeComponent();

            Bucket keranjangBuah = new Bucket(2);
            BucketController bucketcontroller = new BucketController(keranjangBuah, this);

            toni = new Seller("Toni", bucketcontroller);

            listBoxBucket.ItemsSource = keranjangBuah.findAll();
        }
```

selanjutnya masuk pada BucketEventListener agar dapat menghandle event yang dibuat

``` csharp
interface BucketEventListener
    {
        void onSucced(string message);
        void onFailed(string message);
    }
```

Setelah itu masuk pada Bucket.cs yang berfungsi untuk menampung data yang di add

``` javascript
 public Bucket(int capacity)
        {
            this.capacity = capacity;
            this.fruits = new List<Fruit>();
        }

        public void insert(Fruit fruit)
        {
            this.fruits.Add(fruit);
        }

        public void remove(int position)
        {
            this.fruits.RemoveAt(position);
        }

        public List<Fruit> findAll()
        {
            return this.fruits;
        }

        public int getCapacity()
        {
            return this.capacity;
        }

        public int countItems()
        {
            return this.fruits.Count();
        }
```

selanjutnya masuk pada Fruit.cs yang berfungsi untuk memasukkan nama buah

``` csharp
 {
        public string name { get; set; }

        public Fruit(string name)
        {
            this.name = name;
        }
        public string getName()
        {
            return this.name;
        }

    }
```

Dan terakhir ialah BucketController.cs untuk memberikan informasi jika barang yang di tambahkan itu sudah penuh atau tidak
``` javascript
 public void addFruit(Fruit fruit)
        {
            if (bucketIsOverload())
            {
                eventListener.onFailed("Ops, keranjang Penuh");
            }
            else
            {
                this.bucket.insert(fruit);
                eventListener.onSucced("Yey, berhasil ditambahkan");
            }
        }
```

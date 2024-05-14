# Tugas_3_Struktur_Data
import heapq

class Peta:
    # Metode init (inisiasi)
    def __init__(self):
        self.daftarKota = {}
    
    # Metode tambahKota untuk menambah kota
    def tambahKota(self, kota):
        if kota not in self.daftarKota:
            self.daftarKota[kota] = {}
    
    # Metode printKota untuk menampilkan kota
    def printKota(self):
        for kota in self.daftarKota:
            print(f"{kota} -- {self.daftarKota[kota]}")
    
    # Metode tambahJalan untuk menambah jarak
    def tambahJalan(self, kota1, kota2, jarak):
        if kota1 in self.daftarKota and kota2 in self.daftarKota:
            self.daftarKota[kota1][kota2] = jarak
            self.daftarKota[kota2][kota1] = jarak
    
    # Metode hapusKota untuk menghapus kota yang di dalam daftar kota
    def hapusKota(self, kotaDihapus):
        if kotaDihapus in self.daftarKota:
            for kota in self.daftarKota:
                if kotaDihapus in self.daftarKota[kota]:
                    del self.daftarKota[kota][kotaDihapus]
            del self.daftarKota[kotaDihapus]
    
    # Metode hapusJalan untuk menghapus jarak yang ada di dalam daftar kota
    def hapusJalan(self, kota1, kota2):
        if kota1 in self.daftarKota and kota2 in self.daftarKota:
            del self.daftarKota[kota1][kota2]
            del self.daftarKota[kota2][kota1]

    # Metode Dijkstra untuk menemukan jarak terpendek
    def dijkstra(self, source):
        distances = {city: float('inf') for city in self.daftarKota}
        distances[source] = 0
        priority_queue = [(0, source)]
          
        while priority_queue:
            current_distance, current_city = heapq.heappop(priority_queue)
            
            if current_distance > distances[current_city]:
                continue
            
            for neighbor, weight in self.daftarKota[current_city].items():
                distance = current_distance + weight
                if distance < distances[neighbor]:
                    distances[neighbor] = distance
                    heapq.heappush(priority_queue, (distance, neighbor))
        
        return distances
    
    # Metode ruteTempuh untuk menampilkan jarak tempuh dari kota1 ke kota2
    def ruteTempuh(self, kota1, kota2):
        if kota1 not in self.daftarKota or kota2 not in self.daftarKota:
            print("Kamu harus memasukkan sesuai daftar kota")
            return

        distances = self.dijkstra(kota1)
        if distances[kota2] == float('inf'):
            print(f"Tidak ada rute dari {kota1} ke {kota2}")
        else:
            print(f"Jarak terpendek dari {kota1} ke {kota2} adalah {distances[kota2]} km")


# Variabel untuk daftar nama kota di peta Jawa Timur
KotaJawaTimur = ["Surabaya", "Sidoarjo", "Malang", "Blitar", "Tulungagung", "Trenggalek", "Ponorogo", "Madiun", "Ngawi", "Bojonegoro"]

# Variabel untuk memanggil kelas Peta
JawaTimur = Peta()

# Memasukkan nama kota ke dalam kelas
for kota in KotaJawaTimur:
    JawaTimur.tambahKota(kota)

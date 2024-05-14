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

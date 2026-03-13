# Flappy Tetris — Oyun Mantığı (Türkçe Özet)

- Ekran sabit, dünya yatay kayan dairesel bir ızgara (`world[wc][row]`).
- Tetris parçası ekranın belirli bir sütununda (`PIECE_COL`) sabit durur; Flappy Bird fiziğiyle (yerçekimi + zıplama) yukarı/aşağı hareket eder.
- `SPACE` tuşu parçayı yukarı fırlatır ve saat yönünde döndürür.
- Dünya her kare sola kayar; parça, dünya sütunlarına çarpışma kontrolüyle etkileşime girer.
- Parça yere değince `lockPiece()` bloğu dünya ızgarasına yazar.
- Oyun biter: parça üst 2 satıra çıkarsa veya kayan dünya parçanın konumuna çarparsa.

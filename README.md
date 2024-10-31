# ikl
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Iklan Minuman Penyegar dengan Elemen Lemon dan Kelapa</title>
  <style>
    /* Gaya Umum */
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #e0f7fa;
      font-family: Arial, sans-serif;
    }

    /* Banner Iklan Minuman */
    .iklan-minuman {
      position: relative;
      width: 90%;
      max-width: 600px;
      background: linear-gradient(135deg, #00bfa5, #00e5ff);
      color: #ffffff;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      text-align: center;
      overflow: hidden;
      animation: popUp 1s ease-out;
    }

    /* Gaya Lemon dan Kelapa */
    .lemon, .kelapa-muda {
      position: absolute;
      width: 60px;
      height: auto;
      opacity: 0.8;
      z-index: 1;
    }

    .lemon {
      top: -20px;
      right: -20px;
      transform: rotate(-25deg);
    }

    .kelapa-muda {
      bottom: -20px;
      left: -20px;
      transform: rotate(15deg);
    }

    /* Teks Iklan */
    .iklan-minuman h1 {
      font-size: 2em;
      margin: 10px 0;
      z-index: 2;
    }

    .iklan-minuman p {
      font-size: 1.1em;
      margin: 0 0 20px;
      z-index: 2;
    }

    /* Harga Minuman */
    .harga-container {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-top: 10px;
      z-index: 2;
    }

    .harga {
      background-color: #ffeb3b;
      color: #333333;
      padding: 10px 15px;
      font-weight: bold;
      border-radius: 8px;
      font-size: 1.2em;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
    }

    /* Tombol CTA */
    .cta-button {
      display: inline-block;
      margin-top: 20px;
      padding: 12px 30px;
      background-color: #ffeb3b;
      color: #333333;
      font-weight: bold;
      font-size: 1em;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      text-decoration: none;
    }

    .cta-button:hover {
      background-color: #fff176;
    }

    /* Modal untuk Metode Pembayaran */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      justify-content: center;
      align-items: center;
    }

    .modal-content {
      background-color: #ffffff;
      padding: 20px;
      border-radius: 10px;
      text-align: center;
      max-width: 300px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
    }

    .modal-content img {
      width: 150px;
      height: 150px;
      margin-bottom: 15px;
    }

    .modal-content button {
      padding: 8px 20px;
      background-color: #ff5733;
      color: #ffffff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
      margin-top: 10px;
    }

    /* Pesan Terima Kasih */
    .thank-you-message {
      display: none;
      text-align: center;
      background-color: #00bfa5;
      color: #ffffff;
      padding: 15px;
      border-radius: 10px;
      margin-top: 20px;
      font-size: 1.2em;
    }
  </style>
</head>
<body>

  <!-- Banner Iklan Minuman -->
  <div class="iklan-minuman">
    <!-- Elemen Lemon dan Kelapa -->
    <img src="lemon.png" alt="Lemon" class="lemon">
    <img src="kelapa-muda.png" alt="Kelapa Muda" class="kelapa-muda">

    <img src="botol-minuman.png" alt="Minuman Penyegar" class="botol-gambar">
    <h1>Segarkan Harimu!</h1>
    <p>Nikmati kesegaran ekstra dari <strong>Minuman FreshXY</strong> dengan rasa lemon dan kelapa muda yang menyegarkan di setiap tegukan!</p>

    <div class="harga-container">
      <div class="harga">Ukuran Kecil: Rp 5.000</div>
      <div class="harga">Ukuran Besar: Rp 7.000</div>
    </div>

    <button class="cta-button" onclick="showModal()">Pesan Sekarang</button>

    <!-- Pesan Terima Kasih -->
    <div class="thank-you-message" id="thankYouMessage">
      Terima kasih, tunggu pesanan Anda!
    </div>
  </div>

  <!-- Modal untuk Metode Pembayaran -->
  <div class="modal" id="paymentModal">
    <div class="modal-content">
      <h2>Metode Pembayaran</h2>
      <p>Pilih metode pembayaran:</p>
      <!-- Metode QR Code -->
      <button onclick="confirmPayment('QR')">QR Code</button>
      <br>
      <img src="qrcode.png" alt="QR Code Pembayaran" id="qrCode" style="display: none; margin-top: 10px;">
      <br>
      <!-- Metode COD -->
      <button onclick="confirmPayment('COD')">Bayar di Tempat (COD)</button>
      <button onclick="closeModal()">Tutup</button>
    </div>
  </div>

  <!-- Script JavaScript -->
  <script>
    // Fungsi untuk menampilkan modal
    function showModal() {
      document.getElementById('paymentModal').style.display = 'flex';
    }

    // Fungsi untuk menutup modal
    function closeModal() {
      document.getElementById('paymentModal').style.display = 'none';
      document.getElementById('qrCode').style.display = 'none';
    }

    // Fungsi untuk mengonfirmasi pembayaran dan menampilkan pesan terima kasih
    function confirmPayment(method) {
      if (method === 'QR') {
        document.getElementById('qrCode').style.display = 'block';
      } else {
        document.getElementById('thankYouMessage').style.display = 'block';
        closeModal();
      }

      // Menampilkan pesan terima kasih setelah beberapa detik jika metode QR
      setTimeout(() => {
        document.getElementById('thankYouMessage').style.display = 'block';
        closeModal();
      }, 2000);
    }
  </script>

</body>
</html>

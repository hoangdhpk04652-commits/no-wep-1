<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Minimalist Form</title>
  
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Mulish:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    /* ==========================================
       1. RESET & CẤU HÌNH HỆ THỐNG ĐƠN VỊ (CSS)
       ========================================== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html {
      font-size: 62.5%; /* Định nghĩa lại: 1rem = 10px */
    }

    body {
      font-family: "Mulish", sans-serif;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #f4f5f7; /* Màu nền bổ sung giúp nổi bật thẻ main */
    }

    /* ==========================================
       2. BỐ CỤC CHÍNH CỦA BIỂU MẪU
       ========================================== */
    main {
      width: 40rem;
      height: 45rem;
      margin: 0 auto;
      padding: 2rem;
      background: #ffffff;
      border-radius: 2rem;
      box-shadow: 2px 3px 5px rgba(0, 0, 0, 0.2);
    }

    h1 {
      text-align: center;
      font-size: 3rem;
      padding: 1rem 2rem;
      color: #222222;
    }

    form {
      margin: 3rem 0;
      display: flex;
      flex-direction: column;
      row-gap: 2rem;
    }

    /* ==========================================
       3. CẤU TRÚC ĐẦU VÀO (INPUT & TEXTAREA)
       ========================================== */
    .input__container {
      display: flex;
      flex-direction: column;
      row-gap: 0.5rem;
    }

    .input__container label { 
      font-size: 1.6rem; 
      font-weight: 600;
      color: #333333;
    }

    .input__container input,
    textarea {
      padding: 1rem 2rem;
      border-radius: 5px;
      border: 1px solid #555555;
      font-size: 1.4rem;
      font-family: inherit;
      outline: none;
      resize: none;
      transition: border-color 0.2s, box-shadow 0.2s;
    }

    /* Hiệu ứng focus khi người dùng click vào ô nhập liệu */
    .input__container input:focus,
    textarea:focus {
      border-color: #000000;
      box-shadow: 0 0 0 3px rgba(0, 0, 0, 0.05);
    }

    /* ==========================================
       4. NÚT BẤM (BUTTON)
       ========================================== */
    button {
      align-self: flex-start;
      padding: 1rem 2rem;
      border-radius: 5px;
      border: none;
      background: #333333;
      color: #ffffff;
      font-size: 1.4rem;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.2s;
    }

    /* Hiệu ứng rê chuột lên nút bấm */
    button:hover {
      background: #111111;
    }
  </style>
</head>
<body>

  <main>
    <h1>Welcome to my Form</h1>
    <form id="form">
      
      <div class="input__container">
        <label for="name">Name</label>
        <input type="text" id="name" name="name" required />
      </div>
      
      <div class="input__container">
        <label for="email">Email</label>
        <input type="email" id="email" name="email" required />
      </div>
      
      <div class="input__container">
        <label for="message">Message</label>
        <textarea id="message" name="message" rows="4" required></textarea>
      </div>
      
      <button type="submit">Submit</button>
    </form>
  </main>

  <script>
    "use strict";

    // Chọn biểu mẫu form từ DOM
    const form = document.getElementById("form");

    // Lắng nghe sự kiện submit của form
    form.addEventListener("submit", function (event) {
        // Ngăn chặn hành vi tải lại trang mặc định của trình duyệt
        event.preventDefault(); 

        // Lấy giá trị dữ liệu và dùng .trim() để loại bỏ khoảng trắng thừa ở 2 đầu
        const name = document.getElementById("name").value.trim();
        const email = document.getElementById("email").value.trim();
        const message = document.getElementById("message").value.trim();

        // Biểu thức chính quy (Regex) để kiểm tra định dạng email của bạn
        const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

        // Kiểm tra tính hợp lệ của Email
        if (!emailPattern.test(email)) {
            alert("Wrong email format");
            return; // Dừng hàm lại, không xử lý các lệnh bên dưới
        }

        // Nếu tất cả dữ liệu hợp lệ, xử lý thành công (Mô phỏng xuất log dữ liệu)
        console.log("Dữ liệu gửi lên hệ thống:", { name, email, message });
        
        // Hiển thị thông báo thành công cho người dùng
        alert("Form submitted successfully");

        // Làm sạch toàn bộ các ô nhập liệu trong form sau khi hoàn tất
        this.reset(); 
    });
  </script>

</body>
</html>

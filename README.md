<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>Noise Media</title>
    <link rel="stylesheet" type="text/css" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    
    <style>
        /* ==========================================
           1. CẤU HÌNH CHUNG & PHÔNG CHỮ
           ========================================== */
        @import url('https://fonts.googleapis.com/css?family=PT+Sans');
        @import url('https://fonts.googleapis.com/css?family=PT+Serif');

        html, body {
            margin: 0;
            padding: 0;
            font-family: 'PT Serif', 'Helvetica', 'Arial';
        }

        h1, h2, h4, h5, h6 {
            font-family: 'PT Sans', 'Helvetica', 'Arial';
        }

        .normal-wrapper {
            width: 900px;
            margin: 0 auto;
            padding: 15px 40px;
            overflow: auto;
        }

        .hidden {
            display: none;
        }

        /* ==========================================
           2. THANH TRÊN CÙNG & ĐƯỜNG TRANG TRÍ
           ========================================== */
        #top-bar {
            width: 100%;
            background: #F1F1F1;
            border-bottom: 1px solid #D4D4D4;
            height: 25px;
        }

        #top-color-splash {
            width: 100%;
            height: 4px;
            background: #EB6361;
        }

        /* ==========================================
           3. LOGO & THANH ĐIỀU HƯỚNG (NAVBAR)
           ========================================== */
        .logo-icon {
            color: #000000;
            font-size: 60pt;
            float: left;
        }

        h1 {
            float: left;
            margin: 21px 0 0 25px;
        }

        #navbar {
            list-style-type: none;
            margin: 29px 0 0 0;
            padding: 0; 
            float: right;
            font-size: 16pt;
        }

        #navbar li {
            display: inline;
        }

        #navbar li a:link, #navbar li a:visited, #navbar li a:active {
            text-decoration: none;
            color: #000000;
            padding: 0 16px 0 10px;
            margin: 0;
            border-right: 2px solid #B4B4B4;
        }

        #navbar li a:link.last-link {
            border-right: 0px;
        }

        #navbar li a:hover {
            color: #EB6361;
        }

        /* ==========================================
           4. PHẦN GIỚI THIỆU (HERO SECTION)
           ========================================== */
        .one-third {
            width: 40%;
            float: left;
            box-sizing: border-box;
            margin-top: 20px;
        }

        .two-third {
            width: 60%;
            float: left;
            box-sizing: border-box;
            padding-left: 40px;
            text-align: right;
            margin-top: 20px;
        }

        .featured-image {
            max-width: 500px;
            width: 100%;
            height: auto;
        }

        .no-margin-top {
            margin-top: 0;
        }

        /* ==========================================
           5. KHU VỰC TRÍCH DẪN (QUOTE)
           ========================================== */
        #quote-area {
            background: #363636;
            color: #FFFFFF;
            text-align: center;
            padding: 15px 0;
            clear: both;
        }

        h3 {
            font-weight: normal;
            font-size: 20pt;
            margin-top: 0px;
        }

        h4 {
            font-weight: normal;
            font-size: 16pt;
            margin-bottom: 0;
        }

        /* ==========================================
           6. KHU VỰC CÁC TÍNH NĂNG (FEATURES/ICONS)
           ========================================== */
        .icon-outer {
            box-sizing: border-box;
            float: left;
            width: 33.33%;
            padding: 25px;
            margin: 0;
            text-align: center;
        }

        .icon-circle {
            background: #EEEEEE;
            color: #B4B4B4;
            width: 200px;
            height: 200px;
            border-radius: 200px;
            margin: 0 auto;
            border: 2px solid #D6D6D6;
            box-sizing: border-box;
            font-size: 75pt;
            padding: 30px 0 0 0;
            cursor: pointer;
        }

        .icon-circle:hover {
            color: #FFFFFF;
            background: #EB6361;
        }

        .icon-circle .logo-icon {
            float: none;
            font-size: inherit;
            color: inherit;
        }

        h5 {
            margin: 15px 0 10px 0;
            font-size: 20pt;
        }

        /* ==========================================
           7. CHÂN TRANG (FOOTER)
           ========================================== */
        #footer {
            width: 100%;
            background: #F1F1F1;
            border-top: 1px solid #D4D4D4;
            height: 150px;
            clear: both;
        }
    </style>
</head>
<body>

    <div id="top-bar"></div>

    <div class="normal-wrapper">
        <div id="logo-container">
            <i class="fa fa-volume-down logo-icon"></i> 
            <h1>Noise Media</h1>
        </div>
        <ul id="navbar">
            <li><a href="">Home</a></li>
            <li><a href="">About</a></li>
            <li><a href="">Reviews</a></li>
            <li><a href="" class="last-link">Contact</a></li>
        </ul>
    </div>

    <div id="top-color-splash"></div>

    <div class="normal-wrapper">
        <div class="one-third">
            <h2 class="no-margin-top">Welcome!</h2>
            <p>Noise Media is a technology company specialising in tech reviews.</p>
            <p>We’re very good at what we do, but unfortunately, we are not a real company.</p>
            <p>Make sure you visit makeuseof.com for the full tutorial on how to build this website.</p>
            <p>Alternatively, check out our review of the Panasonic G80 shown on the right!</p>
        </div>
        <div class="two-third">
            <img id="f-image-1" class="featured-image" src="https://images.unsplash.com/photo-1516035069371-29a1b244cc32?w=500" alt="Image 1" />
            <img id="f-image-2" class="featured-image hidden" src="https://images.unsplash.com/photo-1542751371-adc38448a05e?w=500" alt="Image 2" />
            <img id="f-image-3" class="featured-image hidden" src="https://images.unsplash.com/photo-1550745165-9bc0b252726f?w=500" alt="Image 3" />
        </div>
    </div>

    <div id="quote-area">
        <div class="normal-wrapper">
            <h3>“makeuseof is the best website ever”</h3>
            <h4>Joe Coburn</h4>
        </div>
    </div>

    <div class="normal-wrapper">
        <div class="icon-outer">
            <div class="icon-circle">
                <i class="fa fa-youtube"></i>
            </div>
            <h5>YouTube</h5>
            <p>Checkout our YouTube channel for more tech reviews, tutorials and giveaways!</p>
        </div>
        <div class="icon-outer">
            <div class="icon-circle">
                <i class="fa fa-camera-retro"></i>
            </div>
            <h5>Reviews</h5>
            <p>If you’re planning to buy a new gadget, check here first. We’ll give you in-depth reviews of the latest devices.</p>
        </div>
        <div class="icon-outer">
            <div class="icon-circle">
                <i class="fa fa-dollar"></i>
            </div>
            <h5>Buying Guides</h5>
            <p>At Buying Guides we strive to provide readers with the tools to get the best stuff for the lowest amount of money.</p>
        </div>
    </div>

    <div id="footer"></div>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js" type="text/javascript"></script>
    <script type="text/javascript">
        $(document).ready(function() {
            var time = 2500; // Thời gian chuyển ảnh (2.5 giây)
            
            // Lấy các thẻ ảnh bằng JQuery
            var $im1 = $('#f-image-1');
            var $im2 = $('#f-image-2');
            var $im3 = $('#f-image-3');

            setInterval(function(){
                changeImage(); 
            }, time);

            var currentImage = 1;
            function changeImage(){
                switch(currentImage) {
                    case 1:
                        $im1.hide();
                        $im2.show();
                        $im3.hide();
                        currentImage = 2;
                        break;
                    case 2:
                        $im1.hide();
                        $im2.hide();
                        $im3.show();
                        currentImage = 3;
                        break;
                    default:
                        $im1.show();
                        $im2.hide();
                        $im3.hide();
                        currentImage = 1;
                }
            }
        });
    </script>
</body>
</html>


<main>
     <h1>Welcome to my Form</h1>
     <form id="form">
       <div class="input__container">
         <label for="name">Name</label>
           <!-- The 'required' prop ensures a filled field before submission -->
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
       <button>Submit</button>
     </form>
</main>

* {
 margin: 0;
 padding: 0;
 box-sizing: border-box;
}

html {
 font-size: 62.5%;
}

body {
 font-family: "Mulish", sans-serif;
 height: 100vh;
 display: flex;
 justify-content: center;
 align-items: center;
}

main {
 width: 40rem;
 box-shadow: 2px 3px 5px rgba(0, 0, 0, 0.2);
 margin: 0 auto;
 height: 45rem;
 border-radius: 2rem;
 padding: 2rem;
}

h1 {
 text-align: center;
 font-size: 3rem;
 padding: 1rem 2rem;
}

form {
 margin: 3rem 0;
 display: flex;
 flex-direction: column;
 row-gap: 2rem;
}

.input__container {
 display: flex;
 flex-direction: column;
 row-gap: 0.5rem;
}

.input__container label { font-size: 1.6rem; }

.input__container input,
textarea {
 padding: 1rem 2rem;
 border-radius: 5px;
 border: 1px solid #555;
 resize: none;
}

button {
 align-self: flex-start;
 padding: 1rem 2rem;
 border-radius: 5px;
 border: none;
 background: #333;
 color: #fff;
 cursor: pointer;
}

<script>
 "use strict";
    const form = document.getElementById("form");
</script>

form.addEventListener("submit", function (event) { });
form.addEventListener("submit", function (event) {
    // Prevent page reload on submit
    event.preventDefault(); 
    // Selecting the email value filled by the user
    const email = document.getElementById("email").value;
});

form.addEventListener("submit", function (event) {
    // Preventing page reload on submit
    event.preventDefault(); 

  // Selecting the email value filled by the user
    const email = document.getElementById("email").value;

  // Checking for valid email using a simple regex pattern
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

 if (!emailPattern.test(email)) {
      alert("Wrong email format");
      return;
    }

  // If everything passes, show success message
    alert("Form submitted successfully");
});


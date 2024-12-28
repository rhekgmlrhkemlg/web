<!DOCTYPE html>
<html lang="ko">
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>작품 갤러리</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script&family=Noto+Sans+KR:wght@400;700&family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            background: linear-gradient(135deg, #ffffff, #88aaff);
            display: flex;
            flex-direction: column;
            margin: 0;
            font-family: 'Roboto', Arial, sans-serif;
            scroll-behavior: smooth; /* CSS로 기본 부드러운 스크롤 적용 */
        }

        /* 메뉴바 스타일 */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            display: flex;
            justify-content: space-around;
            align-items: center;
            padding: 10px 0;
            z-index: 200;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
        }

        nav a {
            color: white;
            text-decoration: none;
            font-size: 18px;
            font-weight: bold;
            font-family: 'Dancing Script', cursive;
            padding: 5px 10px;
            transition: background-color 0.3s ease;
        }

        nav a:hover {
            background-color: rgba(255, 255, 255, 0.3);
            border-radius: 5px;
        }

        header {
            width: 100%;
            padding: 50px 20px 20px;
            text-align: center;
            background-color: rgba(255, 255, 255, 0.8);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-top: 60px; /* 메뉴바 공간 확보 */
        }

        header h1 {
            font-size: 32px;
            margin: 0;
            color: #444;
        }

        main {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-top: 50px; /* 메뉴바와 헤더 공간 확보 */
        }

        .circle-button {
            width: 200px;
            height: 200px;
            background-color: #cceeff;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 20px;
            cursor: pointer;
            box-shadow: 0 8px 12px rgba(0, 0, 0, 0.2);
            margin: 20px;
            text-align: center;
            font-family: 'Dancing Script', cursive;
            transition: all 0.4s ease;
        }

        .circle-button:hover {
            transform: translateY(-10px) scale(1.1);
            background-color: #aaddff;
            box-shadow: 0 12px 16px rgba(0, 0, 0, 0.3);
        }

        .gallery {
            display: none;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 100%;
            margin-top: 30px;
        }

        .gallery-items {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
        }

        .overlay {
            position: relative;
            width: 200px;
            height: 250px;
            overflow: hidden;
            cursor: pointer;
            text-align: center;
            border-radius: 15px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        .overlay img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 15px;
            transition: transform 0.2s ease-in-out;
        }

        .overlay:hover img {
            transform: scale(1.1);
        }

        .description {
            text-align: center;
            margin-top: 5px;
            font-size: 14px;
            color: #555;
        }

        .back-button {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #ff6666;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .back-button:hover {
            background-color: #ff4444;
        }

        footer {
            text-align: center;
            padding: 10px 0;
            background-color: rgba(255, 255, 255, 0.9);
            box-shadow: 0 -4px 6px rgba(0, 0, 0, 0.1);
            font-family: 'Noto Sans KR', sans-serif;
        }

        footer p {
            margin: 0;
            color: #666;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <nav>
        <a href="#home">Home</a>
        <a href="#gallery1">Gallery 1</a>
        <a href="#gallery2">Gallery 2</a>
    </nav>
    <header id="home">
        <h1>작품 갤러리</h1>
    </header>
    <main>
        <div class="circle-button" onclick="showGallery('gallery1')">works by GO</div>
        <div class="circle-button" onclick="showGallery('gallery2')">FAVORITE WORKS</div>

        <div class="gallery" id="gallery1">
            <button class="back-button" onclick="goBack()">뒤로가기</button>
            <div class="gallery-items"></div>
        </div>

        <div class="gallery" id="gallery2">
            <button class="back-button" onclick="goBack()">뒤로가기</button>
            <div class="gallery-items"></div>
        </div>
    </main>
    <footer>
        <p>© 2024 고다희 예술 작품.</p>
    </footer>

    <script>
      

        const galleryData = {
            gallery1: [
                { title: 'Its beginning to look a lot like christmas', description: '겨울의 냄새가 나는 영상입니다.', img: 'art1.jpg' },
                { title: 'KDH', description: '이니셜로 만든 영상입니다.', img: 'art2.jpg' },
            ],
            gallery2: [
                { title: '조개 나무', description: '바다의 나무를 표현한 작품입니다.', img: 'art1.jpg' },
                { title: '고래칠', description: '고래를 직접 색칠할 수 있는 도안입니다.', img: 'art2.jpg' },
                { title: '대왕 생선', description: '다양한 물고기들의 조합체입니다.', img: 'art3.jpg' },
            ],
        };

        function showGallery(id) {
            const gallery = document.getElementById(id);
            const galleryItems = gallery.querySelector('.gallery-items');
            galleryItems.innerHTML = '';

            galleryData[id].forEach(item => {
                const overlay = document.createElement('div');
                overlay.className = 'overlay';
                overlay.innerHTML = `
                    <img src="${item.img}" alt="${item.title}">
                    <div class="description">
                        <strong>${item.title}</strong><br>${item.description}
                    </div>
                `;
                galleryItems.appendChild(overlay);
            });

            document.querySelectorAll('.circle-button').forEach(button => button.style.display = 'none');
            document.querySelectorAll('.gallery').forEach(gallery => gallery.style.display = 'none');
            gallery.style.display = 'flex';
        }

        function goBack() {
            document.querySelectorAll('.circle-button').forEach(button => button.style.display = 'flex');
            document.querySelectorAll('.gallery').forEach(gallery => gallery.style.display = 'none');
        }
    </script>
</body>
</html>


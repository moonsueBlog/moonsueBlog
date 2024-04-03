---
layout: post
title: 서울 어디서 여행할까
date: 2024-04-03 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 34.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---
## 서울 관광지 혼잡도

:heart: 수영과 문수 서울 데이트 할 장소를 찾아보자요:kissing_heart:
(실시간 서울 관광지 인구 데이터)

<!-- HTML과 JavaScript 코드 시작 -->
<div class="button-container">
    <button class="button" onclick="getData('전체보기')">전체보기</button>
    <button class="button" onclick="getData('관광특구')">관광특구</button>
    <button class="button" onclick="getData('공원')">공원</button>
    <button class="button" onclick="getData('고궁·문화유산')">고궁·문화유산</button>
    <button class="button" onclick="getData('발달상권')">발달상권</button>
    <button class="button" onclick="getData('인구밀집지역')">인구밀집지역</button>
</div>

<div id="cardContainer" class="card-container">
   
</div>

<style>
    .card-container {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        justify-content: center; /* 중앙 정렬을 추가합니다. */
    }
    .card {
        width: 250px;
        border-radius: 10px;
        overflow: hidden;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
        background: #fff;
    }
    .card img {
        width: 100%;
        height: 150px;
        object-fit: cover;
    }
    .card-info {
        padding: 15px;
    }
    .card-title {
        font-size: 16px;
        font-weight: bold;
        margin: 5px 0;
    }
    .status-label {
        display: inline-block;
        padding: 5px 10px;
        border-radius: 20px;
        color: #fff;
        text-align: center;
        margin-top: 10px;
    }
    .busy { background: #DD1F3D; }
    .moderate { background: #FF8040; }
    .calm { background: #FFB100; }
    .button-container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
        margin-bottom: 30px;
    }
    .button {
        padding: 10px 20px;
        border-radius: 5px;
        background-color: #007bff;
        color: #fff;
        cursor: pointer;
        border: none;
        outline: none;
        transition: background-color 0.3s;
    }
    .button:hover {
        background-color: #0056b3;
    }

    @media (max-width: 768px) {
        .card {
            width: 100%; /* 모바일에서는 카드의 너비를 화면 너비에 맞춥니다. */
        }
        .button {
            width: 100%; /* 모바일에서 버튼의 너비를 조정합니다. */
            margin-bottom: 10px; /* 버튼 간의 마진을 추가합니다. */
        }
    }
</style>


<script>
    function getData(category) {
        var xhr = new XMLHttpRequest();
        xhr.open("GET", "https://data.seoul.go.kr/SeoulRtd/getCategoryList?page=1&category=" + encodeURIComponent(category) + "&count=115&sort=true", true);
        xhr.onload = function () {
            if (xhr.status >= 200 && xhr.status < 300) {
                var data = JSON.parse(xhr.responseText);
                var cardContainer = document.getElementById('cardContainer');
                cardContainer.innerHTML = '';

                data.row.forEach(function(item) {
                    var card = document.createElement('div');
                    card.className = 'card';

                    var img = document.createElement('img');
                    img.src = 'https://cdn.ekw.co.kr/news/photo/202008/10197_10652_4054.jpg';
                    img.alt = item.area_nm;

                    var cardInfo = document.createElement('div');
                    cardInfo.className = 'card-info';

                    var title = document.createElement('div');
                    title.className = 'card-title';
                    title.textContent = item.area_nm;

                        var statusLabel = document.createElement('div');
                        statusLabel.className = 'status-label';
                        statusLabel.style.backgroundColor = item.congestion_color;
                        statusLabel.textContent = item.area_congest_lvl;

                        cardInfo.appendChild(title);
                        cardInfo.appendChild(statusLabel);
                        card.appendChild(img); // 이미지 추가
                        card.appendChild(cardInfo);

                        cardContainer.appendChild(card);
                });
            } else {
                console.error('The request failed!');
            }
        };
        xhr.send();
    }
</script>
<!-- HTML과 JavaScript 코드 끝 -->

---
layout: post
title: 미아 사거리 하행 열차정보
date: 2024-04-03 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 34.jpg # Add image post (optional)
tags: [seoul, subway] # add tag
---
## 마이사거리 열차 정보


<div id="station-container" class="station-container">
  <!-- 실시간 도착 정보가 여기에 표시됩니다 -->
</div>


<style>
  .station-container {
    font-family: 'Arial', sans-serif;
    color: #333;
    max-width: 700px;
    margin: 20px auto;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background-color: #f9f9f9;
  }

  .line-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    background: #00A5DE;
    color: white;
    padding: 10px;
    border-radius: 10px;
  }

  .station-name {
    font-size: 1.5em;
    color: white;
  }

  .arrival-time {
    font-size: 1.2em;
    font-weight: bold;
  }

  .time-bar {
    display: flex;
    align-items: center;
  }

  .time-dot {
    height: 20px;
    width: 20px;
    background-color: white;
    border-radius: 50%;
    display: inline-block;
    margin-right: 5px;
  }

  .time-line {
    flex-grow: 1;
    height: 5px;
    background-color: white;
  }

  /* 이곳에 추가적인 스타일링을 추가합니다. */
</style>

<script>
/* 실제 API로부터 데이터를 받아오는 코드는 여기에 들어갑니다. */

function fetchData() {
  // 실제 API 호출
  fetch('http://swopenapi.seoul.go.kr/api/subway/{keyvalue}/json/realtimeStationArrival/1/5/%EB%AF%B8%EC%95%84%EC%82%AC%EA%B1%B0%EB%A6%AC')
    .then(response => response.json())
    .then(data => {
      // API에서 받은 데이터로 DOM 업데이트
      updateDOM(data.realtimeArrivalList);
    })
    .catch(error => {
      console.error('Error fetching data: ', error);
      // 오류 처리 로직
    });
}


/* 화면 업데이트 함수 */
function updateDOM(arrivalList) {
  const stationContainer = document.getElementById('station-container');
  stationContainer.innerHTML = ''; // 컨테이너를 비웁니다.

  arrivalList.filter(item => item.updnLine === '하행').forEach((item, index) => {
    if (index < 2) { // 첫 번째와 두 번째 하행 정보만 표시
      const lineInfoDiv = document.createElement('div');
      lineInfoDiv.className = 'line-info';

      const stationNameSpan = document.createElement('span');
      stationNameSpan.className = 'station-name';
      stationNameSpan.textContent = '미아사거리';

      const arrivalTimeSpan = document.createElement('span');
      arrivalTimeSpan.className = 'arrival-time';
      arrivalTimeSpan.textContent = item.arvlMsg2;

      lineInfoDiv.appendChild(stationNameSpan);
      lineInfoDiv.appendChild(arrivalTimeSpan);

      const timeBarDiv = document.createElement('div');
      timeBarDiv.className = 'time-bar';

      const timeDotDiv = document.createElement('div');
      timeDotDiv.className = 'time-dot';

      const timeLineDiv = document.createElement('div');
      timeLineDiv.className = 'time-line';

      timeBarDiv.appendChild(timeDotDiv);
      timeBarDiv.appendChild(timeLineDiv);

      lineInfoDiv.appendChild(timeBarDiv);

      stationContainer.appendChild(lineInfoDiv);
    }
  });
}
document.addEventListener('DOMContentLoaded', fetchData);

</script>
<!-- HTML과 JavaScript 코드 끝 -->

<template>
  <body v-for="station in bus_station">
    <div id="bus-table">
        <h2>{{ station.station_name }}</h2>
        <table>
            <thead>
                <tr>
                    <th>버스 번호</th>
                    <th>다음 버스 도착 시간</th>
                    <th>정차 버튼</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="route in station.get_route">
                    <td>{{ route }}</td>
                    <td>{{ station.stop_time }}</td>
                    <td><button class="arrival-button" data-bus="123">정차</button></td>
                </tr>
                <!-- 다른 버스 정보를 추가할 수 있습니다 -->
            </tbody>
        </table>
    </div>
  </body>
</template>


<style scoped>

  body {
      font-family: Arial, sans-serif;
      margin: 0;
      height: 100%;
  }
  h2{
    padding: 10px;
  }

  #bus-table {
      font-size: 30px;
      background-color: #fff;
      padding: 20px;
      margin: 20px;
      border: 2px solid #333;
      border-radius: 10px;
      max-width: 800px;
      margin: 0 auto;
      overflow-x: auto; /* 가로 스크롤바 활성화 */
  }

  table {
      width: 100%;
      height: 700px;
      border-collapse: collapse;
  }

  table, th, td {
      border: 1px solid #000;
  }

  th, td {
      padding: 15px;
      text-align: center;
  }

  th {
      background-color: #333;
      color: #fff;
  }

  tr:nth-child(even) {
      background-color: #f2f2f2;
  }
  .arrival-button{
    font-size: 35px;
  }

</style>


<script setup>
import { ref } from 'vue'

const bus_station = ref(null);
const API_URL = 'http://127.0.0.1:8000/api/';
fetch(API_URL + 'BusStation/')
  .then(res => res.json())
  .then(json => bus_station.value = json)

</script>

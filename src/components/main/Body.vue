<template>
  <div>
      <div class="status_ic">
      </div>
      <div class="status_score">
          {{ score }}
      </div>
      <div class="status_descrption">

      </div>
      <div class="status_datetime">
          {{ datetime }}
      </div>
      <button @click="getData">가져오기</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            score: 0,
            datetime: 0,
        }
    },
    created: function() {
        this.getData();
        this.searchCoordinateToAddress()
    },
    methods : {
        getData() {
            axios({
                method: 'get',
                url : 'http://openAPI.seoul.go.kr:8088/sample/json/RealtimeCityAir/1/5/',
                responseType: 'json'
            }).then(response=> {
                let PM10=response.data.RealtimeCityAir.row[0];
                this.score = PM10.PM10;
                this.datetime = PM10.MSRDT;
            })
        },
        searchCoordinateToAddress() {
            latlag=navigator.geolocation.getCurrentPosition();
            console.log(latlag);
            var tm128 = naver.maps.TransCoord.fromLatLngToTM128(latlng);

            infoWindow.close();

            naver.maps.Service.reverseGeocode({
                location: tm128,
                coordType: naver.maps.Service.CoordType.TM128
            }, function(status, response) {
                if (status === naver.maps.Service.Status.ERROR) {
                    return alert('Something Wrong!');
                }

                var items = response.result.items,
                    htmlAddresses = [];

                for (var i=0, ii=items.length, item, addrType; i<ii; i++) {
                    item = items[i];
                    addrType = item.isRoadAddress ? '[도로명 주소]' : '[지번 주소]';

                    htmlAddresses.push((i+1) +'. '+ addrType +' '+ item.address);
                    htmlAddresses.push('&nbsp&nbsp&nbsp -> '+ item.point.x +','+ item.point.y);
                }

                infoWindow.setContent([
                        '<div style="padding:10px;min-width:200px;line-height:150%;">',
                        '<h4 style="margin-top:5px;">검색 좌표 : '+ response.result.userquery +'</h4><br />',
                        htmlAddresses.join('<br />'),
                        '</div>'
                    ].join('\n'));

                infoWindow.open(map, latlng);
        });
}

    }

}
</script>

<style>

</style>

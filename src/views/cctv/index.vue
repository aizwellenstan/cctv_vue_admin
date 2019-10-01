<template>
  <div class="example">
    <div class="tabs">
      <TabItem
        v-for="item in list"
        :key="item.id"
        v-model="currentId"
        v-bind="item"
      />
    </div>
    <div id="contents" class="contents">
      <transition>
        <section :key="currentId">
          <!-- {{ current.content }} -->
          <div v-for="(cam, index) in current.cams" :key="index" height="700px">
            <div class="camdiv">
              <img :id="cam.cam" width="100%" height="110px">
              {{ cam.cam }}
            </div>
          </div>
        </section>
      </transition>
    </div>
  </div>
</template>

<script>
import TabItem from './TabItem.vue'
import io from 'socket.io-client'

export default {
  components: { TabItem },
  data() {
    return {
    //   socket: io('localhost:6147/cam0'),
      currentId: 1,
      list: [
        {
          id: 1,
          label: 'Tab1',
          content: 'コンテンツ1',
          cams: [
            {
              cam: 'cam0'
            },
            {
              cam: 'cam1'
            },
            {
              cam: 'cam2'
            },
            {
              cam: 'cam3'
            },
            {
              cam: 'cam4'
            },
            {
              cam: 'cam5'
            },
            {
              cam: 'cam6'
            },
            {
              cam: 'cam7'
            },
            {
              cam: 'cam8'
            },
            {
              cam: 'cam9'
            },
            {
              cam: 'cam10'
            },
            {
              cam: 'cam11'
            },
            {
              cam: 'cam12'
            },
            {
              cam: 'cam13'
            },
            {
              cam: 'cam14'
            },
            {
              cam: 'cam15'
            },
            {
              cam: 'cam16'
            },
            {
              cam: 'cam17'
            },
            {
              cam: 'cam18'
            },
            {
              cam: 'cam19'
            },
            {
              cam: 'cam20'
            },
            {
              cam: 'cam21'
            },
            {
              cam: 'cam22'
            },
            {
              cam: 'cam23'
            },
            {
              cam: 'cam24'
            },
            {
              cam: 'cam25'
            },
            {
              cam: 'cam26'
            },
            {
              cam: 'cam27'
            },
            {
              cam: 'cam28'
            },
            {
              cam: 'cam29'
            },
            {
              cam: 'cam30'
            },
            {
              cam: 'cam31'
            },
            {
              cam: 'cam32'
            },
            {
              cam: 'cam33'
            },
            {
              cam: 'cam34'
            },
            {
              cam: 'cam35'
            },
            {
              cam: 'cam36'
            },
            {
              cam: 'cam37'
            },
            {
              cam: 'cam38'
            },
            {
              cam: 'cam39'
            }
          ]
        },
        {
          id: 2,
          label: 'Tab2',
          content: 'コンテンツ2',
          cams: [
            {
              cam: 'cam40'
            },
            {
              cam: 'cam41'
            },
            {
              cam: 'cam42'
            },
            {
              cam: 'cam43'
            },
            {
              cam: 'cam44'
            },
            {
              cam: 'cam45'
            },
            {
              cam: 'cam46'
            },
            {
              cam: 'cam47'
            },
            {
              cam: 'cam48'
            },
            {
              cam: 'cam49'
            },
            {
              cam: 'cam50'
            },
            {
              cam: 'cam51'
            },
            {
              cam: 'cam52'
            },
            {
              cam: 'cam53'
            },
            {
              cam: 'cam54'
            },
            {
              cam: 'cam55'
            },
            {
              cam: 'cam56'
            },
            {
              cam: 'cam57'
            },
            {
              cam: 'cam58'
            },
            {
              cam: 'cam59'
            },
            {
              cam: 'cam60'
            },
            {
              cam: 'cam61'
            },
            {
              cam: 'cam62'
            },
            {
              cam: 'cam63'
            },
            {
              cam: 'cam64'
            },
            {
              cam: 'cam65'
            },
            {
              cam: 'cam66'
            },
            {
              cam: 'cam67'
            },
            {
              cam: 'cam68'
            },
            {
              cam: 'cam69'
            },
            {
              cam: 'cam70'
            },
            {
              cam: 'cam71'
            },
            {
              cam: 'cam72'
            },
            {
              cam: 'cam73'
            },
            {
              cam: 'cam74'
            },
            {
              cam: 'cam75'
            },
            {
              cam: 'cam76'
            },
            {
              cam: 'cam77'
            },
            {
              cam: 'cam78'
            },
            {
              cam: 'cam79'
            }
          ]
        }
      ]
    }
  },
  computed: {
    current() {
      return this.list.find(el => el.id === this.currentId) || {}
    }
  },
  mounted() {
    function base64ArrayBuffer(arrayBuffer) {
      var base64 = ''
      var encodings = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'

      var bytes = new Uint8Array(arrayBuffer)
      var byteLength = bytes.byteLength
      var byteRemainder = byteLength % 3
      var mainLength = byteLength - byteRemainder

      var a, b, c, d
      var chunk

      // Main loop deals with bytes in chunks of 3
      for (var i = 0; i < mainLength; i = i + 3) {
        // Combine the three bytes into a single integer
        chunk = (bytes[i] << 16) | (bytes[i + 1] << 8) | bytes[i + 2]

        // Use bitmasks to extract 6-bit segments from the triplet
        a = (chunk & 16515072) >> 18 // 16515072 = (2^6 - 1) << 18
        b = (chunk & 258048) >> 12 // 258048   = (2^6 - 1) << 12
        c = (chunk & 4032) >> 6 // 4032     = (2^6 - 1) << 6
        d = chunk & 63 // 63       = 2^6 - 1

        // Convert the raw binary segments to the appropriate ASCII encoding
        base64 += encodings[a] + encodings[b] + encodings[c] + encodings[d]
      }

      // Deal with the remaining bytes and padding
      if (byteRemainder === 1) {
        chunk = bytes[mainLength]

        a = (chunk & 252) >> 2 // 252 = (2^6 - 1) << 2

        // Set the 4 least significant bits to zero
        b = (chunk & 3) << 4 // 3   = 2^2 - 1

        base64 += encodings[a] + encodings[b] + '=='
      } else if (byteRemainder === 2) {
        chunk = (bytes[mainLength] << 8) | bytes[mainLength + 1]

        a = (chunk & 64512) >> 10 // 64512 = (2^6 - 1) << 10
        b = (chunk & 1008) >> 4 // 1008  = (2^6 - 1) << 4

        // Set the 2 least significant bits to zero
        c = (chunk & 15) << 2 // 15    = 2^4 - 1

        base64 += encodings[a] + encodings[b] + encodings[c] + '='
      }

      return base64
    }
    var uri = []
    var socket = []
    var image = []
    var bytes = []
    for (var i = 0; i < 39; i++) {
      image[i] = document.getElementById(('cam' + i).toString())
      uri[i] = '192.168.1.165:6147/cam' + i
      uri[i] = uri[i].toString()
      socket[i] = io(uri[i])
    }
    function sleep(waitMsec) {
      var startMsec = new Date()
      while (new Date() - startMsec < waitMsec) {
        console.log()
      }
    }

    socket[0].on('data', function(data0) {
      bytes[0] = new Uint8Array(data0)
      image[0].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[0])
    })
    sleep(200)
    socket[1].on('data', function(data1) {
      bytes[1] = new Uint8Array(data1)
      image[1].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[1])
    })
    sleep(200)
    socket[2].on('data', function(data2) {
      bytes[2] = new Uint8Array(data2)
      image[2].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[2])
    })
    sleep(200)
    socket[3].on('data', function(data3) {
      bytes[3] = new Uint8Array(data3)
      image[3].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[3])
    })
    sleep(200)
    socket[4].on('data', function(data4) {
      bytes[4] = new Uint8Array(data4)
      image[4].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[4])
    })
    sleep(200)
    socket[5].on('data', function(data5) {
      bytes[5] = new Uint8Array(data5)
      image[5].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[5])
    })
    sleep(200)
    socket[6].on('data', function(data6) {
      bytes[6] = new Uint8Array(data6)
      image[6].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[6])
    })
    sleep(200)
    socket[7].on('data', function(data7) {
      bytes[7] = new Uint8Array(data7)
      image[7].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[7])
    })
    sleep(200)
    socket[8].on('data', function(data8) {
      bytes[8] = new Uint8Array(data8)
      image[8].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[8])
    })
    sleep(200)
    socket[9].on('data', function(data9) {
      bytes[9] = new Uint8Array(data9)
      image[9].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[9])
    })
    sleep(200)
    socket[10].on('data', function(data10) {
      bytes[10] = new Uint8Array(data10)
      image[10].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[10])
    })
    sleep(200)
    socket[11].on('data', function(data11) {
      bytes[11] = new Uint8Array(data11)
      image[11].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[11])
    })
    sleep(200)
    socket[12].on('data', function(data12) {
      bytes[12] = new Uint8Array(data12)
      image[12].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[12])
    })
    sleep(200)
    socket[13].on('data', function(data13) {
      bytes[13] = new Uint8Array(data13)
      image[13].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[13])
    })
    sleep(200)
    socket[14].on('data', function(data14) {
      bytes[14] = new Uint8Array(data14)
      image[14].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[14])
    })
    sleep(200)
    socket[15].on('data', function(data15) {
      bytes[15] = new Uint8Array(data15)
      image[15].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[15])
    })
    sleep(200)
    socket[16].on('data', function(data16) {
      bytes[16] = new Uint8Array(data16)
      image[16].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[16])
    })
    sleep(200)
    socket[17].on('data', function(data17) {
      bytes[17] = new Uint8Array(data17)
      image[17].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[17])
    })
    sleep(200)
    socket[18].on('data', function(data18) {
      bytes[18] = new Uint8Array(data18)
      image[18].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[18])
    })
    sleep(200)
    socket[19].on('data', function(data19) {
      bytes[19] = new Uint8Array(data19)
      image[19].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[19])
    })
    sleep(200)
    socket[20].on('data', function(data20) {
      bytes[20] = new Uint8Array(data20)
      image[20].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[20])
    })
    sleep(200)
    socket[21].on('data', function(data21) {
      bytes[21] = new Uint8Array(data21)
      image[21].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[21])
    })
    sleep(200)
    socket[22].on('data', function(data22) {
      bytes[22] = new Uint8Array(data22)
      image[22].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[22])
    })
    sleep(200)
    socket[23].on('data', function(data23) {
      bytes[23] = new Uint8Array(data23)
      image[23].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[23])
    })
    sleep(200)
    socket[24].on('data', function(data24) {
      bytes[24] = new Uint8Array(data24)
      image[24].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[24])
    })
    sleep(200)
    socket[25].on('data', function(data25) {
      bytes[25] = new Uint8Array(data25)
      image[25].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[25])
    })
    sleep(200)
    socket[26].on('data', function(data26) {
      bytes[26] = new Uint8Array(data26)
      image[26].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[26])
    })
    sleep(200)
    socket[27].on('data', function(data27) {
      bytes[27] = new Uint8Array(data27)
      image[27].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[27])
    })
    sleep(200)
    socket[28].on('data', function(data28) {
      bytes[28] = new Uint8Array(data28)
      image[28].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[28])
    })
    sleep(200)
    socket[29].on('data', function(data29) {
      bytes[29] = new Uint8Array(data29)
      image[29].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[29])
    })
    sleep(200)
    socket[30].on('data', function(data30) {
      bytes[30] = new Uint8Array(data30)
      image[30].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[30])
    })
    sleep(200)
    socket[31].on('data', function(data31) {
      bytes[31] = new Uint8Array(data31)
      image[31].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[31])
    })
    sleep(200)
    socket[32].on('data', function(data32) {
      bytes[32] = new Uint8Array(data32)
      image[32].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[32])
    })
    sleep(200)
    socket[33].on('data', function(data33) {
      bytes[33] = new Uint8Array(data33)
      image[33].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[33])
    })
    sleep(200)
    socket[34].on('data', function(data34) {
      bytes[34] = new Uint8Array(data34)
      image[34].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[34])
    })
    sleep(200)
    socket[35].on('data', function(data35) {
      bytes[35] = new Uint8Array(data35)
      image[35].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[35])
    })
    sleep(200)
    socket[36].on('data', function(data36) {
      bytes[36] = new Uint8Array(data36)
      image[36].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[36])
    })
    sleep(200)
    socket[37].on('data', function(data37) {
      bytes[37] = new Uint8Array(data37)
      image[37].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[37])
    })
    sleep(200)
    socket[38].on('data', function(data38) {
      bytes[38] = new Uint8Array(data38)
      image[38].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[38])
    })
    sleep(200)
    socket[39].on('data', function(data39) {
      bytes[39] = new Uint8Array(data39)
      image[39].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[39])
    })
    socket[40].on('data', function(data40) {
      bytes[40] = new Uint8Array(data40)
      image[40].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[40])
    })
    sleep(200)
    socket[41].on('data', function(data41) {
      bytes[41] = new Uint8Array(data41)
      image[41].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[41])
    })
    sleep(200)
    socket[42].on('data', function(data42) {
      bytes[42] = new Uint8Array(data42)
      image[42].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[42])
    })
    sleep(200)
    socket[43].on('data', function(data43) {
      bytes[43] = new Uint8Array(data43)
      image[43].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[43])
    })
    sleep(200)
    socket[44].on('data', function(data44) {
      bytes[44] = new Uint8Array(data44)
      image[44].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[44])
    })
    sleep(200)
    socket[45].on('data', function(data45) {
      bytes[45] = new Uint8Array(data45)
      image[45].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[45])
    })
    sleep(200)
    socket[46].on('data', function(data46) {
      bytes[46] = new Uint8Array(data46)
      image[46].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[46])
    })
    sleep(200)
    socket[47].on('data', function(data7) {
      bytes[47] = new Uint8Array(data7)
      image[47].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[47])
    })
    sleep(200)
    socket[48].on('data', function(data48) {
      bytes[48] = new Uint8Array(data48)
      image[48].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[48])
    })
    sleep(200)
    socket[49].on('data', function(data49) {
      bytes[49] = new Uint8Array(data49)
      image[49].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[49])
    })
    socket[50].on('data', function(data50) {
      bytes[50] = new Uint8Array(data50)
      image[50].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[50])
    })
    sleep(200)
    socket[51].on('data', function(data51) {
      bytes[51] = new Uint8Array(data51)
      image[51].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[15])
    })
    sleep(200)
    socket[52].on('data', function(data52) {
      bytes[52] = new Uint8Array(data52)
      image[52].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[52])
    })
    sleep(200)
    socket[53].on('data', function(data53) {
      bytes[53] = new Uint8Array(data53)
      image[53].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[53])
    })
    sleep(200)
    socket[54].on('data', function(data54) {
      bytes[54] = new Uint8Array(data54)
      image[54].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[54])
    })
    sleep(200)
    socket[55].on('data', function(data55) {
      bytes[55] = new Uint8Array(data55)
      image[55].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[55])
    })
    sleep(200)
    socket[56].on('data', function(data56) {
      bytes[56] = new Uint8Array(data56)
      image[56].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[56])
    })
    sleep(200)
    socket[57].on('data', function(data57) {
      bytes[57] = new Uint8Array(data57)
      image[57].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[57])
    })
    sleep(200)
    socket[58].on('data', function(data58) {
      bytes[58] = new Uint8Array(data58)
      image[58].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[58])
    })
    sleep(200)
    socket[59].on('data', function(data59) {
      bytes[59] = new Uint8Array(data59)
      image[59].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[59])
    })
    socket[60].on('data', function(data60) {
      bytes[60] = new Uint8Array(data60)
      image[60].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[60])
    })
    sleep(200)
    socket[61].on('data', function(data61) {
      bytes[61] = new Uint8Array(data61)
      image[61].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[61])
    })
    sleep(200)
    socket[62].on('data', function(data62) {
      bytes[62] = new Uint8Array(data62)
      image[62].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[62])
    })
    sleep(200)
    socket[63].on('data', function(data63) {
      bytes[63] = new Uint8Array(data63)
      image[63].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[63])
    })
    sleep(200)
    socket[64].on('data', function(data64) {
      bytes[64] = new Uint8Array(data64)
      image[64].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[64])
    })
    sleep(200)
    socket[65].on('data', function(data65) {
      bytes[65] = new Uint8Array(data65)
      image[65].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[65])
    })
    sleep(200)
    socket[66].on('data', function(data66) {
      bytes[66] = new Uint8Array(data66)
      image[66].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[66])
    })
    sleep(200)
    socket[67].on('data', function(data67) {
      bytes[67] = new Uint8Array(data67)
      image[67].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[67])
    })
    sleep(200)
    socket[68].on('data', function(data68) {
      bytes[68] = new Uint8Array(data68)
      image[68].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[68])
    })
    sleep(200)
    socket[69].on('data', function(data69) {
      bytes[69] = new Uint8Array(data69)
      image[69].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[69])
    })
    sleep(200)
    socket[0].on('data', function(data70) {
      bytes[70] = new Uint8Array(data70)
      image[70].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[70])
    })
    sleep(200)
    socket[71].on('data', function(data71) {
      bytes[71] = new Uint8Array(data71)
      image[71].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[71])
    })
    sleep(200)
    socket[72].on('data', function(data72) {
      bytes[72] = new Uint8Array(data72)
      image[72].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[72])
    })
    sleep(200)
    socket[73].on('data', function(data73) {
      bytes[73] = new Uint8Array(data73)
      image[73].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[73])
    })
    sleep(200)
    socket[74].on('data', function(data74) {
      bytes[74] = new Uint8Array(data74)
      image[74].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[74])
    })
    sleep(200)
    socket[75].on('data', function(data75) {
      bytes[75] = new Uint8Array(data75)
      image[75].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[75])
    })
    sleep(200)
    socket[76].on('data', function(data76) {
      bytes[76] = new Uint8Array(data76)
      image[76].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[76])
    })
    sleep(200)
    socket[77].on('data', function(data77) {
      bytes[77] = new Uint8Array(data77)
      image[77].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[77])
    })
    sleep(200)
    socket[78].on('data', function(data78) {
      bytes[78] = new Uint8Array(data78)
      image[78].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[78])
    })
    sleep(200)
    socket[79].on('data', function(data79) {
      bytes[79] = new Uint8Array(data79)
      image[79].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[79])
    })
  }
}
</script>

<style scoped>
.example {
	position: absolute; top: 0; left: 0; height: 100%; width: 100%;
}
.contents {
	height: 100%;
  position: relative;
  overflow: hidden;
  border: 2px solid #000;
}
.item {
  box-sizing: border-box;
  padding: 10px;
  width: 100%;
  transition: all 0.8s ease;
}
/* トランジション用スタイル */
.v-leave-active {
  position: absolute;
}
.v-enter {
  transform: translateX(-100%);
}
.v-leave-to {
  transform: translateX(100%);
}
.camdiv {
	float:left;
	width: 12.5%;
	height: 110px
}
</style>

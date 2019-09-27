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
              {{ cam.cam }}
              <img :id="cam.cam" width="100%" height="100px">
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
          content: 'コンテンツ2'
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
    sleep(4)
    socket[1].on('data', function(data1) {
      bytes[1] = new Uint8Array(data1)
      image[1].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[1])
    })
    sleep(4)
    socket[2].on('data', function(data2) {
      bytes[2] = new Uint8Array(data2)
      image[2].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[2])
    })
    sleep(4)
    socket[3].on('data', function(data3) {
      bytes[3] = new Uint8Array(data3)
      image[3].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[3])
    })
    sleep(4)
    socket[4].on('data', function(data4) {
      bytes[4] = new Uint8Array(data4)
      image[4].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[4])
    })
    sleep(4)
    socket[5].on('data', function(data5) {
      bytes[5] = new Uint8Array(data5)
      image[5].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[5])
    })
    sleep(4)
    socket[6].on('data', function(data6) {
      bytes[6] = new Uint8Array(data6)
      image[6].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[6])
    })
    sleep(4)
    socket[7].on('data', function(data7) {
      bytes[7] = new Uint8Array(data7)
      image[7].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[7])
    })
    sleep(4)
    socket[8].on('data', function(data8) {
      bytes[8] = new Uint8Array(data8)
      image[8].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[8])
    })
    sleep(4)
    socket[9].on('data', function(data9) {
      bytes[9] = new Uint8Array(data9)
      image[9].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[9])
    })
    sleep(4)
    socket[10].on('data', function(data10) {
      bytes[10] = new Uint8Array(data10)
      image[10].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[10])
    })
    sleep(4)
    socket[11].on('data', function(data11) {
      bytes[11] = new Uint8Array(data11)
      image[11].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[11])
    })
    sleep(4)
    socket[12].on('data', function(data12) {
      bytes[12] = new Uint8Array(data12)
      image[12].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[12])
    })
    sleep(4)
    socket[13].on('data', function(data13) {
      bytes[13] = new Uint8Array(data13)
      image[13].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[13])
    })
    sleep(4)
    socket[14].on('data', function(data14) {
      bytes[14] = new Uint8Array(data14)
      image[14].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[14])
    })
    sleep(4)
    socket[15].on('data', function(data15) {
      bytes[15] = new Uint8Array(data15)
      image[15].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[15])
    })
    sleep(4)
    socket[16].on('data', function(data16) {
      bytes[16] = new Uint8Array(data16)
      image[16].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[16])
    })
    sleep(4)
    socket[17].on('data', function(data17) {
      bytes[17] = new Uint8Array(data17)
      image[17].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[17])
    })
    sleep(4)
    socket[18].on('data', function(data18) {
      bytes[18] = new Uint8Array(data18)
      image[18].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[18])
    })
    sleep(4)
    socket[19].on('data', function(data19) {
      bytes[19] = new Uint8Array(data19)
      image[19].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[19])
    })
    sleep(4)
    socket[20].on('data', function(data20) {
      bytes[20] = new Uint8Array(data20)
      image[20].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[20])
    })
    sleep(4)
    socket[21].on('data', function(data21) {
      bytes[21] = new Uint8Array(data21)
      image[21].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[21])
    })
    sleep(4)
    socket[22].on('data', function(data22) {
      bytes[22] = new Uint8Array(data22)
      image[22].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[22])
    })
    sleep(4)
    socket[23].on('data', function(data23) {
      bytes[23] = new Uint8Array(data23)
      image[23].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[23])
    })
    sleep(4)
    socket[24].on('data', function(data24) {
      bytes[24] = new Uint8Array(data24)
      image[24].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[24])
    })
    sleep(4)
    socket[25].on('data', function(data25) {
      bytes[25] = new Uint8Array(data25)
      image[25].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[25])
    })
    sleep(4)
    socket[26].on('data', function(data26) {
      bytes[26] = new Uint8Array(data26)
      image[26].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[26])
    })
    sleep(4)
    socket[27].on('data', function(data27) {
      bytes[27] = new Uint8Array(data27)
      image[27].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[27])
    })
    sleep(4)
    socket[28].on('data', function(data28) {
      bytes[28] = new Uint8Array(data28)
      image[28].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[28])
    })
    sleep(4)
    socket[29].on('data', function(data29) {
      bytes[29] = new Uint8Array(data29)
      image[29].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[29])
    })
    sleep(4)
    socket[30].on('data', function(data30) {
      bytes[30] = new Uint8Array(data30)
      image[30].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[30])
    })
    sleep(4)
    socket[31].on('data', function(data31) {
      bytes[31] = new Uint8Array(data31)
      image[31].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[31])
    })
    sleep(4)
    socket[32].on('data', function(data32) {
      bytes[32] = new Uint8Array(data32)
      image[32].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[32])
    })
    sleep(4)
    socket[33].on('data', function(data33) {
      bytes[33] = new Uint8Array(data33)
      image[33].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[33])
    })
    sleep(4)
    socket[34].on('data', function(data34) {
      bytes[34] = new Uint8Array(data34)
      image[34].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[34])
    })
    sleep(4)
    socket[35].on('data', function(data35) {
      bytes[35] = new Uint8Array(data35)
      image[35].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[35])
    })
    sleep(4)
    socket[36].on('data', function(data36) {
      bytes[36] = new Uint8Array(data36)
      image[36].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[36])
    })
    sleep(4)
    socket[37].on('data', function(data37) {
      bytes[37] = new Uint8Array(data37)
      image[37].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[37])
    })
    sleep(4)
    socket[38].on('data', function(data38) {
      bytes[38] = new Uint8Array(data38)
      image[38].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[38])
    })
    sleep(4)
    socket[39].on('data', function(data39) {
      bytes[39] = new Uint8Array(data39)
      image[39].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[39])
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
	height: 100px
}
</style>

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
              <img :id="cam.cam" width="100%">
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
            },
            {
              cam: 'cam40'
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
    var uri = '192.168.1.165:6147/cam' + (1 - 1)
    console.log(uri)
    var socket = io(uri)
    socket.on('data', function(data) {
      var bytes = new Uint8Array(data)
      setTimeout(function() {
        console.log('imgsrc')
      }, 1000)

      for (var i = 1; i < 41; i++) {
        var image = document.getElementById('cam' + i)
        image.src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes)
      }
      // var image=document.getElementById('cam1')
      // 				image.src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes);
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
	height: 120px
}
</style>

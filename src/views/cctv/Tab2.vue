<template>
  <div width="100%">
    <div v-for="(cam, index) in cams" :key="index" class="camdiv">
      <img :id="cam.cam" class="camimg" width="100%">
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client'
export default {
  data() {
    return {
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
    for (var i = 40; i <= 79; i++) {
      image[i] = document.getElementById(('cam' + i).toString())
      uri[i] = '192.168.1.165:6147/cam' + i
      uri[i] = uri[i].toString()
      socket[i] = io(uri[i])
      image[i].src = 'data:image/png;base64,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'
    }

    socket[40].on('data', function(data40) {
      bytes[40] = new Uint8Array(data40)
      image[40].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[40])
    })

    socket[41].on('data', function(data41) {
      bytes[41] = new Uint8Array(data41)
      image[41].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[41])
    })

    socket[42].on('data', function(data42) {
      bytes[42] = new Uint8Array(data42)
      image[42].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[42])
    })

    socket[43].on('data', function(data43) {
      bytes[43] = new Uint8Array(data43)
      image[43].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[43])
    })

    socket[44].on('data', function(data44) {
      bytes[44] = new Uint8Array(data44)
      image[44].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[44])
    })

    socket[45].on('data', function(data45) {
      bytes[45] = new Uint8Array(data45)
      image[45].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[45])
    })

    socket[46].on('data', function(data46) {
      bytes[46] = new Uint8Array(data46)
      image[46].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[46])
    })

    socket[47].on('data', function(data7) {
      bytes[47] = new Uint8Array(data7)
      image[47].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[47])
    })

    socket[48].on('data', function(data48) {
      bytes[48] = new Uint8Array(data48)
      image[48].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[48])
    })

    socket[49].on('data', function(data49) {
      bytes[49] = new Uint8Array(data49)
      image[49].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[49])
    })
    socket[50].on('data', function(data50) {
      bytes[50] = new Uint8Array(data50)
      image[50].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[50])
    })

    socket[51].on('data', function(data51) {
      bytes[51] = new Uint8Array(data51)
      image[51].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[51])
    })

    socket[52].on('data', function(data52) {
      bytes[52] = new Uint8Array(data52)
      image[52].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[52])
    })

    socket[53].on('data', function(data53) {
      bytes[53] = new Uint8Array(data53)
      image[53].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[53])
    })

    socket[54].on('data', function(data54) {
      bytes[54] = new Uint8Array(data54)
      image[54].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[54])
    })

    socket[55].on('data', function(data55) {
      bytes[55] = new Uint8Array(data55)
      image[55].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[55])
    })

    socket[56].on('data', function(data56) {
      bytes[56] = new Uint8Array(data56)
      image[56].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[56])
    })

    socket[57].on('data', function(data57) {
      bytes[57] = new Uint8Array(data57)
      image[57].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[57])
    })

    socket[58].on('data', function(data58) {
      bytes[58] = new Uint8Array(data58)
      image[58].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[58])
    })

    socket[59].on('data', function(data59) {
      bytes[59] = new Uint8Array(data59)
      image[59].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[59])
    })
    socket[60].on('data', function(data60) {
      bytes[60] = new Uint8Array(data60)
      image[60].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[60])
    })

    socket[61].on('data', function(data61) {
      bytes[61] = new Uint8Array(data61)
      image[61].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[61])
    })

    socket[62].on('data', function(data62) {
      bytes[62] = new Uint8Array(data62)
      image[62].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[62])
    })

    socket[63].on('data', function(data63) {
      bytes[63] = new Uint8Array(data63)
      image[63].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[63])
    })

    socket[64].on('data', function(data64) {
      bytes[64] = new Uint8Array(data64)
      image[64].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[64])
    })

    socket[65].on('data', function(data65) {
      bytes[65] = new Uint8Array(data65)
      image[65].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[65])
    })

    socket[66].on('data', function(data66) {
      bytes[66] = new Uint8Array(data66)
      image[66].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[66])
    })

    socket[67].on('data', function(data67) {
      bytes[67] = new Uint8Array(data67)
      image[67].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[67])
    })

    socket[68].on('data', function(data68) {
      bytes[68] = new Uint8Array(data68)
      image[68].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[68])
    })

    socket[69].on('data', function(data69) {
      bytes[69] = new Uint8Array(data69)
      image[69].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[69])
    })

    socket[0].on('data', function(data70) {
      bytes[70] = new Uint8Array(data70)
      image[70].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[70])
    })

    socket[71].on('data', function(data71) {
      bytes[71] = new Uint8Array(data71)
      image[71].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[71])
    })

    socket[72].on('data', function(data72) {
      bytes[72] = new Uint8Array(data72)
      image[72].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[72])
    })

    socket[73].on('data', function(data73) {
      bytes[73] = new Uint8Array(data73)
      image[73].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[73])
    })

    socket[74].on('data', function(data74) {
      bytes[74] = new Uint8Array(data74)
      image[74].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[74])
    })

    socket[75].on('data', function(data75) {
      bytes[75] = new Uint8Array(data75)
      image[75].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[75])
    })

    socket[76].on('data', function(data76) {
      bytes[76] = new Uint8Array(data76)
      image[76].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[76])
    })

    socket[77].on('data', function(data77) {
      bytes[77] = new Uint8Array(data77)
      image[77].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[77])
    })

    socket[78].on('data', function(data78) {
      bytes[78] = new Uint8Array(data78)
      image[78].src = 'data:image/webP;base64,' + base64ArrayBuffer(bytes[78])
    })

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

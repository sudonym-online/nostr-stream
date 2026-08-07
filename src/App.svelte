<script lang="ts">
    const conf : DisplayMediaStreamOptions = {
        audio: false,
        video: true
    };

    let video!: HTMLVideoElement;
    let frame = $state<string>('')

    async function start(config: DisplayMediaStreamOptions) {
        let stream!: MediaStream;
        try {
            stream = await navigator.mediaDevices.getDisplayMedia(config); 
            video.srcObject = stream;
        } catch (error) {
            console.log(`Error: ${error}`)
        }

    }

    function getFrame(src : HTMLVideoElement) {
       let canvas = document.createElement('canvas');
       canvas.width = src.videoWidth;
       canvas.height = src.videoHeight;
       let ctx = canvas.getContext('2d');
       ctx?.drawImage(src, 0, 0, canvas.width, canvas.height);
       let image = canvas.toDataURL('image/png');
       return image;
    }

</script>

<button id="start" onclick={() => start(conf)}>Start Capture</button>

<!-- <button id="stop">Stop Capture</button> -->

<video id="video" autoplay muted playsinline bind:this={video} ></video>

<button id="frame-btn" onclick={() => frame = getFrame(video)}>Get Current Frame</button>
<img src={frame} alt="captured frame">


<script lang="ts">
    const conf : DisplayMediaStreamOptions = {
        audio: false,
        video: true
    };

    let video!: HTMLVideoElement;

    async function start(config: DisplayMediaStreamOptions) {
        let stream!: MediaStream
        try {
            stream = await navigator.mediaDevices.getDisplayMedia(config); 
            video.srcObject = stream;
        } catch (error) {
            console.log(`Error: ${error}`)
        }

    }
</script>

<button id="start" onclick={() => start(conf)}>Start Capture</button>

<button id="stop">Stop Capture</button>

<video id="video" autoplay muted playsinline bind:this={video} ></video>


<template>
  <Teleport to="body">
    <div class="music-player" :class="{ 'is-playing': isPlaying }" @click="toggleMusic">
      <div class="vinyl-disc">
        <div class="vinyl-inner"></div>
      </div>
      <span class="music-label">♫</span>
    </div>
  </Teleport>
  <!-- Hidden YouTube player -->
  <div id="yt-player-container" style="position:absolute;width:0;height:0;overflow:hidden;pointer-events:none;"></div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const YOUTUBE_VIDEO_ID = 'sBiSqt8k3U4';

const isPlaying = ref(false);
let player = null;
let apiReady = false;

const loadYouTubeAPI = () => {
  return new Promise((resolve) => {
    if (window.YT && window.YT.Player) {
      resolve();
      return;
    }
    const tag = document.createElement('script');
    tag.src = 'https://www.youtube.com/iframe_api';
    document.head.appendChild(tag);
    window.onYouTubeIframeAPIReady = () => {
      resolve();
    };
  });
};

const initPlayer = async () => {
  await loadYouTubeAPI();
  apiReady = true;

  player = new window.YT.Player('yt-player-container', {
    height: '0',
    width: '0',
    videoId: YOUTUBE_VIDEO_ID,
    playerVars: {
      autoplay: 0,
      controls: 0,
      loop: 1,
      playlist: YOUTUBE_VIDEO_ID, // Required for loop to work
      modestbranding: 1,
      rel: 0,
      showinfo: 0,
    },
    events: {
      onReady: () => {
        player.setVolume(40);
      },
      onStateChange: (event) => {
        // YT.PlayerState.ENDED = 0
        if (event.data === 0) {
          player.playVideo(); // Loop fallback
        }
      },
    },
  });
};

onMounted(() => {
  initPlayer();
});

onUnmounted(() => {
  if (player && player.destroy) {
    player.destroy();
  }
});

const toggleMusic = () => {
  if (!player || !apiReady) return;

  if (isPlaying.value) {
    player.pauseVideo();
  } else {
    player.playVideo();
  }
  isPlaying.value = !isPlaying.value;
};

// Auto-play when envelope opens
const startMusic = () => {
  if (player && apiReady && !isPlaying.value) {
    player.playVideo();
    isPlaying.value = true;
  }
};

defineExpose({ startMusic });
</script>

<style>
.music-player {
  position: fixed;
  bottom: 30px;
  right: 20px;
  width: 46px;
  height: 46px;
  z-index: 9999;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(253, 251, 247, 0.9);
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
  border: 1px solid rgba(197, 160, 89, 0.3);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.music-player:hover {
  transform: scale(1.1);
  box-shadow: 0 6px 15px rgba(197, 160, 89, 0.2);
}

.vinyl-disc {
  position: absolute;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: conic-gradient(
    from 0deg,
    #2c2c2c 0deg,
    #3a3a3a 30deg,
    #1a1a1a 60deg,
    #333 90deg,
    #2c2c2c 120deg,
    #3a3a3a 150deg,
    #1a1a1a 180deg,
    #333 210deg,
    #2c2c2c 240deg,
    #3a3a3a 270deg,
    #1a1a1a 300deg,
    #333 330deg,
    #2c2c2c 360deg
  );
  animation: none;
}

.is-playing .vinyl-disc {
  animation: spin 3s linear infinite;
}

.vinyl-inner {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--color-gold) 30%, #c5a059aa 70%);
  border: 1px solid rgba(197, 160, 89, 0.5);
}

.music-label {
  position: relative;
  z-index: 2;
  color: white;
  font-size: 0.7rem;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
  pointer-events: none;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@media (max-width: 600px) {
  .music-player {
    bottom: 20px;
    right: 20px;
    width: 40px;
    height: 40px;
  }
  .vinyl-disc {
    width: 30px;
    height: 30px;
  }
  .vinyl-inner {
    width: 12px;
    height: 12px;
  }
}
</style>

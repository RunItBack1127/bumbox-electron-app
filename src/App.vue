<template>
  <div :class="{'speaker-off': this.speakerOff}" id="speaker-content-container">
    <div class="container--fixed" id="speaker-model-container">
      <SpeakerModelDisplay/>
    </div>
    <div class="container--fixed" id="dashboard-controls-container">
      <DashboardControls/>
    </div>
  </div>
</template>

<script>
import DashboardControls from './components/dashboard/DashboardControls.vue';
import SpeakerModelDisplay from './components/model_display/SpeakerModelDisplay.vue';

export default {
  name: 'App',
  components: {
    DashboardControls,
    SpeakerModelDisplay
  },
  data() {
    return {
      speakerOff: true,
    }
  },
  methods: {
    init: function() {
      window.ipc.on('toggle-speaker-off', () => {
        this.speakerOff = !this.speakerOff;
      });
    }
  },
  mounted() {
    this.init();
    document.title = 'Bumbox';
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  width: 100vw;
  height: 100vh;
}

:root {
  --app-font: "Manrope", sans-serif;
  --app-font-size: 16px;
  --app-content-color: #fff;
  --app-background-color: #000;
}

button {
  background: transparent;
  border: none;
  cursor: pointer;
}

#app {
  font-family: var(--app-font);
  font-size: var(--app-font-size);
  color: var(--app-content-color);
  background-color: var(--app-background-color);
  width: 100%;
  height: 100%;
}

.container--fixed {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
}

#speaker-model-container {
  z-index: 100;
}

#dashboard-controls-container {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: transparent;
  z-index: 100;
}

#speaker-content-container.speaker-off .speaker-toggle-control {
  opacity: 0.5;
  pointer-events: none;
}

@font-face {
  font-family: "Manrope";
  src: url("./assets/fonts/Manrope/Manrope.ttf");
}
</style>

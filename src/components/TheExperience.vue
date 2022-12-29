<script setup lang="ts">
import { ref } from 'vue';
import { Color } from 'three';
import { STLLoader } from 'three/examples/jsm/loaders/STLLoader';

import { useLoader } from '@tresjs/core';
import { OrbitControls, STLModel } from '@tresjs/cientos';

const bgColor = new Color('#82DBC5');

const meshPosition = [0, 3, 0];

const lightRef = ref(null);

const { scene } = await useLoader(
  STLLoader,
  'https://storage.googleapis.com/ucloud-v3/ccab50f18fb14c91ccca300a.stl'
);

scene.position.y = -80;
</script>

<template>
  <Suspense>
    <TresCanvas
      :clear-color="bgColor"
      shadows
      alpha
      window-size
      power-preference="high-performance"
      preserve-drawing-buffer
    >
      <OrbitControls />
      <TresPerspectiveCamera
        :position="[1, 4, 7]"
        :fov="75"
        :near="0.1"
        :far="1000"
      />
      <TresScene :fog="bgColor">
        <TresMesh v-bind="scene" />
        <TresDirectionalLight
          ref="lightRef"
          :position="[-4, 8, 4]"
          :intensity="1.5"
          :look-at="akuAkuRef"
        />
        <TresDirectionalLightHelper v-if="false" :args="[lightRef, 5]" />
        <TresAxesHelper />
      </TresScene>
    </TresCanvas>
  </Suspense>
</template>

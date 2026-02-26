<script setup lang="ts">
/* eslint-disable */
// @ts-nocheck
import { Renderer, Program, Mesh, Color, Triangle } from 'ogl';
import { onMounted, onUnmounted, ref } from 'vue';

const props = defineProps({
  colorStops: { type: Array, default: () => ["#300505", "#050505", "#400505"] },
  amplitude: { type: Number, default: 1.0 },
  speed: { type: Number, default: 0.5 }
});

const container = ref<HTMLElement | null>(null);
let renderer: any, gl: any, program: any, mesh: any, raf: any;

const VERT = `#version 300 es
in vec2 position;
void main() { gl_Position = vec4(position, 0.0, 1.0); }`;

const FRAG = `#version 300 es
precision highp float;
uniform float uTime;
uniform float uAmplitude;
uniform vec3 uColorStops[3];
uniform vec2 uResolution;
out vec4 fragColor;
void main() {
  vec2 uv = gl_FragCoord.xy / uResolution;
  vec3 rampColor = mix(uColorStops[0], uColorStops[1], uv.x);
  fragColor = vec4(rampColor * 0.5, 1.0);
}
`;

onMounted(() => {
  if (!container.value) return;
  renderer = new Renderer({ alpha: true, antialias: true });
  gl = renderer.gl;
  const colorStopsArray = props.colorStops.map(hex => {
    const c = new Color(hex as string);
    return [c.r, c.g, c.b];
  });
  program = new Program(gl, {
    vertex: VERT, fragment: FRAG,
    uniforms: {
      uTime: { value: 0 },
      uAmplitude: { value: props.amplitude },
      uColorStops: { value: colorStopsArray },
      uResolution: { value: [container.value.offsetWidth, container.value.offsetHeight] }
    }
  });
  mesh = new Mesh(gl, { geometry: new Triangle(gl), program });
  container.value.appendChild(gl.canvas);
  const update = (t: number) => {
    raf = requestAnimationFrame(update);
    program.uniforms.uTime.value = t * 0.001 * props.speed;
    renderer.render({ scene: mesh });
  };
  raf = requestAnimationFrame(update);
});

onUnmounted(() => {
  cancelAnimationFrame(raf);
  if (gl) gl.getExtension("WEBGL_lose_context")?.loseContext();
});
</script>

<template>
  <div ref="container" class="absolute inset-0 w-full h-full pointer-events-none -z-10" />
</template>

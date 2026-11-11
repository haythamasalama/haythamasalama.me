<script setup lang="ts">
  /**
   * A short silent product clip that plays in a loop while it is on screen.
   * With reduced motion it stays on its poster and shows controls instead.
   */
  const { src, poster, alt, width, height } = defineProps<{
    src: string;
    poster: string;
    alt: string;
    width: number;
    height: number;
  }>();

  const video = useTemplateRef<HTMLVideoElement>('video');
  const reduced = ref(false);
  let observer: IntersectionObserver | undefined;

  onMounted(() => {
    const element = video.value;

    if (!element) {
      return;
    }

    reduced.value = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    if (reduced.value) {
      return;
    }

    observer = new IntersectionObserver(([entry]) => {
      if (entry?.isIntersecting) {
        element.play().catch(() => {});
      }
      else {
        element.pause();
      }
    }, { threshold: 0.4 });

    observer.observe(element);
  });

  onBeforeUnmount(() => observer?.disconnect());
</script>

<template>
  <figure class="not-prose my-10">
    <div class="overflow-hidden rounded-xl border border-line bg-raised">
      <video
        ref="video"
        :src="src"
        :poster="poster"
        :width="width"
        :height="height"
        :aria-label="alt"
        :controls="reduced"
        muted
        loop
        playsinline
        preload="none"
        class="block h-auto w-full"
      />
    </div>
    <figcaption v-if="$slots.default" class="mt-3 text-sm leading-normal text-muted">
      <slot mdc-unwrap="p" />
    </figcaption>
  </figure>
</template>

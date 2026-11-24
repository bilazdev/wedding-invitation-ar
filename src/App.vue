<script setup lang="ts">
    import PageAr from "./components/page-ar/PageAr.vue";
    import { ref, onMounted, onUnmounted } from 'vue';

    const isLandscape = ref(false);

    let mediaQuery;

    const checkOrientation = () => {
      isLandscape.value = mediaQuery.matches;
    };

    onMounted(() => {
      mediaQuery = window.matchMedia('(orientation: landscape)');

      checkOrientation();

      mediaQuery.addEventListener('change', checkOrientation);
    });

    onUnmounted(() => {
      mediaQuery?.removeEventListener('change', checkOrientation);
    });

</script>

<template>
  <div>
    <!-- Your website content -->
    <slot />

    <!-- Landscape overlay -->
    <div v-if="isLandscape" class="landscape-overlay">
      <div class="message">
        <div class="rotate-icon">📱</div>
        <h2>Oops!</h2>
        <p>
            يتعذر عرض الصفحة في غير الوضعية الأفقية للجوالات حصراً
        </p>
      </div>
    </div>
  </div>
    <PageAr/> 
</template>

<style scoped>
    .rings {
        display: absolute;
        top: 0;
    }

    .landscape-overlay {
  position: fixed;
  inset: 0;
  z-index: 999999;
  width: 100vw;
  height: 100vh;
  height: 100dvh;

  display: flex;
  align-items: center;
  justify-content: center;

  background: #111;
  color: white;
  text-align: center;

  padding: 24px;
  box-sizing: border-box;
}

.message {
  max-width: 320px;
}

.rotate-icon {
  font-size: 48px;
  margin-bottom: 20px;
}

.message h2 {
  font-size: 24px;
  margin-bottom: 12px;
}

.message p {
  font-size: 16px;
  line-height: 1.6;
  color: #ccc;
}
</style>

<script setup>
import AppHeader from './components/AppHeader.vue'
import HeroSection from './components/HeroSection.vue'
import FeaturesSection from './components/FeaturesSection.vue'
import SecuritySection from './components/SecuritySection.vue'
import StatsSection from './components/StatsSection.vue'
import CTASection from './components/CTASection.vue'
import AppFooter from './components/AppFooter.vue'
import ComeSoon from './components/ComeSoon.vue'
</script>


<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
    <AppHeader />
    <HeroSection/>
    <FeaturesSection />
    <SecuritySection />
    <StatsSection />
    <CTASection />
    <ComeSoon />
    <AppFooter /> 
  </div>
</template>

<style scoped>
.prose {
  max-width: none;
}

.prose p {
  margin-bottom: 1rem;
  line-height: 1.6;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

.animate-float {
  animation: float 3s ease-in-out infinite;
}
</style>
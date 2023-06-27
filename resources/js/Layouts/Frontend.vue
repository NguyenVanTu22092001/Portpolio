<script setup>
import Header from "@/Components/Frontend/Header.vue";
import Footer from "@/Components/Frontend/Footer.vue";
// import Hero from "@/Components/Frontend/Hero.vue";
import Promote from "@/Components/Frontend/Promote.vue";
import About from "@/Components/Frontend/About.vue";
import Services from "@/Components/Frontend/Services.vue";
</script>
<template>
    <div class="bg-slate-200 dark:bg-slate-900">
        <!-- Header -->
        <Header />
        
        <main class="min-h-screen">
            <slot />
        </main>
        <!-- Footer -->
        <Footer />
    </div>
</template>
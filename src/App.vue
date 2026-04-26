<!-- TEMPLATE -->
<template>

    <header class="fixed top-0 left-0 w-full z-50 bg-transparent">
        <nav class="w-full px-3 sm:px-4 md:px-6 py-3 md:py-4 flex items-center justify-between font-medium text-white drop-shadow-[0_2px_2px_rgba(0,0,0,0.5)]">
        <h1 class="logo-bubble text-4xl md:text-5xl text-pink-600 drop-shadow-[0_0_5px_#410e34] absolute left-1/2 -translate-x-1/2 md:static md:translate-x-0 ">
          BARBSTAND
        </h1>
        <button class="md:hidden text-2xl px-2" @click="menuAbierto = !menuAbierto" aria-label="Abrir menú"> 
            {{ menuAbierto ? '✕' : '☰' }}
        </button>
        <div v-if="menuAbierto" class="md:hidden absolute top-full left-0 w-full bg-black/80 backdrop-blur-md flex flex-col items-center py-6 gap-6 transition-all">
            <a v-for="item in navegacion" 
              :key="item.href" 
              :href="item.href" 
              @click="menuAbierto = false"
              class="text-xl hover:text-pink-500 transition">
              {{ item.nombre }}
            </a>
        </div>
        <div class="hidden md:flex items-center gap-10">
            <a v-for="item in navegacion" 
              :key="item.href" 
              :href="item.href" 
              class="hover:text-[#ff00cc] hover:drop-shadow-[0_0_10px_#ff00cc] transition">
              {{ item.nombre }}
            </a>
        </div>
      </nav>
    </header>
    <div :class="[colorFondo, 'transition-colors duration-1000 ease-in-out min-h-screen']">
      <main>
        <section id="inicio" data-bg="bg-black" class="h-screen w-full relative overflow-hidden">
      <!-- Carrusel -->
          <Carousel :autoplay="2000" :wrap-around="true" :transition="800"class="h-full w-full">
            <!-- Cambiamos "images" por "slides" para que Vue lea los objetos con texto -->
            <Slide v-for="(slide, i) in slides" :key="i">
              <div 
                class="h-screen w-full bg-cover bg-center flex items-center justify-center relative"
                :style="{ backgroundImage: `url(${slide.url})` }"
              >
                <!-- Capa oscura para que el texto resalte mejor -->
                <div class="absolute inset-0 bg-black/30"></div>

                <div class="relative z-10 text-center px-4">
                  <!-- Aquí imprimimos el título que pusiste (STRAYKIDS, ATEEZ...) -->
                  <h2 class="text-white text-5xl md:text-7xl font-black uppercase italic drop-shadow-2xl">
                    {{ slide.titulo }}
                  </h2>
                  
                  <!-- Aquí imprimimos el subtítulo de cada uno -->
                  <p class="text-white text-lg md:text-2xl mt-4 font-medium drop-shadow-lg">
                    {{ slide.subtitulo }}
                  </p>
                </div>
              </div>
            </Slide>
            <!-- Indicadores (puntitos) -->
            <template #addons>
              <Pagination class="absolute bottom-8 left-1/2 -translate-x-1/2 custom-pagination" />
            </template>
          </Carousel>
        </section>

      <!-- SECCIÓN: QUÉ PODEMOS TRAER -->
        <!-- BENTO GRID-->
        <section id="podemos-traer" data-bg="bg-amber-50" class="py-24 px-6">
        <!-- TÍTULO CON AIRE (Para ambos modos) -->
          <div class="max-w-7xl mx-auto mb-16 px-4">
            <h2 class="text-5xl md:text-7xl font-black text-pink-600 uppercase italic leading-none">
              ¿Qué podemos <br class="md:hidden"> <span class="text-black">traer?</span>
            </h2>
          </div>

          <!-- VISTA MÓVIL: Carrusel (Solo se ve en celulares) -->
          <div class="md:hidden">
            <Carousel :items-to-show="1.1" :snap-align="'center'" :wrap-around="true">
              <Slide v-for="item in categorias" :key="item.id">
                <div class="px-3 w-full h-[500px]">
                  
                  <!-- Si es AliExpress usamos tu diseño rosa, si no, el de imagen -->
                  <div v-if="item.isAli" class="w-full h-full bg-pink-500 rounded-[3rem] flex flex-col justify-center items-center p-8 shadow-xl">
                    <div class="w-48 h-48 bg-white/20 rounded-full flex items-center justify-center mb-6">
                        <img :src="item.img" class="w-32 h-32 object-contain" />
                    </div>
                    <h3 class="text-white font-bold text-2xl uppercase italic text-center">{{ item.titulo }}</h3>
                  </div>

                  <div v-else class="relative w-full h-full rounded-[3rem] overflow-hidden shadow-xl">
                    <img :src="item.img" class="absolute inset-0 w-full h-full object-cover" />
                    <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent flex flex-col justify-end p-10 text-left">
                      <h3 class="text-3xl font-black text-white uppercase italic">{{ item.titulo }}</h3>
                      <p class="text-white/80 text-sm mt-2">{{ item.desc }}</p>
                    </div>
                  </div>
                </div>
              </Slide>
            </Carousel>
          </div>

                    <!-- VISTA DESKTOP: Tu Grid original (Solo se ve en PC) -->
          <div class="hidden md:grid grid-cols-4 grid-rows-2 gap-8 h-[700px]">
            
            <!-- 1. ÁLBUMES (Tus 2 columnas y 2 filas) -->
            <div class="md:col-span-2 md:row-span-2 relative group overflow-hidden rounded-[3rem] shadow-lg">
              <img :src="imgalbum" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
              <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent flex flex-col justify-end p-10 text-white">
                <h3 class="text-3xl font-black uppercase italic">Álbumes</h3>
                <p class="text-sm font-medium opacity-90">Toda la discografía y POBs.</p>
              </div>
            </div>

            <!-- 2. LIGHTSTICKS (Tus 2 columnas y 1 fila) -->
            <div class="md:col-span-2 md:row-span-1 relative group overflow-hidden rounded-[3rem] shadow-lg">
              <img :src="imglightstick" class="absolute inset-0 w-full h-full object-cover transition-transform duration-700 group-hover:scale-105" />
              <div class="absolute inset-0 bg-black/10 group-hover:bg-transparent transition-all flex items-center p-8">
                <h3 class="text-2xl font-black text-white uppercase drop-shadow-lg">Lightsticks</h3>
              </div>
            </div>

            <!-- 3. MERCH OFICIAL (Tu columna 1 y fila 1) -->
            <div class="md:col-span-1 md:row-span-1 relative group overflow-hidden rounded-[3rem] shadow-lg">
              <img :src="imgmerch" class="absolute inset-0 w-full h-full object-cover transition-transform duration-500 group-hover:scale-110" />
              <div class="absolute inset-0 flex items-end justify-center p-6">
                  <span class="bg-white/90 backdrop-blur-sm px-6 py-2 rounded-full text-xs font-bold text-pink-600 uppercase shadow-sm">
                      Merch Oficial
                  </span>
              </div>
            </div>

            <!-- 4. ALIEXPRESS (Tu diseño rosa con el círculo) -->
            <div class="md:col-span-1 md:row-span-1 bg-pink-500 flex flex-col justify-center items-center p-6 rounded-[3rem] hover:rotate-3 transition-transform cursor-pointer shadow-lg shadow-pink-200">
              <div class="w-48 h-48 bg-white/20 rounded-full flex items-center justify-center mb-3 overflow-hidden p-2">
                <img :src="imgali" class="w-full h-full object-contain" />
              </div>
              <h3 class="text-white font-bold text-center leading-tight uppercase text-sm">
                Pedidos de AliExpress
              </h3>
            </div>
          </div>
        </section>



        <!-- SECCIÓN: HORARIO DE ATENCIÓN -->
        <section id="horario" data-bg="bg-black" class="py-24 px-6 flex justify-center items-center">
          <div class="max-w-4xl w-full flex flex-col md:flex-row items-center gap-12 md:gap-24">
            
            <!-- LADO IZQUIERDO: El dibujo del Reloj (Inmóvil) -->
            <div class="shrink-0">
              <div class="relative w-48 h-48 md:w-56 md:h-56 rounded-full bg-white border-4 border-pink-500 shadow-[0_0_30px_rgba(255,0,204,0.3)] flex items-center justify-center">
                
                <!-- Puntos decorativos de las horas -->
                <div class="absolute top-3 w-1 h-3 bg-pink-100 rounded-full"></div>
                <div class="absolute bottom-3 w-1 h-3 bg-pink-100 rounded-full"></div>
                <div class="absolute left-3 h-1 w-3 bg-pink-100 rounded-full"></div>
                <div class="absolute right-3 h-1 w-3 bg-pink-100 rounded-full"></div>

                <!-- Punto central -->
                <div class="w-3 h-3 bg-pink-600 rounded-full z-20"></div>

                <!-- Manecilla de la HORA (Fija en las 10) -->
                <div class="absolute bottom-1/2 left-1/2 w-1.5 h-12 bg-slate-800 origin-bottom -translate-x-1/2 rounded-full rotate-[320deg] z-10"></div>

                <!-- Manecilla de los MINUTOS (Fija en las 2) -->
                <div class="absolute bottom-1/2 left-1/2 w-1 h-18 bg-slate-400 origin-bottom -translate-x-1/2 rounded-full rotate-[45deg] z-10"></div>
              </div>
            </div>

            <!-- LADO DERECHO: La Información -->
            <div class="flex-1 text-center md:text-left space-y-8">
              <h2 class="text-4xl md:text-6xl font-black text-white uppercase italic tracking-tighter">
                Horario de <br> <span class="text-pink-500">Atención</span>
              </h2>

              <div class="space-y-6">
                <!-- Lunes-Viernes -->
                <div class="border-l-4 border-pink-500 pl-6">
                  <p class="text-pink-500 font-bold uppercase text-sm tracking-widest mb-1">Lunes a Viernes</p>
                  <p class="text-white text-2xl font-medium">9:00 am — 6:00 pm</p>
                </div>

                <!-- Sábados -->
                <div class="border-l-4 border-pink-300 pl-6">
                  <p class="text-pink-300 font-bold uppercase text-sm tracking-widest mb-1">Sábados</p>
                  <p class="text-white text-2xl font-medium">10:00 am — 4:00 pm</p>
                </div>

                <!-- Domingos -->
                <div class="border-l-4 border-amber-800 pl-6 opacity-40">
                  <p class="text-amber-500 font-bold uppercase text-sm tracking-widest mb-1">Domingos</p>
                  <p class="text-amber-500 text-xl font-medium">Cerrado</p>
                </div>
              </div>
            </div>
          </div>
        </section>

      </main>
    </div>
    <footer>
      <p>© 2026 Barbstand</p>
    </footer>
</template>

<!-- SCRIPT -->
<script setup>
    import { ref,onMounted } from 'vue'
    const menuAbierto = ref(false)

    const colorFondo = ref('bg-white') // Color inicial (debajo del carrusel)

    onMounted(() => {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {

            colorFondo.value = entry.target.dataset.bg
          }
        })
      }, 
      { threshold: 0.3 }) // Se activa cuando está el 30% de la sección

      // Le decimos al observador que vigile todas las secciones que tengan 'data-bg'
      document.querySelectorAll('section[data-bg]').forEach((section) => {
        observer.observe(section)
      })
    })

    import img1 from './assets/stray-kids-2025-5120x2880-23839.jpg'
    import img2 from './assets/ateez.jpg'
    import img3 from './assets/bts.jpg'
    import img4 from './assets/enhypen.jpeg'
    import img5 from './assets/aespa.jpg'
    import img6 from './assets/blackpink.jpg'
    import img7 from './assets/babymonster.jpg'

    const slides= [
      {
        url:img1, 
        titulo: 'STRAYKIDS',
        subtitulo: 'Traemos tus álbumes y photocards favoritas',
      },
      {
        url:img2,
        titulo: 'ATEEZ',
        subtitulo: 'Treaemos tu merch favorita por encargo',
      },
      {
        url:img3,
        titulo: 'BTS',
        subtitulo: 'Traemos tus álbumes y photocards favoritas',
      },
      {
        url:img4,
        titulo: 'ENHYPEN',
        subtitulo: 'Hacemos tu sueño de tener tus álbumes y merch realidad',
      },
      {
        url:img5,
        titulo: 'AESPA',
        subtitulo: 'Traemos tus álbumes y photocards favoritas',
      },
      {
        url:img6,
        titulo: 'BLACKPINK',
        subtitulo: 'Treaemos tu merch favorita por encargo',
      },
      {
        url:img7,
        titulo: 'BABYMONSTER',
        subtitulo: 'Traemos tus álbumes y photocards favoritas',
      },

    ]
    import 'vue3-carousel/dist/carousel.css'
    import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel'

    import imgalbum from './assets/album.jpg'
    import imglightstick from './assets/lightsticks.jpg' 
    import imgmerch from './assets/kpopplush.jpg' 
    import imgali from './assets/merch.jpg'

    const categorias = [
    {id: 1, titulo: 'Álbumes', desc: 'Toda la discografía y POBs.', img: imgalbum, clase: 'col-span-2 row-span-2' },
    {id: 2, titulo: 'Lightsticks', desc: '', img: imglightstick, clase: 'col-span-2 row-span-1' },
    {id: 3, titulo: 'Merch Oficial', desc: '', img: imgmerch, clase: 'col-span-1 row-span-1' }
    ]
 

    const navegacion = [
    {nombre: 'Inicio', href: '#inicio' },
    {nombre: 'Qué podemos traer', href: '#podemos-traer' },
    {nombre: 'Encargos pasados', href: '#encargos-pasados' },
    {nombre: 'Contacto', href: '#contacto' },
    {nombre: 'Horario de atención', href: '#horario' }
    ]


    
</script>
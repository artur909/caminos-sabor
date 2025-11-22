<template>
  <!-- Hero -->
  <section id="hero" class="relative overflow-hidden hero-bg">
    <div class="stars-overlay"></div>
    <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-8 lg:px-12 py-28 md:py-32 grid md:grid-cols-2 gap-16 items-center">
      <div class="max-w-[75ch]">
        <h1 class="text-4xl md:text-5xl font-extrabold tracking-tight">
          Los Caminos del Sabor
        </h1>
        <p class="mt-6 text-neutral-700">
          Un videojuego que revaloriza la gastronomía peruana con estilo pixelart.
        </p>
        <div class="mt-10 flex gap-6" id="cta">
          <a href="#recetas" class="px-5 py-3 rounded-md bg-[#B13704] text-white font-semibold hover:opacity-90">Explorar recetas</a>
          <a href="#artesanos" class="px-5 py-3 rounded-md bg-[#fec53d] text-[#2b2b2b] font-semibold hover:opacity-90">Canjear productos</a>
        </div>
        <p class="mt-5 text-xs text-neutral-500">Conoce a ganadores y participa para ser el próximo.</p>
      </div>
      <div class="flex md:justify-end">
        <div class="w-full md:w-96 h-56 bg-[linear-gradient(135deg,#fec53d_0%,#B13704_50%,#6c9328_100%)] border-4 border-[#6c9328] shadow-[0_0_0_8px_#fec53d]">
        </div>
      </div>
    </div>
  </section>

  <!-- Descripción del juego -->
  <section id="descripcion" class="bg-white">
    <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-8 lg:px-12 py-28 md:py-32 grid md:grid-cols-3 gap-16">
      <div class="md:col-span-2 max-w-[75ch] section-card">
        <h2 class="section-heading text-2xl md:text-3xl font-extrabold">Descripción del videojuego</h2>
        <p class="mt-8 text-neutral-700 leading-relaxed md:leading-loose">
          Los Caminos del Sabor: un videojuego que invita a redescubrir las recetas y tradiciones culinarias del Perú a través de una experiencia interactiva única.
        </p>
        <p class="mt-6 text-neutral-700 leading-relaxed md:leading-loose">
          La historia nos presenta a Misti y Blanca, dos jóvenes de Paititi que emprenden una travesía por las principales ciudades del país con una misión especial: recopilar los secretos de la cocina peruana para completar el libro de recetas de su maestro.
        </p>
        <p class="mt-6 text-neutral-700 leading-relaxed md:leading-loose">
          Este proyecto busca revalorizar la riqueza gastronómica del Perú, llevando a los jugadores a conocer la diversidad de sabores que caracterizan a cada región.
        </p>
      </div>
      <aside class="space-y-4">
        <div class="section-card">
          <p class="text-sm">Beta presentada en PERUMEC con gran entusiasmo y expectativa.</p>
        </div>
        <div class="section-card">
          <p class="text-sm">Próximamente disponible en Play Store y versión web.</p>
        </div>
      </aside>
    </div>
  </section>

  <!-- Recetas (slider infinito) -->
  <section id="recetas" class="bg-neutral-50">
    <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-8 lg:px-12 py-28 md:py-32 grid md:grid-cols-2 gap-16 items-center">
      <div class="max-w-[75ch]">
        <h2 class="section-heading text-2xl md:text-3xl font-extrabold">Recetas destacadas</h2>
        <p class="mt-4 text-sm text-neutral-600 leading-relaxed">Slider infinito con movimiento automático y videos verticales.</p>
      </div>
      <div class="mt-12 overflow-hidden relative">
        <button class="carousel-arrow absolute left-2 md:left-0 top-1/2 -translate-y-1/2 z-10 grid place-items-center" @click="speedBurst('backward')" @pointerdown="startHold('backward')" @pointerup="stopHold" @pointerleave="stopHold" aria-label="Retroceder">◄</button>
        <button class="carousel-arrow absolute right-2 md:right-0 top-1/2 -translate-y-1/2 z-10 grid place-items-center" @click="speedBurst('forward')" @pointerdown="startHold('forward')" @pointerup="stopHold" @pointerleave="stopHold" aria-label="Avanzar">►</button>
        <div ref="marqueeRef" class="marquee flex gap-6">
          <div class="flex gap-4 shrink-0">
            <article v-for="recipe in recipes" :key="'a-'+recipe.id" class="min-w-64 w-64 bg-white border-2 border-[#2b2b2b] shadow-[4px_4px_0_0_#B13704] hover:shadow-[2px_2px_0_0_#B13704] transition-transform hover:-translate-y-0.5">
              <button class="w-full text-left" @click="openRecipe(recipe)">
                <div class="h-36 bg-[repeating-linear-gradient(45deg,#fec53d_0_10px,#B13704_10px_20px,#6c9328_20px_30px)]"></div>
                <div class="p-4 space-y-2">
                  <h3 class="font-semibold">{{ recipe.title }}</h3>
                  <p class="text-xs text-neutral-600">{{ recipe.subtitle }}</p>
                  <div class="flex items-center gap-2 text-[11px] text-neutral-700">
                    <span class="px-2 py-0.5 bg-[#fec53d] text-[#2b2b2b] rounded">{{ recipe.region }}</span>
                    <span class="px-2 py-0.5 bg-[#6c9328] text-white rounded">{{ recipe.difficulty }}</span>
                    <span class="px-2 py-0.5 bg-[#B13704] text-white rounded">{{ recipe.time }}</span>
                  </div>
                  <div class="mt-2 flex flex-wrap gap-1">
                    <span v-for="tag in recipe.tags" :key="tag" class="px-2 py-0.5 bg-neutral-100 border text-[11px]">{{ tag }}</span>
                  </div>
                </div>
              </button>
            </article>
          </div>
          <div class="flex gap-4 shrink-0" aria-hidden="true">
            <article v-for="recipe in recipes" :key="'b-'+recipe.id" class="min-w-64 w-64 bg-white border-2 border-[#2b2b2b] shadow-[4px_4px_0_0_#B13704]">
              <div class="h-36 bg-[repeating-linear-gradient(45deg,#fec53d_0_10px,#B13704_10px_20px,#6c9328_20px_30px)]"></div>
              <div class="p-4 space-y-2">
                <h3 class="font-semibold">{{ recipe.title }}</h3>
                <p class="text-xs text-neutral-600">{{ recipe.subtitle }}</p>
                <div class="flex items-center gap-2 text-[11px] text-neutral-700">
                  <span class="px-2 py-0.5 bg-[#fec53d] text-[#2b2b2b] rounded">{{ recipe.region }}</span>
                  <span class="px-2 py-0.5 bg-[#6c9328] text-white rounded">{{ recipe.difficulty }}</span>
                  <span class="px-2 py-0.5 bg-[#B13704] text-white rounded">{{ recipe.time }}</span>
                </div>
                <div class="mt-2 flex flex-wrap gap-1">
                  <span v-for="tag in recipe.tags" :key="tag" class="px-2 py-0.5 bg-neutral-100 border text-[11px]">{{ tag }}</span>
                </div>
              </div>
            </article>
          </div>
        </div>
      </div>
      <!--<p class="mt-4 text-xs text-neutral-500">Haz clic en una receta para ver su video vertical.</p>-->
    </div>
  </section>

  <!-- Artesanos -->
  <section id="artesanos" class="bg-white">
    <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-8 lg:px-12 py-28 md:py-32">
      <div class="flex items-center justify-between">
        <h2 class="section-heading text-2xl md:text-3xl font-extrabold">Artesanos y productos</h2>
        <button class="px-3 py-2 rounded-md bg-[#B13704] text-white text-sm font-semibold hover:opacity-90" @click="openProductModal(exampleProduct)">
          Ver producto
        </button>
      </div>
      <div class="mt-12 grid sm:grid-cols-2 md:grid-cols-3 gap-10">
        <article v-for="n in 6" :key="n" class="border rounded-md bg-neutral-50">
          <div class="h-40 bg-[repeating-linear-gradient(90deg,#fec53d_0_12px,#B13704_12px_24px,#6c9328_24px_36px)]"></div>
          <div class="p-4">
            <h3 class="font-semibold">Producto artesanal</h3>
            <p class="text-sm text-neutral-600">Canjeable con puntos del juego.</p>
            <button class="mt-4 px-3 py-2 rounded-md bg-[#fec53d] text-[#2b2b2b] text-sm font-semibold" @click="openProductModal(exampleProduct)">Reclamar</button>
          </div>
        </article>
      </div>
    </div>
  </section>

  <!-- Aliados -->
  <section id="aliados" class="bg-neutral-50">
    <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-8 lg:px-12 py-28 md:py-32">
      <h2 class="section-heading text-2xl md:text-3xl font-extrabold">Aliados</h2>
      <div class="mt-12 grid grid-cols-2 md:grid-cols-4 gap-10">
        <div v-for="n in 8" :key="n" class="h-20 bg-white border rounded-md shadow-sm flex items-center justify-center">
          <span class="w-8 h-8 bg-[#6c9328]"></span>
        </div>
      </div>
    </div>
  </section>

  <!-- Modales -->
  <div v-if="showRecipe" class="fixed inset-0 z-[100] bg-black/60 backdrop-blur-sm flex items-center justify-center p-4" role="dialog" aria-modal="true" @click.self="closeRecipe">
    <div class="relative max-w-5xl w-full h-[85vh] bg-white border-2 border-[#2b2b2b] shadow-[8px_8px_0_0_#B13704] rounded-md overflow-hidden">
      <button class="absolute left-2 top-1/2 -translate-y-1/2 z-[101] p-2 rounded-md border bg-white hover:bg-neutral-50" @click="goToPrevRecipe" aria-label="Anterior">◄</button>
      <button class="absolute right-2 top-1/2 -translate-y-1/2 z-[101] p-2 rounded-md border bg-white hover:bg-neutral-50" @click="goToNextRecipe" aria-label="Siguiente">►</button>
      <div class="flex flex-col h-full">
        <!-- Header del modal -->
        <div class="p-4 border-b flex items-center justify-between">
          <h3 class="font-semibold">{{ selectedRecipe.title }}</h3>
          <div class="flex items-center gap-2 text-xs">
            <span class="px-2 py-0.5 bg-[#fec53d] text-[#2b2b2b] rounded">{{ selectedRecipe.region }}</span>
            <span class="px-2 py-0.5 bg-[#6c9328] text-white rounded">{{ selectedRecipe.difficulty }}</span>
            <span class="px-2 py-0.5 bg-[#B13704] text-white rounded">{{ selectedRecipe.time }}</span>
            <button class="ml-2 px-2 py-1 rounded-md border bg-white hover:bg-neutral-50" @click="closeRecipe" aria-label="Cerrar">✕</button>
          </div>
        </div>
  
        <!-- Contenido en dos columnas -->
        <div class="grid md:grid-cols-2 gap-0 flex-1 min-h-0">
          <!-- Columna izquierda: detalle de la receta -->
          <div class="p-4 overflow-y-auto">
            <p class="text-neutral-700 text-sm">{{ selectedRecipe.description }}</p>

            <div class="mt-4 grid grid-cols-2 gap-3 text-xs">
              <div>
                <h4 class="font-semibold text-sm">Porciones</h4>
                <p class="mt-1">{{ selectedRecipe.servings }} porciones</p>
              </div>
              <div>
                <h4 class="font-semibold text-sm">Calorías</h4>
                <p class="mt-1">~{{ selectedRecipe.calories }} kcal por porción</p>
              </div>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Utensilios</h4>
              <ul class="mt-2 flex flex-wrap gap-2 text-xs">
                <li v-for="u in selectedRecipe.utensils" :key="u" class="px-2 py-1 bg-neutral-100 border rounded">{{ u }}</li>
              </ul>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Ingredientes</h4>
              <ul class="mt-2 flex flex-wrap gap-2 text-xs">
                <li v-for="ing in ingredientList" :key="ing" class="px-2 py-1 bg-neutral-100 border rounded">{{ ing }}</li>
              </ul>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Preparación paso a paso</h4>
              <ol class="mt-2 space-y-2 text-sm list-decimal list-inside">
                <li v-for="(step, i) in selectedRecipe.steps" :key="i">{{ step }}</li>
              </ol>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Acompañamientos</h4>
              <ul class="mt-2 flex flex-wrap gap-2 text-xs">
                <li v-for="p in selectedRecipe.pairings" :key="p" class="px-2 py-1 bg-neutral-100 border rounded">{{ p }}</li>
              </ul>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Alérgenos</h4>
              <ul class="mt-2 flex flex-wrap gap-2 text-xs">
                <li v-for="a in selectedRecipe.allergens" :key="a" class="px-2 py-1 bg-neutral-100 border rounded">{{ a }}</li>
              </ul>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Historia y origen</h4>
              <p class="mt-2 text-xs text-neutral-700">{{ selectedRecipe.origin }}</p>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Notas del chef</h4>
              <p class="mt-2 text-xs text-neutral-700">{{ selectedRecipe.notes }}</p>
            </div>

            <div class="mt-4">
              <h4 class="font-semibold text-sm">Etiquetas</h4>
              <div class="mt-2 flex flex-wrap gap-2 text-xs">
                <span v-for="tag in selectedRecipe.tags" :key="tag" class="px-2 py-1 bg-neutral-100 border rounded">{{ tag }}</span>
              </div>
            </div>
          </div>
  
          <!-- Columna derecha: video vertical -->
          <div class="p-4 md:border-l overflow-y-auto">
            <div class="w-full h-[70vh] border rounded-md bg-neutral-50">
              <iframe v-if="currentVideoUrl" :src="currentVideoUrl" class="w-full h-full" frameborder="0" allow="autoplay; encrypted-media; picture-in-picture" allowfullscreen></iframe>
              <div v-else class="w-full h-full flex items-center justify-center text-center p-4">
                <p class="text-sm text-neutral-600">No se pudo cargar el video. <a :href="selectedRecipe?.video?.url" target="_blank" class="underline text-[#B13704]">Abrir en TikTok</a></p>
              </div>
            </div>
          </div>
        </div>
  
        <!-- Footer del modal 
        <div class="p-4 border-t flex justify-end gap-2">
          <button class="px-3 py-2 rounded-md bg-[#6c9328] text-white text-sm" @click="closeRecipe">Cerrar</button>
        </div>
         -->
      </div>
    </div>
  </div>

  <div v-if="showProduct" class="fixed inset-0 bg-black/60 flex items-center justify-center p-4" @click.self="closeProductModal">
    <div class="max-w-xl w-full bg-white rounded-md overflow-hidden">
      <div class="p-4 border-b">
        <h3 class="font-semibold">Detalle del producto</h3>
      </div>
      <div class="p-4 space-y-3">
        <p class="text-neutral-700">{{ selectedProduct.description }}</p>
        <p class="text-neutral-700">Artesano: {{ selectedProduct.artisan }}</p>
        <div class="border rounded-md p-4 bg-neutral-50">
          <h4 class="font-semibold">Formulario de contacto</h4>
          <form @submit.prevent="submitClaim" class="mt-2 grid gap-3">
            <input type="text" placeholder="Nombre" class="border rounded-md p-2" required />
            <input type="email" placeholder="Correo" class="border rounded-md p-2" required />
            <textarea placeholder="Mensaje" class="border rounded-md p-2" rows="3" required></textarea>
            <button type="submit" class="px-3 py-2 rounded-md bg-[#B13704] text-white text-sm font-semibold">Enviar</button>
          </form>
        </div>
      </div>
      <!--
      -->
      <div class="p-4 border-t flex justify-end">
        <button class="px-3 py-2 rounded-md bg-[#6c9328] text-white text-sm" @click="closeProductModal">Cerrar</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch, onUnmounted } from 'vue'

// Recetas
const showRecipe = ref(false)
const selectedRecipe = ref<any>(null)

const recipes = ref([
  {
    id: 'ceviche',
    title: 'Ceviche clásico',
    subtitle: 'Mar y frescura en cada bocado',
    region: 'Costa',
    difficulty: 'Media',
    time: '25 min',
    servings: 4,
    calories: 320,
    tags: ['Pescado', 'Limón', 'Ají', 'Cebolla'],
    utensils: ['Bowl de vidrio', 'Cuchillo bien afilado', 'Tabla', 'Colador'],
    allergens: ['Pescado'],
    pairings: ['Camote', 'Choclo', 'Cancha', 'Chicha morada'],
    ingredients: 'Pescado, limón, ají limo, cebolla morada, sal, cilantro',
    description: 'Icono de la cocina peruana con toques cítricos y picantes.',
    origin: 'Platillo emblemático de la costa peruana. Su frescura y acidez reflejan el carácter del mar y la identidad culinaria local.',
    notes: 'Usa pescado muy fresco, cítricos recién exprimidos y evita sobrecurtir para mantener textura firme.',
    steps: [
      'Cortar el pescado en cubos de 1–2 cm y mantenerlo frío.',
      'Sazonar con sal y mezclar suavemente.',
      'Agregar jugo de limón recién exprimido y dejar curtir 5–10 minutos.',
      'Añadir ají limo picado y cebolla morada en pluma.',
      'Probar y ajustar sal/acidez si fuera necesario.',
      'Servir con camote, choclo y cancha.'
    ],
    video: { provider: 'tiktok', videoId: '6718335390845095173', url: 'https://www.tiktok.com/@scout2015/video/6718335390845095173' }
  },
  {
    id: 'lomo',
    title: 'Lomo saltado',
    subtitle: 'Salteado criollo con papas doradas',
    region: 'Lima',
    difficulty: 'Media',
    time: '40 min',
    servings: 3,
    calories: 650,
    tags: ['Res', 'Soya', 'Papas', 'Cebolla'],
    utensils: ['Wok o sartén grande', 'Espátula', 'Cuchillo', 'Tabla'],
    allergens: ['Soya', 'Gluten'],
    pairings: ['Arroz blanco', 'Papas fritas', 'Cerveza ligera'],
    ingredients: 'Lomo de res, cebolla, tomate, salsa de soya, vinagre, papas',
    description: 'Tradición criolla con técnica salteada y sabor intenso.',
    origin: 'Fusión peruano-china (chifa). Salteado a fuego alto con técnica y sazón que reflejan la influencia nikkei y china.',
    notes: 'Sella la carne a fuego alto y evita sobrecocinar las verduras. Integra el wok con movimiento constante.',
    steps: [
      'Cortar el lomo en tiras y sazonar ligeramente.',
      'Sellar la carne muy caliente por tandas para lograr dorado.',
      'Retirar la carne y saltear cebolla y tomate a fuego alto.',
      'Desglasar con un toque de vinagre y salsa de soya.',
      'Reincorporar la carne con el jugo que soltó y mezclar.',
      'Servir acompañado de arroz blanco y papas fritas.'
    ],
    video: { provider: 'tiktok', videoId: '6948210747285441798', url: 'https://www.tiktok.com/@scout2015/video/6948210747285441798' }
  },
  {
    id: 'aji',
    title: 'Ají de gallina',
    subtitle: 'Cremoso y picantito',
    region: 'Sierra',
    difficulty: 'Media',
    time: '35 min',
    servings: 4,
    calories: 500,
    tags: ['Gallina', 'Ají amarillo', 'Pan', 'Leche'],
    utensils: ['Olla', 'Licuadora', 'Cucharón'],
    allergens: ['Lácteos', 'Gluten', 'Nueces'],
    pairings: ['Arroz blanco', 'Papas sancochadas', 'Aceitunas negras', 'Huevo duro'],
    ingredients: 'Pechuga deshilachada, ají amarillo, pan remojado, leche, nueces',
    description: 'Clásico reconfortante con textura cremosa y ají amarillo.',
    origin: 'Receta tradicional con raíces limeñas y coloniales, muy presente en hogares y fondas del Perú.',
    notes: 'Busca una textura cremosa y homogénea; ajusta el picante al gusto y controla el espesor con leche o caldo.',
    steps: [
      'Sancochar la pechuga y deshilachar finamente.',
      'Remojar pan en leche y licuar con ají amarillo.',
      'Sudar cebolla con ajo, añadir la crema y llevar a hervor suave.',
      'Agregar la gallina deshilachada y mezclar hasta textura cremosa.',
      'Rectificar sal y servir con arroz, papas, aceitunas y huevo.'
    ],
    video: { provider: 'tiktok', videoId: '6749520869598481669', url: 'https://www.tiktok.com/@zachking/video/6749520869598481669' }
  }
])

function openRecipe(recipe: any) {
  selectedRecipe.value = recipe
  showRecipe.value = true
}
function closeRecipe() { showRecipe.value = false }

function getSelectedIndex() {
  return recipes.value.findIndex((r: any) => r?.id === selectedRecipe.value?.id)
}
function goToPrevRecipe() {
  const idx = getSelectedIndex()
  if (idx < 0) return
  const nextIdx = (idx - 1 + recipes.value.length) % recipes.value.length
  selectedRecipe.value = recipes.value[nextIdx]
}
function goToNextRecipe() {
  const idx = getSelectedIndex()
  if (idx < 0) return
  const nextIdx = (idx + 1) % recipes.value.length
  selectedRecipe.value = recipes.value[nextIdx]
}

const onKeyDown = (e: KeyboardEvent) => {
  if (!showRecipe.value) return
  if (e.key === 'Escape') { e.preventDefault(); closeRecipe() }
  else if (e.key === 'ArrowRight') { e.preventDefault(); goToNextRecipe() }
  else if (e.key === 'ArrowLeft') { e.preventDefault(); goToPrevRecipe() }
}

const currentVideoUrl = computed(() => {
  const v = selectedRecipe.value?.video
  if (!v) return ''
  if (v.provider === 'tiktok' && v.videoId) return `https://www.tiktok.com/embed/v3/${v.videoId}`
  if (v.provider === 'url' && v.url) return v.url
  if (v.provider === 'youtube' && v.videoId) return `https://www.youtube.com/embed/${v.videoId}`
  return ''
})

const ingredientList = computed(() => {
  const raw = selectedRecipe.value?.ingredients || ''
  return raw.split(',').map((i: string) => i.trim()).filter(Boolean)
})

// Control del slider: referencia y aceleración sostenida/ráfaga con reinicio fiable
const marqueeRef = ref<HTMLElement | null>(null)
let speedResetTimer: number | null = null
const holdingAccel = ref(false)

function applyMarquee(durationSeconds: number, direction: 'normal' | 'reverse') {
  const el = marqueeRef.value
  if (!el) return
  el.style.setProperty('--marquee-duration', `${durationSeconds}s`)
  el.style.setProperty('--marquee-direction', direction)
  el.style.animationPlayState = 'running'
}
function restartMarquee() {
  const el = marqueeRef.value
  if (!el) return
  el.classList.remove('marquee')
  void el.offsetWidth
  el.classList.add('marquee')
}
function startHold(dir: 'forward' | 'backward') {
  holdingAccel.value = true
  if (speedResetTimer) { window.clearTimeout(speedResetTimer); speedResetTimer = null }
  applyMarquee(6, dir === 'forward' ? 'normal' : 'reverse')
  restartMarquee()
}
function stopHold() {
  holdingAccel.value = false
  if (speedResetTimer) { window.clearTimeout(speedResetTimer); speedResetTimer = null }
  applyMarquee(22, 'normal')
  restartMarquee()
}
function speedBurst(dir: 'forward' | 'backward') {
  if (holdingAccel.value) return
  applyMarquee(8, dir === 'forward' ? 'normal' : 'reverse')
  restartMarquee()
  if (speedResetTimer) window.clearTimeout(speedResetTimer)
  speedResetTimer = window.setTimeout(() => {
    applyMarquee(22, 'normal')
    restartMarquee()
  }, 3000)
}

// Artesanos (sin cambios)
const showProduct = ref(false)
const selectedProduct = ref({ description: 'Caja de ingredientes premium', artisan: 'Colectivo Gastronómico' })
const exampleProduct = selectedProduct.value

function openProductModal(product: any) {
  selectedProduct.value = product
  showProduct.value = true
}
function closeProductModal() { showProduct.value = false }

function submitClaim() {
  alert('Solicitud enviada. Nos contactaremos pronto.')
}

// Bloquear scroll de la página cuando el modal está abierto
watch(showRecipe, (val) => {
  if (typeof document !== 'undefined') {
    document.documentElement.classList.toggle('overflow-hidden', val)
    document.body.classList.toggle('overflow-hidden', val)
  }
  if (typeof window !== 'undefined') {
    if (val) window.addEventListener('keydown', onKeyDown)
    else window.removeEventListener('keydown', onKeyDown)
  }
})

onUnmounted(() => {
  if (typeof window !== 'undefined') window.removeEventListener('keydown', onKeyDown)
})
</script>

<style>
/* Animación existente */
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
/* Animaciones y helpers para slider infinito */
.marquee { animation: marquee var(--marquee-duration, 22s) linear infinite; animation-direction: var(--marquee-direction, normal); }

@media (prefers-reduced-motion: reduce) { .marquee { animation: none; } }

/* Hero background & stars overlay - enhanced */
.hero-bg { background:
  radial-gradient(1200px 600px at 0% -10%, rgba(254,197,61,.12), transparent 60%),
  radial-gradient(800px 500px at 100% 0%, rgba(108,147,40,.10), transparent 65%),
  linear-gradient(to bottom, #ffffff, #fffdf5 50%, #faf7f0);
}
.hero-bg::after {
  content:""; position:absolute; inset:auto auto -40% -20%;
  width: 1200px; height: 1200px; pointer-events:none;
  background: radial-gradient(closest-side, rgba(254,197,61,.25), transparent 60%);
  filter: blur(24px); opacity:.35; transform: translate3d(0,0,0);
  animation: floaty 18s ease-in-out infinite;
}
@keyframes floaty { 0%,100% { transform: translateY(0) } 50% { transform: translateY(-10px) } }

@keyframes twinkle { 0%,100% { opacity:.14 } 50% { opacity:.22 } }
.stars-overlay { position:absolute; inset:0; pointer-events:none;
  background-image: radial-gradient(rgba(43,43,43,0.18) 1px, transparent 1px);
  background-size: 22px 22px; opacity:.18; animation: twinkle 6s ease-in-out infinite;
  filter: contrast(105%) saturate(104%);
}

/* Encabezados decorativos tipo referencia */
.section-heading {
  position: relative; display: inline-flex; align-items: center; gap: .75rem;
  padding: .25rem .75rem; text-transform: none; letter-spacing: .01em;
}
.section-heading::before, .section-heading::after {
  content: ""; display: block; width: 72px; height: 2px;
  background: linear-gradient(to right, transparent, #B13704 50%, transparent);
  border-radius: 9999px; opacity: .4;
}
@media (min-width: 768px) { .section-heading::before, .section-heading::after { width: 96px; } }

/* Tarjetas/secciones con borde y sombra de marca */
.section-card {
  background: linear-gradient(180deg, #ffffff 0%, #fffaf4 100%);
  border: 2px solid #2b2b2b; border-radius: 18px;
  box-shadow: 8px 8px 0 0 #B13704; padding: 1rem;
}

/* Flechas del carrusel como botones redondos */
.carousel-arrow {
  width: 40px; height: 40px; border-radius: 9999px;
  border: 2px solid #2b2b2b; background: rgba(255,255,255,.95);
  box-shadow: 4px 4px 0 0 #B13704; transition: transform .15s, box-shadow .15s, background-color .15s;
}
.carousel-arrow:hover { transform: translateY(-1px); box-shadow: 2px 2px 0 0 #B13704; }

/* Hero title gradient */
#hero h1 {
  background: linear-gradient(90deg, var(--ink) 0%, var(--brand-red) 60%, var(--ink) 100%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}

/* CTA polish */
#cta a { border: 2px solid var(--ink); box-shadow: 4px 4px 0 0 var(--brand-red); transition: transform .15s, box-shadow .15s; }
#cta a:hover { transform: translateY(-1px); box-shadow: 2px 2px 0 0 var(--brand-red); }
#cta a:active { transform: translateY(0); }

/* Cards hover polish */
.section-card { transition: transform .2s, box-shadow .2s; }
.section-card:hover { transform: translateY(-2px); box-shadow: 6px 6px 0 0 var(--brand-red); }

/* Accessibility */
.carousel-arrow:focus-visible { outline: 2px solid var(--brand-green); outline-offset: 2px; }

/* Recipe cards subtle lift */
#recetas article:hover { transform: translateY(-2px); }
</style>
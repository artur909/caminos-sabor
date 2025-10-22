<template>
  <div class="min-h-screen flex flex-col bg-white text-neutral-900">
    <!-- Header -->
    <header class="sticky top-0 z-40 bg-white/90 backdrop-blur border-b border-neutral-200">
      <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-6 lg:px-8 py-3 flex items-center justify-between">
        <a href="#hero" class="flex items-center gap-2 font-semibold">
          <span class="inline-block w-6 h-6 bg-[#B13704] border-2 border-[#2b2b2b] shadow-[3px_3px_0_0_#fec53d]"></span>
          <span>Caminos & Sabor</span>
        </a>
        <nav class="hidden md:flex items-center gap-6 text-sm">
          <a href="#hero" class="px-2 py-1 rounded-none border-b-2 border-transparent hover:border-[#B13704] hover:text-[#B13704]">Inicio</a>
          <a href="#descripcion" class="px-2 py-1 rounded-none border-b-2 border-transparent hover:border-[#B13704] hover:text-[#B13704]">Descripción</a>
          <a href="#recetas" class="px-2 py-1 rounded-none border-b-2 border-transparent hover:border-[#B13704] hover:text-[#B13704]">Recetas</a>
          <a href="#artesanos" class="px-2 py-1 rounded-none border-b-2 border-transparent hover:border-[#B13704] hover:text-[#B13704]">Artesanos</a>
          <a href="#aliados" class="px-2 py-1 rounded-none border-b-2 border-transparent hover:border-[#B13704] hover:text-[#B13704]">Aliados</a>
        </nav>
        <a href="#cta" class="inline-flex items-center px-4 py-2 rounded-none border-2 border-[#2b2b2b] bg-[#fec53d] text-[#2b2b2b] font-bold shadow-[4px_4px_0_0_#B13704] hover:shadow-[2px_2px_0_0_#B13704] active:translate-y-px">
          Jugar ahora
        </a>
      </div>
    </header>

    <!-- Main content -->
    <main class="flex-1">
      <slot />
    </main>

    <!-- Footer -->
    <footer class="border-t border-neutral-200">
      <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-6 lg:px-8 py-8 grid md:grid-cols-3 gap-6">
        <div>
          <h3 class="font-semibold">Los Caminos del Sabor</h3>
          <p class="mt-2 text-sm text-neutral-600">Videojuego que revaloriza la gastronomía peruana.</p>
        </div>
        <div>
          <h3 class="font-semibold">Navegación</h3>
          <ul class="mt-2 text-sm text-neutral-600 space-y-2">
            <li><a href="#descripcion" class="hover:text-[#B13704]">Descripción</a></li>
            <li><a href="#recetas" class="hover:text-[#B13704]">Recetas</a></li>
            <li><a href="#artesanos" class="hover:text-[#B13704]">Artesanos</a></li>
            <li><a href="#aliados" class="hover:text-[#B13704]">Aliados</a></li>
          </ul>
        </div>
        <div>
          <h3 class="font-semibold">Contacto</h3>
          <p class="mt-2 text-sm text-neutral-600">¿Tienes preguntas? Escríbenos para colaborar o apoyar el proyecto.</p>
          <a href="#contacto" class="mt-3 inline-flex items-center px-3 py-2 rounded-md bg-[#6c9328] text-white text-sm font-semibold hover:opacity-90">Contacto</a>
        </div>
      </div>
      <div class="bg-neutral-50 text-neutral-500 text-xs py-4">
        <div class="mx-auto w-full max-w-[min(100vw,1600px)] px-6 lg:px-8">© 2025 IMB Institute</div>
      </div>
    </footer>
  </div>
</template>
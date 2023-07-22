<script setup>
import { ref } from "vue";
const images = [
  {
    id: 1,
    label: "1st Image",
    image:
      "https://images.unsplash.com/photo-1500964757637-c85e8a162699?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8b2NlYW4lMjBsYW5kc2NhcGV8ZW58MHx8MHx8fDA%3D&w=1000&q=80",
  },
  {
    id: 2,
    label: "2nd Image",
    image:
      "https://helpx.adobe.com/content/dam/help/en/photoshop/using/convert-color-image-black-white/jcr_content/main-pars/before_and_after/image-before/Landscape-Color.jpg",
  },
  {
    id: 3,
    label: "3rd Image",
    image:
      "https://d150u0abw3r906.cloudfront.net/wp-content/uploads/2021/10/image2-2-1024x649.png",
  },
];

let currentImage = ref({
  id: 1,
  label: "1st Image",
  image:
    "https://images.unsplash.com/photo-1500964757637-c85e8a162699?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8b2NlYW4lMjBsYW5kc2NhcGV8ZW58MHx8MHx8fDA%3D&w=1000&q=80",
});
let currentIndex = 0;
const changeImage = (navigation) => {
  if (navigation === "next") {
    currentIndex = (currentIndex + 1) % images.length;
  }
  if (navigation === "previous") {
    currentIndex = (currentIndex - 1 + images.length) % images.length;
  }
  // Update the currentIndex to the next image index

  currentImage.value = images[currentIndex]; // Update the currentImage using the new currentIndex
};
</script>

<template>
  <div
    id="carouselExampleCaptions"
    class="relative"
    data-te-carousel-init
    data-te-carousel-slide
    style="max-width: 900px; min-width: 900px"
  >
    <!--Carousel indicators-->
    <div
      class="absolute bottom-0 left-0 right-0 z-[2] mx-[15%] mb-4 flex list-none justify-center p-0"
      data-te-carousel-indicators
    >
      <button
        v-for="image in images"
        type="button"
        data-te-target="#carouselExampleCaptions"
        data-te-slide-to="0"
        data-te-carousel-active
        class="mx-[3px] box-content h-[3px] w-[30px] flex-initial cursor-pointer border-0 border-y-[10px] border-solid border-transparent bg-clip-padding p-0 -indent-[999px] transition-opacity duration-[600ms] ease-[cubic-bezier(0.25,0.1,0.25,1.0)] motion-reduce:transition-none"
        aria-current="true"
        :class="currentImage.id === image.id ? 'bg-blue-500' : 'bg-red-500'"
        aria-label="Slide 1"
        @click="currentImage = image"
      ></button>
    </div>

    <!--Carousel items-->
    <div
      class="relative w-full overflow-hidden after:clear-both after:block after:content-['']"
    >
      <div
        class="relative float-left -mr-[100%] w-full transition-transform duration-[600ms] ease-in-out motion-reduce:transition-none"
        data-te-carousel-active
        data-te-carousel-item
        style="backface-visibility: hidden"
      >
        <img
          :src="currentImage.image"
          class="block w-900 h-600"
          alt="..."
          style="overflow: hidden; aspect-ratio: 16/9; object-fit: cover"
        />
        <div
          class="absolute inset-x-[15%] bottom-5 hidden py-5 text-center text-white md:block"
        >
          <h5 class="text-xl">{{ currentImage.label }}</h5>
          <p>Some representative placeholder content for the first slide.</p>
        </div>
      </div>
    </div>

    <!--Carousel controls - prev item-->
    <button
      class="absolute bottom-0 left-0 top-0 z-[1] flex w-[15%] items-center justify-center border-0 bg-none p-0 text-center text-white opacity-50 transition-opacity duration-150 ease-[cubic-bezier(0.25,0.1,0.25,1.0)] hover:text-white hover:no-underline hover:opacity-90 hover:outline-none focus:text-white focus:no-underline focus:opacity-90 focus:outline-none motion-reduce:transition-none"
      type="button"
      data-te-target="#carouselExampleCaptions"
      data-te-slide="prev"
      @click="changeImage('previous')"
    >
      <span class="inline-block h-8 w-8">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="h-6 w-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15.75 19.5L8.25 12l7.5-7.5"
          />
        </svg>
      </span>
      <span
        class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]"
        >Previous</span
      >
    </button>
    <!--Carousel controls - next item-->
    <button
      class="absolute bottom-0 right-0 top-0 z-[1] flex w-[15%] items-center justify-center border-0 bg-none p-0 text-center text-white opacity-50 transition-opacity duration-150 ease-[cubic-bezier(0.25,0.1,0.25,1.0)] hover:text-white hover:no-underline hover:opacity-90 hover:outline-none focus:text-white focus:no-underline focus:opacity-90 focus:outline-none motion-reduce:transition-none"
      type="button"
      data-te-target="#carouselExampleCaptions"
      data-te-slide="next"
      @click="changeImage('next')"
    >
      <span class="inline-block h-8 w-8">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="h-6 w-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M8.25 4.5l7.5 7.5-7.5 7.5"
          />
        </svg>
      </span>
      <span
        class="!absolute !-m-px !h-px !w-px !overflow-hidden !whitespace-nowrap !border-0 !p-0 ![clip:rect(0,0,0,0)]"
        >Next</span
      >
    </button>
  </div>
</template>

<style scoped></style>

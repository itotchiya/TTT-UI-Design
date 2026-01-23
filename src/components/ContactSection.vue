<template>
  <section id="contact" class="scroll-mt-20 py-12 md:py-16">
    <div class="mx-auto max-w-6xl px-6">
      <div class="grid gap-16 md:items-start">
        <!-- Right: Form -->
        <div class="bg-white p-8 shadow-2xl md:p-12 mx-auto w-full max-w-3xl">
          <div class="text-center mb-10">
            <h2 class="text-2xl md:text-4xl font-bold tracking-tight text-[#0C2340] uppercase">{{ $t('contact.title') }}</h2>
            <div class="mt-6 w-12 h-1 bg-[#968243] mx-auto opacity-30"></div>
          </div>

          <form class="space-y-6" @submit.prevent="handleSubmit">
            <!-- Contact Info -->
            <div class="grid gap-4 sm:grid-cols-2">
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">{{ $t('contact.form.firstName') }}</label>
                <input
                  v-model.trim="form.firstName"
                  class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  :placeholder="$t('contact.form.firstNamePlaceholder')"
                />
              </div>
              <div>
                <label class="mb-1.5 block text-sm font-medium text-slate-700">{{ $t('contact.form.lastName') }}</label>
                <input
                  v-model.trim="form.lastName"
                  class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                  :placeholder="$t('contact.form.lastNamePlaceholder')"
                />
              </div>
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">{{ $t('contact.form.email') }}</label>
              <input
                v-model.trim="form.email"
                type="email"
                class="w-full border border-slate-200 px-4 py-3 text-sm outline-none transition focus:border-slate-400 focus:ring-2 focus:ring-slate-100"
                :placeholder="$t('contact.form.emailPlaceholder')"
              />
            </div>

            <div>
              <label class="mb-1.5 block text-sm font-medium text-slate-700">{{ $t('contact.form.phone') }}</label>
              <div class="flex items-center rounded-lg shadow-sm">
                <div class="relative">
                  <button 
                    type="button" 
                    class="inline-flex items-center shrink-0 z-10 text-slate-700 bg-slate-50 border border-slate-200 hover:bg-slate-100 focus:ring-4 focus:ring-slate-100 font-medium rounded-s-lg text-sm px-4 py-3 focus:outline-none transition-colors"
                    @click="dropdownOpen = !dropdownOpen"
                  >
                    <template v-if="selectedCountry">
                      <img v-if="selectedCountry.type === 'img'" :src="selectedCountry.src" class="w-4 h-4 me-2 object-cover rounded-sm" />
                      <svg v-else-if="selectedCountry.id === 'us'" class="w-4 h-4 me-2" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M8.00013 14.6666C11.6821 14.6666 14.667 11.6818 14.667 7.99992C14.667 4.31802 11.6821 1.33325 8.00013 1.33325C4.31811 1.33325 1.33325 4.31802 1.33325 7.99992C1.33325 11.6818 4.31811 14.6666 8.00013 14.6666Z" fill="white"/><path d="M7.71167 7.99975H14.6678C14.6678 7.39807 14.5876 6.8152 14.4382 6.26074H7.71167V7.99975Z" fill="#D80027"/><path d="M7.71167 4.52172H13.6894C13.2813 3.85583 12.7596 3.26726 12.1512 2.78271H7.71167V4.52172Z" fill="#D80027"/><path d="M8.00053 14.6667C9.56944 14.6667 11.0115 14.1244 12.1502 13.2175H3.85083C4.98958 14.1244 6.43162 14.6667 8.00053 14.6667Z" fill="#D80027"/><path d="M2.31233 11.4784H13.689C14.0167 10.9438 14.2708 10.3594 14.4379 9.73926H1.56348C1.73059 10.3594 1.98469 10.9438 2.31233 11.4784V11.4784Z" fill="#D80027"/><path d="M4.42123 2.37426H5.02873L4.46365 2.78478L4.6795 3.44902L4.11445 3.03851L3.5494 3.44902L3.73584 2.87519C3.23832 3.28961 2.80224 3.77514 2.44289 4.31614H2.63754L2.27784 4.57745C2.2218 4.67093 2.16806 4.7659 2.11655 4.86227L2.28831 5.3909L1.96786 5.15808C1.8882 5.32684 1.81534 5.49941 1.74985 5.67557L1.93908 6.25802H2.63754L2.07246 6.66853L2.28831 7.33278L1.72326 6.92226L1.38479 7.16818C1.35091 7.4405 1.33325 7.71788 1.33325 7.99939H7.9996C7.9996 4.31781 7.9996 3.88378 7.9996 1.33325C6.68268 1.33325 5.45506 1.71525 4.42123 2.37426V2.37426ZM4.6795 7.33278L4.11445 6.92226L3.5494 7.33278L3.76524 6.66853L3.20017 6.25802H3.89862L4.11445 5.59377L4.33027 6.25802H5.02873L4.46365 6.66853L4.6795 7.33278ZM4.46365 4.72666L4.6795 5.3909L4.11445 4.98039L3.5494 5.3909L3.76524 4.72666L3.20017 4.31614H3.89862L4.11445 3.6519L4.33027 4.31614H5.02873L4.46365 4.72666ZM7.07068 7.33278L6.50563 6.92226L5.94058 7.33278L6.15643 6.66853L5.59135 6.25802H6.28981L6.50563 5.59377L6.72146 6.25802H7.41991L6.85484 6.66853L7.07068 7.33278ZM6.85484 4.72666L7.07068 5.3909L6.50563 4.98039L5.94058 5.3909L6.15643 4.72666L5.59135 4.31614H6.28981L6.50563 3.6519L6.72146 4.31614H7.41991L6.85484 4.72666ZM6.85484 2.78478L7.07068 3.44902L6.50563 3.03851L5.94058 3.44902L6.15643 2.78478L5.59135 2.37426H6.28981L6.50563 1.71002L6.72146 2.37426H7.41991L6.85484 2.78478Z" fill="#1A47B8"/></svg>
                      <svg v-else-if="selectedCountry.id === 'uk'" class="w-4 h-4 me-2" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M9 16.5C13.1421 16.5 16.5 13.1421 16.5 9C16.5 4.85786 13.1421 1.5 9 1.5C4.85786 1.5 1.5 4.85786 1.5 9C1.5 13.1421 4.85786 16.5 9 16.5Z" fill="white"/><path d="M3.05081 4.43384C2.46168 5.20033 2.01745 6.08378 1.75879 7.04352H5.66049L3.05081 4.43384Z" fill="#1A47B8"/><path d="M16.2415 7.04349C15.9828 6.08378 15.5386 5.20033 14.9495 4.43384L12.3398 7.04349H16.2415Z" fill="#1A47B8"/><path d="M1.75879 10.9567C2.01748 11.9164 2.46171 12.7998 3.05081 13.5663L5.6604 10.9567H1.75879Z" fill="#1A47B8"/><path d="M13.5677 3.05047C12.8012 2.46134 11.9178 2.01711 10.9581 1.75842V5.66009L13.5677 3.05047Z" fill="#1A47B8"/><path d="M4.43457 14.9497C5.20106 15.5388 6.08451 15.983 7.04422 16.2417V12.3401L4.43457 14.9497Z" fill="#1A47B8"/><path d="M7.04419 1.75842C6.08448 2.01711 5.20104 2.46134 4.43457 3.05044L7.04419 5.66006V1.75842Z" fill="#1A47B8"/><path d="M10.9581 16.2417C11.9178 15.983 12.8012 15.5388 13.5677 14.9497L10.9581 12.3401V16.2417Z" fill="#1A47B8"/><path d="M12.3398 10.9568L14.9495 13.5664C15.5386 12.8 15.9828 11.9165 16.2415 10.9568H12.3398Z" fill="#1A47B8"/><path d="M16.4365 8.02175H9.97831H9.97828V1.56349C9.65804 1.5218 9.33155 1.5 9 1.5C8.66839 1.5 8.34196 1.5218 8.02175 1.56349V8.02169V8.02172H1.56349C1.5218 8.34196 1.5 8.66845 1.5 9C1.5 9.33161 1.5218 9.65804 1.56349 9.97825H8.02169H8.02172V16.4365C8.34196 16.4782 8.66839 16.5 9 16.5C9.33155 16.5 9.65804 16.4782 9.97825 16.4365V9.97831V9.97828H16.4365C16.4782 9.65804 16.5 9.33161 16.5 9C16.5 8.66845 16.4782 8.34196 16.4365 8.02175Z" fill="#D80027"/><path d="M10.9556 10.9566L14.3023 14.3033C14.4563 14.1495 14.6031 13.9886 14.7432 13.8218L11.8779 10.9565H10.9556V10.9566Z" fill="#D80027"/><path d="M7.04405 10.9565H7.04399L3.69727 14.3033C3.85113 14.4572 4.012 14.604 4.17876 14.7441L7.04405 11.8788V10.9565Z" fill="#D80027"/><path d="M7.04299 7.0435V7.04344L3.69623 3.69666C3.5423 3.85052 3.39547 4.01139 3.25537 4.17815L6.12069 7.04347H7.04299V7.0435Z" fill="#D80027"/><path d="M10.9556 7.04363L14.3024 3.69681C14.1485 3.54289 13.9876 3.39605 13.8209 3.25598L10.9556 6.1213V7.04363Z" fill="#D80027"/></svg>
                      <svg v-else-if="selectedCountry.id === 'ch'" class="w-4 h-4 me-2" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg"><rect fill="#d80027" width="32" height="32"/><path fill="#fff" d="M13 6h6v7h7v6h-7v7h-6v-7H6v-6h7z"/></svg>
                      {{ selectedCountry.code }}
                    </template>
                    <svg class="w-2.5 h-2.5 ms-2.5 text-slate-500" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 10 6">
                      <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 4 4 4-4"/>
                    </svg>
                  </button>
                  
                  <!-- Dropdown -->
                  <div v-show="dropdownOpen" class="absolute start-0 top-full mt-1 z-20 w-52 bg-white divide-y divide-slate-100 rounded-lg shadow-xl border border-slate-100 max-h-60 overflow-y-auto">
                    <ul class="py-2 text-sm text-slate-700">
                      <li v-for="country in countryCodes" :key="country.code">
                        <button 
                          type="button" 
                          class="inline-flex w-full px-4 py-2 hover:bg-slate-100 text-left items-center gap-3"
                          @click="selectCountry(country)"
                        >
                          <img v-if="country.type === 'img'" :src="country.src" class="w-4 h-4 object-cover rounded-sm" />
                          <svg v-else-if="country.id === 'us'" class="w-4 h-4" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M8.00013 14.6666C11.6821 14.6666 14.667 11.6818 14.667 7.99992C14.667 4.31802 11.6821 1.33325 8.00013 1.33325C4.31811 1.33325 1.33325 4.31802 1.33325 7.99992C1.33325 11.6818 4.31811 14.6666 8.00013 14.6666Z" fill="white"/><path d="M7.71167 7.99975H14.6678C14.6678 7.39807 14.5876 6.8152 14.4382 6.26074H7.71167V7.99975Z" fill="#D80027"/><path d="M7.71167 4.52172H13.6894C13.2813 3.85583 12.7596 3.26726 12.1512 2.78271H7.71167V4.52172Z" fill="#D80027"/><path d="M8.00053 14.6667C9.56944 14.6667 11.0115 14.1244 12.1502 13.2175H3.85083C4.98958 14.1244 6.43162 14.6667 8.00053 14.6667Z" fill="#D80027"/><path d="M2.31233 11.4784H13.689C14.0167 10.9438 14.2708 10.3594 14.4379 9.73926H1.56348C1.73059 10.3594 1.98469 10.9438 2.31233 11.4784V11.4784Z" fill="#D80027"/><path d="M4.42123 2.37426H5.02873L4.46365 2.78478L4.6795 3.44902L4.11445 3.03851L3.5494 3.44902L3.73584 2.87519C3.23832 3.28961 2.80224 3.77514 2.44289 4.31614H2.63754L2.27784 4.57745C2.2218 4.67093 2.16806 4.7659 2.11655 4.86227L2.28831 5.3909L1.96786 5.15808C1.8882 5.32684 1.81534 5.49941 1.74985 5.67557L1.93908 6.25802H2.63754L2.07246 6.66853L2.28831 7.33278L1.72326 6.92226L1.38479 7.16818C1.35091 7.4405 1.33325 7.71788 1.33325 7.99939H7.9996C7.9996 4.31781 7.9996 3.88378 7.9996 1.33325C6.68268 1.33325 5.45506 1.71525 4.42123 2.37426V2.37426ZM4.6795 7.33278L4.11445 6.92226L3.5494 7.33278L3.76524 6.66853L3.20017 6.25802H3.89862L4.11445 5.59377L4.33027 6.25802H5.02873L4.46365 6.66853L4.6795 7.33278ZM4.46365 4.72666L4.6795 5.3909L4.11445 4.98039L3.5494 5.3909L3.76524 4.72666L3.20017 4.31614H3.89862L4.11445 3.6519L4.33027 4.31614H5.02873L4.46365 4.72666ZM7.07068 7.33278L6.50563 6.92226L5.94058 7.33278L6.15643 6.66853L5.59135 6.25802H6.28981L6.50563 5.59377L6.72146 6.25802H7.41991L6.85484 6.66853L7.07068 7.33278ZM6.85484 4.72666L7.07068 5.3909L6.50563 4.98039L5.94058 5.3909L6.15643 4.72666L5.59135 4.31614H6.28981L6.50563 3.6519L6.72146 4.31614H7.41991L6.85484 4.72666ZM6.85484 2.78478L7.07068 3.44902L6.50563 3.03851L5.94058 3.44902L6.15643 2.78478L5.59135 2.37426H6.28981L6.50563 1.71002L6.72146 2.37426H7.41991L6.85484 2.78478Z" fill="#1A47B8"/></svg>
                          <svg v-else-if="country.id === 'uk'" class="w-4 h-4" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M9 16.5C13.1421 16.5 16.5 13.1421 16.5 9C16.5 4.85786 13.1421 1.5 9 1.5C4.85786 1.5 1.5 4.85786 1.5 9C1.5 13.1421 4.85786 16.5 9 16.5Z" fill="white"/><path d="M3.05081 4.43384C2.46168 5.20033 2.01745 6.08378 1.75879 7.04352H5.66049L3.05081 4.43384Z" fill="#1A47B8"/><path d="M16.2415 7.04349C15.9828 6.08378 15.5386 5.20033 14.9495 4.43384L12.3398 7.04349H16.2415Z" fill="#1A47B8"/><path d="M1.75879 10.9567C2.01748 11.9164 2.46171 12.7998 3.05081 13.5663L5.6604 10.9567H1.75879Z" fill="#1A47B8"/><path d="M13.5677 3.05047C12.8012 2.46134 11.9178 2.01711 10.9581 1.75842V5.66009L13.5677 3.05047Z" fill="#1A47B8"/><path d="M4.43457 14.9497C5.20106 15.5388 6.08451 15.983 7.04422 16.2417V12.3401L4.43457 14.9497Z" fill="#1A47B8"/><path d="M7.04419 1.75842C6.08448 2.01711 5.20104 2.46134 4.43457 3.05044L7.04419 5.66006V1.75842Z" fill="#1A47B8"/><path d="M10.9581 16.2417C11.9178 15.983 12.8012 15.5388 13.5677 14.9497L10.9581 12.3401V16.2417Z" fill="#1A47B8"/><path d="M12.3398 10.9568L14.9495 13.5664C15.5386 12.8 15.9828 11.9165 16.2415 10.9568H12.3398Z" fill="#1A47B8"/><path d="M16.4365 8.02175H9.97831H9.97828V1.56349C9.65804 1.5218 9.33155 1.5 9 1.5C8.66839 1.5 8.34196 1.5218 8.02175 1.56349V8.02169V8.02172H1.56349C1.5218 8.34196 1.5 8.66845 1.5 9C1.5 9.33161 1.5218 9.65804 1.56349 9.97825H8.02169H8.02172V16.4365C8.34196 16.4782 8.66839 16.5 9 16.5C9.33155 16.5 9.65804 16.4782 9.97825 16.4365V9.97831V9.97828H16.4365C16.4782 9.65804 16.5 9.33161 16.5 9C16.5 8.66845 16.4782 8.34196 16.4365 8.02175Z" fill="#D80027"/><path d="M10.9556 10.9566L14.3023 14.3033C14.4563 14.1495 14.6031 13.9886 14.7432 13.8218L11.8779 10.9565H10.9556V10.9566Z" fill="#D80027"/><path d="M7.04405 10.9565H7.04399L3.69727 14.3033C3.85113 14.4572 4.012 14.604 4.17876 14.7441L7.04405 11.8788V10.9565Z" fill="#D80027"/><path d="M7.04299 7.0435V7.04344L3.69623 3.69666C3.5423 3.85052 3.39547 4.01139 3.25537 4.17815L6.12069 7.04347H7.04299V7.0435Z" fill="#D80027"/><path d="M10.9556 7.04363L14.3024 3.69681C14.1485 3.54289 13.9876 3.39605 13.8209 3.25598L10.9556 6.1213V7.04363Z" fill="#D80027"/></svg>
                          <svg v-else-if="country.id === 'ch'" class="w-4 h-4" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg"><rect fill="#d80027" width="32" height="32"/><path fill="#fff" d="M13 6h6v7h7v6h-7v7h-6v-7H6v-6h7z"/></svg>
                          <div class="truncate">
                            <span class="font-medium">{{ country.country }}</span>
                            <span class="text-slate-500 ml-1">({{ country.code }})</span>
                          </div>
                        </button>
                      </li>
                    </ul>
                  </div>
                </div>
                
                <div class="relative w-full">
                  <input 
                    v-model.trim="form.phone"
                    type="tel" 
                    id="phone-input" 
                    class="block w-full z-20 bg-slate-50 border border-slate-200 border-l-0 text-slate-900 text-sm rounded-e-lg focus:ring-[#0C2340] focus:border-[#0C2340] px-4 py-3 outline-none transition-colors" 
                    :placeholder="$t('contact.form.phonePlaceholder')" 
                    required 
                  />
                </div>
              </div>
            </div>

            <!-- Interest Selection (Condensed) -->
            <div class="pt-2">
              <label class="mb-4 block text-sm font-semibold uppercase tracking-wider text-slate-400">{{ $t('contact.form.interests') }}</label>
              <div class="grid gap-4 sm:grid-cols-3">
                <!-- Real Estate -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.realEstate ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.realEstate" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">{{ $t('contact.form.realEstate') }}</span>
                </label>

                <!-- Yachting -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.yachting ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.yachting" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">{{ $t('contact.form.yachting') }}</span>
                </label>

                <!-- Aviation -->
                <label 
                  class="flex items-center gap-3 p-4 border-2 transition cursor-pointer"
                  :class="form.aviation ? 'border-[#968243] bg-[#968243]/5' : 'border-slate-100'"
                >
                  <input v-model="form.aviation" type="checkbox" class="h-5 w-5 rounded-none accent-[#968243]" />
                  <span class="font-medium text-slate-800">{{ $t('contact.form.aviation') }}</span>
                </label>
              </div>
            </div>

            <!-- Actions -->
            <div class="space-y-3 pt-4">
              <button
                type="submit"
                class="w-full py-3.5 text-sm font-semibold text-white shadow-lg transition hover:opacity-90 disabled:opacity-50"
                :style="{ backgroundColor: colors.gold }"
                :disabled="submitting"
              >
                {{ submitting ? $t('contact.form.submitting') : $t('contact.form.submit') }}
              </button>

              <a
                class="block w-full border border-slate-200 bg-white py-3.5 text-center text-sm font-semibold text-slate-700 transition hover:bg-slate-50"
                href="https://thetenderto.com/"
                target="_blank"
              >
                {{ $t('contact.form.discover') }}
              </a>
            </div>

            <p v-if="error" class="rounded-lg bg-red-50 p-3 text-sm text-red-600">
              {{ error }}
            </p>
          </form>
        </div>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="modalOpen" class="fixed inset-0 z-[60] flex items-center justify-center bg-black/50 p-4" @click.self="closeModal">
      <div class="w-full max-w-md rounded-3xl bg-white p-6 shadow-2xl md:p-8">
        <div class="text-center">
          <div class="mx-auto flex h-14 w-14 items-center justify-center rounded-full" :style="{ backgroundColor: colors.gold }">
            <svg class="h-7 w-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h3 class="mt-4 text-xl font-bold text-slate-900">{{ $t('contact.modal.title') }}</h3>
          <p class="mt-2 text-slate-600">
            {{ $t('contact.modal.description') }} <strong>{{ form.email }}</strong>
          </p>
        </div>

        <div class="mt-6 rounded-2xl bg-slate-50 p-4">
          <div class="flex items-center justify-between">
            <span class="text-sm font-medium text-slate-700">{{ $t('contact.modal.redirect') }}</span>
            <span class="rounded-full px-3 py-1 text-sm font-bold text-white" :style="{ backgroundColor: colors.blue }">
              {{ countdown }}s
            </span>
          </div>
          <div class="mt-3 h-2 overflow-hidden rounded-full bg-slate-200">
            <div
              class="h-full rounded-full transition-all duration-1000"
              :style="{
                width: `${progressPercent}%`,
                backgroundColor: colors.gold
              }"
            />
          </div>
        </div>

        <div class="mt-6 flex gap-3">
          <a
            class="flex-1 rounded-xl py-3 text-center text-sm font-semibold text-white shadow transition hover:opacity-90"
            :style="{ backgroundColor: colors.blue }"
            href="https://thetenderto.com/"
            target="_blank"
          >
            {{ $t('contact.modal.openNow') }}
          </a>
          <button
            class="flex-1 rounded-xl border border-slate-200 bg-white py-3 text-sm font-semibold text-slate-700 transition hover:bg-slate-50"
            @click="closeModal"
          >
            {{ $t('contact.modal.close') }}
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { reactive, ref, computed, onUnmounted, watch } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const props = defineProps({
  selectedInterest: {
    type: String,
    default: null
  }
})

const colors = {
  blue: '#0C2340',
  gold: '#968243',
}

const dropdownOpen = ref(false)

const countryCodes = [
  { code: '+33', country: 'France', type: 'img', src: '/assets/Flag-France.webp' },
  { code: '+44', country: 'UK', type: 'svg', id: 'uk' },
  { code: '+1', country: 'USA', type: 'svg', id: 'us' },
  { code: '+41', country: 'Suisse', type: 'svg', id: 'ch' },
  { code: '+212', country: 'Maroc', type: 'img', src: '/assets/Flag_of_Morocco.svg.png' },
  { code: '+377', country: 'Monaco', type: 'img', src: '/assets/Flag_of_Monaco.svg.webp' },
  { code: '+34', country: 'Espagne', type: 'img', src: '/assets/Bandera_de_España.svg' },
]

const selectedCountry = computed(() => {
  return countryCodes.find(c => c.code === form.countryCode) || countryCodes[0]
})

function selectCountry(country) {
  form.countryCode = country.code
  dropdownOpen.value = false
}

const form = reactive({
  realEstate: false,
  yachting: false,
  aviation: false,
  countryCode: '+33',
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
})

// Watch for prop changes to auto-select interest
watch(() => props.selectedInterest, (newVal) => {
  if (newVal) {
    if (newVal === 'immobilier') form.realEstate = true
    if (newVal === 'yachting') form.yachting = true
    if (newVal === 'aviation') form.aviation = true
  }
})

const submitting = ref(false)
const error = ref('')
const modalOpen = ref(false)
const countdown = ref(7)
const countdownStart = 7
let timer = null

const progressPercent = computed(() => {
  const done = countdownStart - countdown.value
  return Math.max(0, Math.min(100, (done / countdownStart) * 100))
})

function closeModal() {
  modalOpen.value = false
  if (timer) {
    clearInterval(timer)
    timer = null
  }
  countdown.value = countdownStart
}

async function handleSubmit() {
  error.value = ''

  if (!form.realEstate && !form.yachting && !form.aviation) {
    error.value = t('contact.error.interest')
    return
  }

  if (!form.firstName || !form.lastName || !form.email || !form.phone) {
    error.value = t('contact.error.fields')
    return
  }

  submitting.value = true
  try {
    // Simulate API call
    console.log('Submitting:', { ...form, fullPhone: `${form.countryCode} ${form.phone}` })
    
    await new Promise(r => setTimeout(r, 700))
    modalOpen.value = true
    countdown.value = countdownStart

    if (timer) clearInterval(timer)
    timer = setInterval(() => {
      countdown.value -= 1
      if (countdown.value <= 0) {
        clearInterval(timer)
        timer = null
        window.location.href = 'https://thetenderto.com/'
      }
    }, 1000)
  } catch {
    error.value = t('contact.error.general')
  } finally {
    submitting.value = false
  }
}

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>
